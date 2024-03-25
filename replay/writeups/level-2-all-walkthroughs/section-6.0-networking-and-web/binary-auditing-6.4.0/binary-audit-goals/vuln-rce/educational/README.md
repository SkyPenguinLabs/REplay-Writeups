---
description: Educational page designed to talk about Remote Code Execution vulnerabilities
cover: ../../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# Educational

{% hint style="info" %}
Unlike the other pages such as [vuln-double-free](../../vuln-double-free/ "mention") we will be actually talking about RCE and what it is and means in a application but also&#x20;
{% endhint %}

## Exploring RCE

This section is split into multiple subsections that give you a deeper explanation of what RCE is and what accounts for it.&#x20;

### What is it?&#x20;

RCE, commonly referred to as Remote Code Execution is one of the most known and basic (_but superrr deep in which it can become quite advanced and unique_) vulnerabilities out there to exist in many applications.

> What does this mean in our scenario?&#x20;

In our scenario, which usually finding RCE on the application is done on our own client side setup- but, anyway, this means that we can execute code on the program through a series (_if needed_) of malicious input to execute a command on the program.&#x20;

### Why is this a security risk?

RCE is a huge problem on many applications, especially if it is easy to exploit remotely. These can basically be major entry points into a main system say some enterprise environment openly running the software.&#x20;

When an attacker obtains shell access or just general command execution, they can do many things on said system even if the environment is sandboxed or limited in its permissions.

### How does this happen in binaries?

In binary applications, RCE can be about anywhere and the golden rule is to not execute system commands if you can. At least- that is the golden rule I live by.

Typically, RCE happens when the program can take external data either given by the user or sent to the client from a remote device or application and does not bother to check the input before piping it or adding it to a command execution process.&#x20;

The example below demonstrates it through packet parsing (go).

```go
/*some random code here that defines packet recv and send*/

type Pkt struct {
    Data string  // General packet data
    Version int  // Version info in packet
    Src  string  // Source
    Dst  string  // Destination
}

func Parse(packet []byte) (string, error) {
    if packet != 0x00 {
        res := packetcap.Parse(*Pkt, packet)
        if res != 0xEEE {
            var str string;
            Username := res.Data;
            // check if some file exists for this user already
            var cmd string
            cmd += "find / -type f -name "
            cmd += fmt.Sprintf("`%s`", Username)
            cmd += " 2>/dev/null"
            return Exec_Syscall(cmd), nil   
        } else {
            return nil, ErrRet("Packet magic invalid")
        }
    }
}

/*Some random ass code below */
```

In this demonstrative code, this program parses a packet and throws it into a string field in the type structure `Data`. It immediately checks to see if the username which must represent a file (maybe game save data?) exists on the system. This is done via command execution on the machine.

> The bad part with this &#x20;

In this code, the program parses the packet without checking the input. If someone could reverse engineer the protocol being used here, find out the field text data and the functions that parse the packets- they could find flaws to inject malicious commands on the machine.

