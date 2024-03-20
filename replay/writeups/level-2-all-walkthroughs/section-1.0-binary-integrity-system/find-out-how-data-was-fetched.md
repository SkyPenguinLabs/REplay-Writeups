---
description: >-
  Solves Objective: Figure how the data fetched remotely and what was called to
  get it to fetch the resource
cover: ../../../../.gitbook/assets/TheWorldIsYours.png
coverY: 0
---

# Find out 'how' data was fetched

### What is this task?

This task just asks you to explain how the data for the binary integrity system was checked.&#x20;

### Answer

This is pretty easy to solve- but basically, the binary integrity system used a website called pastebin to store production hashes of the original binary and used curl to fetch this information. We can confirm that this was curl and this was a system command being executed by using ProcMon and filtering for command API calls.

Found and discovered in - [file-location-of-the-hash.md](file-location-of-the-hash.md "mention")
