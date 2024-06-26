---
layout: page
title: System Security Exploit Practice
description: The coursework on CS5231 Systems Security
img: assets/img/phrack-logo.jpeg
importance: 1
category: tech
---

# Overview
This project page is transfered from my GitHub repo with the same name, click [here](https://github.com/Hanc1999/System-Security-Exploit-Practice) to access.

Practiced several system security exploits with C language in a specific Linux image [Origin](https://drive.google.com/file/d/16WntAiUy3R-uR8M0C4kWJUu8WNLqdfFf/view), most of which aim to achieve root privileges or tamper with some data, breaking the integrity or/and the confidentiality of the system.   Some general techniques applied to the vulnerable custom programs include buffer overflow, integer overflow, format string tricks,  double free, return-to-libc, rop.   More than that, some vulnerabilities once existed in the real-world Linux versions are also exploited, including SUDO and GHTTPD.

# About the VM
The original VM image should be able to achieve from the [Origin](https://drive.google.com/file/d/16WntAiUy3R-uR8M0C4kWJUu8WNLqdfFf/view), tested on the virtualbox on MacOS. 

The repo is more for the demo and learning, for the VM image with all programs installed and exploits compiled, please check [here](https://drive.google.com/file/d/1XL04BKWcssqwin-G9ZG-VCrRrRpBGdaj/view?usp=sharing), on which you can directly try the exploits.
* VM user: student
* psw: student

# About techniques
In techniques there are 6 kinds of exploit techniques with 7 examples, the exploit code and its victim custom codea are classified into different folders. Including `buffer overflow`, `integer overflow`, `doube free`, `format string tricks`, `return2libc` and `rop`. Personally I think the `rop` is the most thrilling one.
- Before run, run the `before_run.sh` to disable ASLR (Address Space Layout Randomization, which is important to disable if we are using any absolute address in exploits) and put `basic` vulnerable programs in `/tmp` folder.
- For the rop exploit, please run the `exploit7-run.sh`. 
- For each source C exploit file please compile them first.
- The structure of the dir has been changed for better demo, if you are using the origin VM image, pelase check the Makefile and bash scripts to tune the paths.

# About real-world
For the real-world exploits, please make sure the original vulnerable versions of the programs are installed.
## SUDO
The Sudo format string vulnerability is found in 2012, with versions 1.8.0 through 1.8.3p1 inclusive. Older versions of sudo are not affected. Details in [CVE-2012-0809](https://www.sudo.ws/security/advisories/sudo_debug/).

Details: In the `sudo_debug()` implementation the program name is passed to the `fprintf()` function. Since the program name can be controlled by the user, user can well-design the program name and exploits the flaw with format string tricks.

- The implementation of the exploit with ASLR disabled can be checked in `sudo_exploit1.sh`.
- We can even apply this exploit with ASLR! With a different implementation logic, please check `sudo_exploit2.sh`. Make sure the ASLR is opened for testing this implementation.

## GHTTPD
Ghttpdv1.4 has a buﬀer overﬂow vulnerability. Details in [CVE-2002-1904](https://nvd.nist.gov/vuln/detail/CVE-2002-1904). Where the remote attacker can overflow the buffer in the host and executes the shellcode.

To start the vulnerable ghttpd:
> cd    /usr/local/ghttpd
> 
> sudo    execstack    -s    ./ghttpd
>
> sudo    ./ghttpd

# Others
- Notice GDB will be a necessary tool to exploit and learn.
- [Phrack Magzine](http://www.phrack.org/) is a good place to learn all the things.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/phrack-logo.jpeg" title="phrack-logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
