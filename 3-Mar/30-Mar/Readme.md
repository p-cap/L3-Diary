# Utilizing python as my port scanner

Referencee: https://www.pythonforbeginners.com/code-snippets-source-code/port-scanner-in-python

#### Below is the code:
```
#!/usr/bin/env python
import socket
import subprocess
import sys
from datetime import datetime

# Clear the screen
subprocess.call('clear', shell=True)

# Ask for input
remoteServer    = raw_input("Enter a remote host to scan: ")
remo  teServerIP  = socket.gethostbyname(remoteServer)

# Print a nice banner with information on which host we are about to scan
print "-" * 60
print "Please wait, scanning remote host", remoteServerIP
print "-" * 60

# Check what time the scan started
t1 = datetime.now()

# Using the range function to specify ports (here it will scans all ports between 1 and 1024)

# We also put in some error handling for catching errors

try:
    for port in range(1,1025):  
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        result = sock.connect_ex((remoteServerIP, port))
        if result == 0:
            print "Port {}: 	 Open".format(port)
        sock.close()

except KeyboardInterrupt:
    print "You pressed Ctrl+C"
    sys.exit()

except socket.gaierror:
    print 'Hostname could not be resolved. Exiting'
    sys.exit()

except socket.error:
    print "Couldn't connect to server"
    sys.exit()

# Checking the time again
t2 = datetime.now()

# Calculates the difference of time, to see how long it took to run the script
total =  t2 - t1

# Printing the information to screen
print 'Scanning Completed in: ', total
```

### /Library/Developer/........./Versions/3.8/lib/python3.8/socket.py
- Looking at the source code of the module was very helpful
- It helped me see if the socket moduel would work on my system

### ```result = sock.connect_ex((remoteServerIP, port))```
- the code above is the core of the port scan to determine whether a port it is open or not. 
```
  result = sock.connect_ex((remoteServerIP, port))
        if result == 0:
            print "Port {}: 	 Open".format(port)
        else:
				print(result)
```
- I also added a print(result) in the else condition to see what result we'll be getting. I tested it and I was getting a 61
### Practice timestampping
- t1 = datetime.now() => grab timestamp before the scan begins
- t2 = datetime.now() => grab timestamp after socket.close()
