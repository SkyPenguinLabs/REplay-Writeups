---
cover: ../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Methodologies and Theory

When looking for network related actions in applications- it helps us a ton to understand the idea of our application. Lets go over some theory and stuff that can help you locate these systems with ease.

## Logical Implementations

For any client side and locally hosted server, there is always going to be multiple steps that are included in developing the server. Lets go over them.

### Where?

A lot of times, we need to plan out where we are going to host it. This also includes the ports and where a user can access it (_via curl or browser?_). This is a pretty simple layout!

* **Port**: In many common applications, servers are started on port numbers like 8080, 8090, and in many cases static sets of locations like 5555 and 4444.&#x20;
* **Location**: This is the address where the server is going to be on- most of the times this server is going to be hosted locally on localhost.

These two components are what make up where the server is going to be located- however, you have a middle man here, someone who actually manipulates **where** data is going to be sent. This is known as the server router and it is essentially one big map of keys and values where the keys are the request paths as a user would request them such as `api/v1/login` and the values are the REAL paths that the server is going to serve or display such as `/static/api/v1/login/login_form.html` or a remote URL where the resource is fetched (sometimes from a CDN).

### How? and What?

How is the component that tells us how the user is going to be sending the server data. If the user need to use something like CURL, then it may only accept CURL specific user agents (_which can be modified in a browser or with specific testing tools_). Other times, this is unmodified. Generally speaking there may also be different forms of authentication and authorization.

> **NOTE: AUTHENTICATION AND AUTHORIZATION ARE NOT THE SAME THING!** \
> \
> Authentication is verifying the identity of a user\
> Authorization is determining what resource the user is allowed to access

This server is pretty basic and we will figure that our as exploration goes further with it.&#x20;

## Finding Local Services

In order to verify a server or service is actually running, we can invoke a simple powershell command to check if a specific process has opened a port on local host. We can also port scan the localhost but that does not help us much in this case because even though we know a port is open, we do not know what process started it. We do not want to chase our tails trying to find a server if we never validating that server exists in the application we are reversing.

To verify that this program does run a server- we can call the following command.

`Get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess`

This command will output what process is running on port 8080. If you want, you can easily build a brute forcing program that runs this command and filters through every single port on the system with a basic powershell script. This powershell script is made and defined in the page linked below.

{% content-ref url="../../../level-exploits-scripts/brute-forcing/process-port-discovery.md" %}
[process-port-discovery.md](../../../level-exploits-scripts/brute-forcing/process-port-discovery.md)
{% endcontent-ref %}

When running this command or script, we eventually discover that the process `SkyOverlay` is running port `8080`. While we are not absolutely certain that this is a server, we can try to access this part of the application using `localhost:8080` since this is rendered as a local port on the local machine.

When we dile this service we get the following webpage.

<figure><img src="../../../../../.gitbook/assets/REplayWebPage.png" alt=""><figcaption></figcaption></figure>

WOO! We found the server! Now we just need to actually verify and locate this server routine!

## Other Methods and Techniques

Finding local services are not always this easy- local servers may also only be used simply for a singular session or single routine- so its important that we understand some ways and other techniques to view or verify that a server or local connection is being made especially statically. Lets check them out!

### Libraries and Imports

As the entire theme of this level has been, imports have been a really good friend to us and they will continue to be our friends the more we get into this level. In many scenarios, developers will not go through the work to implement their own sockets and their own systems for raw local connections as it is too much work and super unsafe for them to do so- programmatically and security wise if you do not know what you are doing.

Alas: many applications that initialize local connections just use the Windows Sock API which is provided by libraries such as Ws2\_32.dll as a way to implement the Winsock API, in turn providing TCP/IP networking functionality at ease. Since our server is local- we can look for import symbols from libraries like Ws2\_32.dll like the following.

* `send` : used for sending data over a connection
* `recv` :  used for receiving data from a connection
* `WSACleanup`: used for cleaning up functions using the `WinSocketApi`
* `WSAStartup`: Used for starting the `WinSocketApi`
* `socket`: Used to initialize a connection&#x20;
* `bind`: Used to bind to a specific address such as _**localhost**_ on a port like _**8080**_
* `listen`: Used to listen for incoming connections on the existing socket
* `close/closesocket`: Used for terminating a connection

All of these functions are helpful for us pinpointing the following parts of the server -

* `Initiation and Setup of the server:` This can help us pinpoint misconfigurations, errors and even more information that can help us further down the line either during further enumeration or exploitation phases.
* `Endpoints on the server:` Endpoints on the server are also going to usually be custom configured using routers- but, when figuring out where specific connections are terminated- we can use this as leverage to track down the endpoint the data was being received at- since most of the times, when data is sent or received then handled, the socket is then closed and the connection is terminated and status is then returned to the initial caller.&#x20;
* `How the server is destroyed:` How the server is cleaned up will tell us if there is anything being leaked or left open after the server is crashed. Knowing this can also help us figure out what we can leverage in the exploitation phase.
* `How the server accepts data:` This is a PRIME help when we want to do exploitation over sockets. By being able to trace and understand how the server handles data on the client side, we can possibly leverage outside connections to send malicious data to the data handler.
* `How the server is setting up calls:` In many scenarios, I have come across servers that were not meant to be interacted with by users and instead is only there for the program to momentarily store and accept data or for interoperability between similar programs/devices. Being able to reverse engineer this will tell us what protocols the server is using to send and receive data, what transportation methods and all that the program is using.

### Error Messages Or Weird Strings

Strings are not always going to be easy to see in a program. A lot of times, game cheaters especially go to the length to encrypt EVERYTHING! However, when you get to further analysis- you may be able to spot some breadcrumbs such as UUIDs left in the wild OR you may find some really simple character like `}` used in the same location as some of the server calls.

For example, say we discovered the server and we started messing around with it and found out that the sever parses user inputs via brackets and colons. Sometimes, developers will leave these out in the wild because they do not think its helpful at all! However, when you analyze smaller symbols or characters like this- especially when you see them adjacent to each other in the program, further analysis will show that this might be apart of the server.&#x20;

Error messages are another big thing- some developers choose to use standard `MessageBoxA` calls to call warning messages or even sucess notices! Being able to trace these down gives you a pretty easy in to said location of the error. In this case, you might land in an area where that same call is used to tell the user that the server did not start or an error occured where the server may be required for the application to even run (despite whether or not there is a need for user interaction or not).





