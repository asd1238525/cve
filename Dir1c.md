# Responsive Blog Site has Directory Traversal Vulnerability in signup.cpp

## supplier 
https://code-projects.org/email-logging-interface-c-programming-source-code/
## Vulnerability file
signup.cpp

## describe

**Code analysis**   

In signup.cpp, the username parameter supplied by the user is used directly to construct a file-system path without any sanitization or validation. An attacker can inject directory-traversal sequences (e.g., ../), causing the application to create folders outside the intended directory.

![image-2025](https://github.com/asd1238525/cve/blob/main/e60423e6d9a5802952dae83ae2e0d086.png)


## POC

![image-2025](https://github.com/asd1238525/cve/blob/main/fa60a39473fe1d54016d5b46de5bcdff.png)

```
Input username:
../dir
The program creates:
../dir.txt
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/cf45073e27740413fa19a2678926ca7f.png)
Successfully escapes the directory and writes the file anywhere on disk.