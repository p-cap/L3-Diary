```ports=$(nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)```

```nmap -p- --min-rate=1000 -T4 10.10.10.27

RESULTS:

Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-10 19:55 UTC
Nmap scan report for 10.10.10.27
Host is up (0.14s latency).
Not shown: 65523 closed ports
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
1433/tcp  open  ms-sql-s
5985/tcp  open  wsman
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 70.00 seconds
```
```
nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] 

- picks only the lines that begins with the numbers 0-9

RESULTS:

135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
1433/tcp  open  ms-sql-s
5985/tcp  open  wsman
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
```

```
nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] | cut -d '/' -f 1

- the delimiter was '/' and show column 1

RESULTS:
135
139
445
1433
5985
47001
49664
49665
49666
49667
49668
49669
```
```
nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ','
- tr replaces the '\n' with commas

RESULTS: 
135,139,445,1433,5985,47001,49664,49665,49666,49667,49668,49669,
```
```
nmap -p- --min-rate=1000 -T4 10.10.10.27 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//
- sed removes the last comma wiht nothing

RESULTS:

135,139,445,1433,5985,47001,49664,49665,49666,49667,49668,49669
```
