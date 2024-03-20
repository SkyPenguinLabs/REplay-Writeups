---
description: >-
  Solves Objective: There was a vulnerability in the website itself, what was
  it?
cover: ../../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Analyzing JS To Find Web Vulnerabilities

### What is this task?

In many scenarios, JavaScript is going to be obfuscated to ensure that users are not sure of what they are reading. In this case, we need to analyze the obfuscated JS we found that is loaded by the server to find a vulnerability in the web application itself.&#x20;

## Analyzing the JS file

The JS portion of the file is shown below.

```javascript
    function submitForm() {
        var u = C;
        (function (Q, t) {
            var F = C,
                r = Q();
            while (!![]) {
                try {
                    var N =
                        (-parseInt(F(0x13a)) / 0x1) * (-parseInt(F(0x128)) / 0x2) +
                        (parseInt(F(0x136)) / 0x3) * (-parseInt(F(0x132)) / 0x4) +
                        (-parseInt(F(0x134)) / 0x5) * (-parseInt(F(0x13e)) / 0x6) +
                        (-parseInt(F(0x131)) / 0x7) * (-parseInt(F(0x120)) / 0x8) +
                        parseInt(F(0x129)) / 0x9 +
                        (parseInt(F(0x13b)) / 0xa) * (-parseInt(F(0x12a)) / 0xb) +
                        (parseInt(F(0x139)) / 0xc) * (-parseInt(F(0x12d)) / 0xd);
                    if (N === t) break;
                    else r["push"](r["shift"]());
                } catch (i) {
                    r["push"](r["shift"]());
                }
            }
        })(f, 0x6c2a7);
        var email = document[u(0x13d)](u(0x12e))[u(0x135)],
            password = document["getElementById"](u(0x121))["value"],
            adminID = document[u(0x13d)](u(0x123))[u(0x135)];
        document[u(0x138)](adminID + email + password);
        function f() {
            var s = [
                "stringify",
                "open",
                "870898ddRapz",
                "5312CqOWpj",
                "DONE",
                "230cFKJvr",
                "value",
                "1086AQGOJa",
                "application/json",
                "write",
                "60MKFvLp",
                "58605FYlsJZ",
                "55010LLYklq",
                "log",
                "getElementById",
                "85362XoYmoR",
                "8vGEAqd",
                "password",
                "readyState",
                "AdminID",
                "status",
                "POST",
                "Login\x20successful",
                "error",
                "30ypsnUw",
                "6514443bjEGYC",
                "550NccHiX",
                "send",
                "Content-Type",
                "3075605yntfOU",
                "email",
            ];
            f = function () {
                return s;
            };
            return f();
        }
        function C(Q, t) {
            var r = f();
            return (
                (C = function (N, i) {
                    N = N - 0x120;
                    var F = r[N];
                    return F;
                }),
                C(Q, t)
            );
        }
        var formData = { email: email, password: password, adminID: adminID };
        console[u(0x13c)](formData);
        var xhr = new XMLHttpRequest();
        xhr[u(0x130)](u(0x125), "/api/v2/login", !![]),
            xhr["setRequestHeader"](u(0x12c), u(0x137)),
            (xhr["onreadystatechange"] = function () {
                var I = u;
                xhr[I(0x122)] === XMLHttpRequest[I(0x133)] && (xhr[I(0x124)] === 0xc8 ? console[I(0x13c)](I(0x126)) : console[I(0x127)]("Login\x20failed"));
            }),
            xhr[u(0x12b)](JSON[u(0x12f)](formData));
        u();
    }
```

Ah shucks! Its been obfuscated! No problem- we can see a few interesting things here.

* **The endpoint** -> <mark style="color:red;">/api/v2/login</mark> in (`xhr[u(0x130)](u(0x125), "/api/v2/login", !![])`)
* **The way data is being concatenated ->** `document[u(0x138)](adminID + email + password);`

Now, I am going to leave this next part to you. Is there any sanitization involved with the way data is being added together? if not, then this is what this means-

{% hint style="info" %}
The web server is vulnerable to XSS, think about how we would make our payload
{% endhint %}

{% content-ref url="answer-page.md" %}
[answer-page.md](answer-page.md)
{% endcontent-ref %}
