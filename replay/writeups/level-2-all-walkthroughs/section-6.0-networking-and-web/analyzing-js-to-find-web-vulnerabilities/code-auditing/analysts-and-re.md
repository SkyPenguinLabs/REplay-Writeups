# Analysts & RE

Reverse engineers and security analysts, believe it or not do have some form of coordination. It just depends on where you see the field most. During these writeups and the REplay shitshow, you may have realized that I did try to add an element of code auditing from binaries all the way up to javascript which is this section.

Often times, when reversing in more specific and secure environments such as the Apple TV environment, auditing source code might be hard because everything is **most likely** pre-compiled and is shipped with the IoT device. Not to mention - companies like Apple are using their own languages and may even be using plugins, libraries and more that may require more reversing due to the lack of documentation or simply undocumented use case. &#x20;

However, in smaller environments, ones that may not be super secure and held right, you may be able to find that an application loads a specific Javascript file, this will also happen for many cheap end Desktop applications written using Python3 with a JS Desktop-app experience.&#x20;

It is through the sysinternals suite, or tools that exists in suites alike or standlone, that we are able to easily discover whether or not an application is pulling up a JS file and of course, our JS auditing goes crazy.&#x20;

### Why does this section exist?

Honestly, I have spent a lot of time auditing source code and at the time of writing recently had signed a security analyst contract at a company. At that company, I **was** for the time sake, auditing Javascript code and checking for any obvious or even complex flaws + things that could generally be changed.&#x20;

Of course, this is a corperate environment and due to the lack of training resources I do not have, I felt that maybe I should build my own training environment and link it with REplay as an extension - JS play.
