---
cover: ../../../../../../../.gitbook/assets/1_X7OK5T-GkCrtzxkW8nM8Sg.webp
coverY: 0
---

# IOF - Integer Overflow

### What is it?

In the most basic and plain step way possible- integer overflows are binary vulnerabilities that exist when the result of a mathematical operation (or just, regular standard push) actually overflows the max possible value for that data type.

If you are new to computer science (pls go back and study if you are), data types exist in many different ways. In programming languages like C/C++, because of the way they are designed, data types like integer8 have both a maximum and minimum value.

If the result of an operation such as adding one number a user supplies to another number overflows the max value for an integer8 (-9,223,372,036,854,775,808 or +9,223,372,036,854,775,807) then the program overflows and crashes.

This can also happen in an underflow scenario.

> Underflow

Integer underflow is the opposite of the overflow. Instead of reaching the max, you reach below the minimum number for the value which also results in a crash.

### Why is it a security risk?

As it may be surprising to you- Integer Overflows are a huge risk in binary applications and are one of the very smallest vulnerabilities but hardest ones to catch all the time. This is because, in more advanced environments- there is always going to be a TON of mathematical operations, especially inside of GUIs.

The only question an attacker needs to ask themselves is simply - "what can I control?"

The idea is that if they can influence the result of an operation, they can try to crash the program by underflowing or overflowing the data type IF the value is not checked or stored or handled properly.&#x20;

Primarily: Unlike BOF, this is not going to directly be immediately exploitable. Instead, the attacker is most likely going to be crafting specific inputs that can crash the program in such a way that opens a "door" if you will to exploiting the program further.

### How can it be prevented?&#x20;

Ensure that you write some form of function that will take an arithmetic operation as an input and will also then handle the result of that operation by properly storing the values and checking to see if the integer result is too large or too small. Considering that REplay uses C++, I provided a good example for you below.

```cpp
#include <iostream>

// not super secure, like god himself but it does the job it needs to
/*
    Use -> SecureExecOperation(
                <-[in].char operation
                <-[in].int Left
                <-[in].int Right
                <-[out].int result
           )

   Example:
        int arith_res;
        if (SecureExecOperation('+', 10, 20, arith_res)) {
            std::cout << arith_res << std::endl;
        } 

    Improvements:
        You can make many improvements and go down the list of values
        and eventually develop a framework that ensures for any user-influenced
        calculation, that the value being handled actually gets checked and the 
        result is properly stored. 
*/
bool SecureExecOperation(char operation, int op1, int op2, int& res) {
    switch (operation) {
    case '+':
        if ((op2 > 0 && op1 > std::numeric_limits<int>::max() - op2) ||
            (op2 < 0 && op1 < std::numeric_limits<int>::min() - op2)) {
            std::cerr << "[!] WARN: Overflow (ret->false)" << std::endl;
            return false;
        }
        res = op1 + op2;
        break;
    case '-':
        if ((op2 < 0 && op1 > std::numeric_limits<int>::max() + op2) ||
            (op2 > 0 && op1 < std::numeric_limits<int>::min() + op2)) {
            std::cerr << "[!] WARN: Underflow (ret->false)" << std::endl;
            return false;
        }
        res = op1 - op2;
        break;
    case '*':
        if (op1 > 0 && op2 > 0 && op1 > std::numeric_limits<int>::max() / op2) {
            std::cerr << "[!] WARN: Overflow (ret->false)" << std::endl;
            return false;
        }
        //-[There is a LOT more that can be done here, especially for multiplication operations
        res = op1 * op2;
        break;
    case '/':
        // A very common issue in general
        if (op2 == 0) {
            //-[Division by zero
            std::cerr << "[!] WARN: Divide by 0 (ret->false)" << std::endl;
            return false;
        }
        res = op1 / op2;
        break;
    default:
        std::cerr << "[!] Err: Invalid operation" << std::endl;
        return false;
    }
    return true;
}

int main() {
    int arith_res;
    if (SecureExecOperation('+', 10, 20, arith_res)) {
        std::cout << arith_res << std::endl;
    }
}
```

