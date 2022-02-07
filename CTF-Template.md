# OffSec Proving Grounds: Linux-WebCal

- MY IP:<br />
192.168.49.139<br />

- TARGET:<br />
192.168.139.97<br />

----

## Table of Contents
- [Reconnaissance](#reconnaissance)
- [Initial Exploits](#initial-exploits)
- [Privilege Escalation](#privilege-escalation)

---

## Reconnaissance

sudo nmap -vv -p0- 192.168.139.97 -oA allPorts

sudo nmap -vv -p22,23,25,53,422,8091,42042 -A 192.168.139.97 -oA openPorts

gobuster dir -u http://192.168.139.97:8091/ -x php,txt,html -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 150 -o gobuster.log

nikto -h "http://192.168.139.97:8091/" | tee nikto.log

---

## Initial Exploits

```
cat /home/????/local.txt

type c:\users\????\desktop\local.txt

```

---

## Privilege Escalation


```
cat /root/proof.txt

type c:\users\administrator\desktop\proof.txt

```

---


---

### Procedures to get a stable reverse shell

Method 1

- rlwrap -r -f . nc -nvlp 445<br />

Method 2<br />

(1) Local machine<br />
- bash

(2) Target machine with the reverse shell<br />
- python -c "import pty; pty.spawn('/bin/bash')" <br />
	OR<br />
	python3 -c "import pty; pty.spawn('/bin/bash')" <br />

- CTRL+Z<br />

(3) Local machine<br />
- stty -a<br />
	rows 35; columns 179<br />
- echo $TERM<br />
	xterm-256color<br />
	
- stty raw -echo<br />
- fg<br />
- reset<br />
- export SHELL=bash && export TERM=xterm && stty rows 30 columns 176<br />

----




