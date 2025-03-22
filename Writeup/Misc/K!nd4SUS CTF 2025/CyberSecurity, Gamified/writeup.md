# Introduction

Author: [cridin1](https://github.com/cridin1)\
Name: CyberSecurity, Gamified\
Solves/Points: 4 solves / 498 points
> Description: Solve a series of cybersecurity-related tasks in order to get your well-deserved flag!

# Description
The challenge starts on the [website](http://chall.ctf.k1nd4sus.it:30042/), where a chat using [Quixe](https://eblong.com/zarf/glulx/quixe/) is exposed.

# Exploit
By looking at the website requests, we can see that one interprets a gblorb payload:

```
Request:
http://chall.ctf.k1nd4sus.it:30042/interpreter/Cybersecurity,%20Gamified.gblorb.js
```

```
Response in Javascript:
$(document).ready(function() {
    GiLoad.load_run(null, 'R2x1bAADAQIABwYAAAkFAAAJBQAAAQAAAAAAPAAFcrgW9k7HSW5mbwABAAA2LjQxMC4zOAABMjUwMzA0wQAAMAMAAATVADEAwQQCAAARGQkAAQBAiQRAgQdAiQBAgQMwEwAAA8vKBDEBAcEEAgAAERkJAAEAQIkEQIEIQIkAQIEDMBMAAAPLygQxAQHBBAIAABEZCQQBBBEZCQABAECJBECBBkCJAECBAzATAAADy8oEMQEBwQQCAAARGQkAAQBAiQRAgQNAiQBAgQMwEwAAA8vKBDEBAcEEAgAAERkJBAIEERkJAAEAQIkEQIEEQIkAQIEDMBMAAAPLygQxAQHBBAIAABEZCQABAECJBECBAUCJAECBAzATAAADy8oEMQEBwQQCAAARGQkAAQBAiQRAgECJAECBAzATAAADy8oEMQEBwQQCAAARGQkAAQARGQkEAQRAiQBAgQJAiQRAgQMwEwAAA8vKBDEBAcEEAgAAERkJBAEEERkJAAEAQIkEQIEFQIkAQIEDMBMAAAPLygQxAQHBBAIAABEZCQABAECJBECBB0CJAECBBDATAAADy8oEMQEBwQQCAAARGQkAAQBAiQRAgQhAiQBAgQQwEwAAA8vKBDEBAcEEAgAAERkJBAEEERkJAAEAQIkEQIEGQIkAQIEEMBMAAAPLygQxAQHBBAIAABEZCQABAECJBECBA0CJAECBBDATAAADy8oEMQEBwQQCAAARGQkEAgQRGQkAAQBAiQRAgQRAiQBAgQQwEwAAA8vKBDEBAcEEAgAAERkJAAEAQIkEQIEBQIkAQIEEMBMAAAPLygQxAQHBBAIAABEZCQABAECJBECAQIkAQIEEMBMAAAPLygQxAQHBBAIAABEZCQABABEZCQQBBECJAECBAkCJBECBBDATAAADy8oEMQEBwQQCAAARGQkEAQQRGQkAAQBAiQRAgQVAiQBAgQQwEwAAA8vKBDEBAcEEAQAAMQDBBAEAADEBAcEEAQAAQNkAACUdAQABC3IDAAWsQSABCHIDAAWsSzEBAcEEAQAAMQDBBAEAADEB/..............', 'base64');
});
```

Using CyberChef,  we can decode the base64 string and turn that in a [file.gblorb](file.gblorb). 

Using [mrifk](https://github.com/wertercatt/mrifk), a decompiler and disassembler for the Glulx virtual machine, we can execute the tool, obtaining the [decompiled.txt](decompiled.txt):

```
.\mrifk.exe .\file.gblorb > decompiled.txt
```

By searching the string "KSUS" in the decompiled file, we can obtain the flag:

```
KSUS{Pls_K4fk4_n0w_wr1t3_4_n0v3l_4b0ut_m3_4s_w3ll}
```



