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
