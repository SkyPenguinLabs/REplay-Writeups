---
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Thread and Routine Manager

Inside of this level and the next level exists **multiple** different anti-tampering, anti-debug, anti-write, anti-read, and many more anti-analysis and exploitation techniques.

All of these systems (at least in Level 2) constantly execute on their own clocks. These systems continue to execute until the threads are stopped during GUI cleanup or the threads are killed via signal that the user wants to quit the application.&#x20;

In order to finish most of these levels, finding the security systems involved is pretty important- however, you must locate the thread manager as specified in [locating-the-thread-management-calls.md](../locating-the-thread-management-calls.md "mention"). This page showcases the source code and explains the system.

## Source Code

This application is entirely written using C++20 in conjunction with the Windows API. The source code below defines the threading system.

```cpp
class Framework_TaskManager {
public:
    // Class construction
    Framework_TaskManager() : Task_Manager_TerminationCall(false) {}

    // Deconstruction
    ~Framework_TaskManager() {
        Terminate();
    }

    // Add newer tasks, note: this is a vector of tasks, again, not an array. fuck.
    // Also: Adding task can run every cycle for said amount. For example, run every 5 seconds
    void AddTask(std::function<void()> task, std::chrono::seconds interval) {
        Tasks.emplace_back(std::move(task), interval);
    }

    // Start the task and thread 
    // this will start the thread and the task and will properly execute
    void Start() {
        if (!thread.joinable()) {
            thread = std::thread(&Framework_TaskManager::Task_Manager_ExecutionThreadStep, this);
        }
    }

    // Terminate or remove the thread
    void Terminate() {
        {
            std::lock_guard<std::mutex> lock(MutX);
            Task_Manager_TerminationCall = true;
        }

        ConditonalVar.notify_all();

        if (thread.joinable()) {
            thread.join();
        }
    }
private:
    // Since we are adding tasks and ensuring that tasks are secure
    // we want to create a structure to define tasks which will include 
    // a function and the time in which the task is executed.
    struct Task {
        std::function<void()> task;
        std::chrono::seconds interval;
        std::chrono::steady_clock::time_point nextRun;

        Task(
            std::function<void()> t, std::chrono::seconds i)
            : task(
                std::move(t)),
            interval(i),
            nextRun(std::chrono::steady_clock::now() + i) {}
    };

    std::vector<Task> Tasks;
    std::mutex MutX;
    std::condition_variable ConditonalVar;
    bool Task_Manager_TerminationCall;
    std::thread thread;


    void Task_Manager_ExecutionThreadStep() {
        std::unique_lock<std::mutex> lock(MutX);

        while (!Task_Manager_TerminationCall) {
            ConditonalVar.wait_until(
                lock,
                Tasks.front().nextRun,
                [this] {
                    return Task_Manager_TerminationCall || std::chrono::steady_clock::now() >= Tasks.front().nextRun;
                }
            );

            if (!Task_Manager_TerminationCall) {
                for (auto& task : Tasks) {
                    task.task();
                    task.nextRun = std::chrono::steady_clock::now() + task.interval;
                }
            }
        }
    }
};
```

The idea of this manager is to allow developers to

* 1: Initialize the class&#x20;
* 2: Create a set of functions they want to execute
* 3: Specify what time those functions are supposed to re-execute on the thread
* 4: Terminate all threads internally when required.

Pretty much, its a digital taks and routine manager that allows us to write flexible, portable, and semi-safe code for non-thread-safe GUI libraries such as ImGUI (_since using regular threads can cause the GUI rendering to crash depending on placement and location_)

### Use of the class

Below, a program is built demonstrating the capabilities of this manager.

```cpp
#include <Windows.h>
#include <iostream>
#include <thread>
#include <functional>
#include <mutex>
#include <vector>
#include <chrono>

class Framework_TaskManager {
  // Hiding this to save your eyes
};

void HelloWorld() {
    Sleep(1000);
    std::cout << "Hello world\n";
}

int main() {
    MessageBoxA(nullptr, "Starting security systems", "security", MB_OK);
    Framework_TaskManager SecThreading;
    SecThreading.AddTask([] {
        HelloWorld();
    }, std::chrono::seconds(1));
    SecThreading.AddTask([] {
        int i = 0;
        std::cout << "andndddd";
        i += 1;
        std::cout << "Value of i [" << i << "]" << std::endl;
    }, std::chrono::seconds(3));
    SecThreading.Start();
    while (true) {
        std::cout << "\n";
        Sleep(4000);
    }
    return 0;
} 
```

