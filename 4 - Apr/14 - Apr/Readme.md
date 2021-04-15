## Python script that checks the a file exits, if the ip has the proper format and if we can connect to the ip via ping

```
import os.path
import sys
import subprocess

ip_file = input("\n# Enter file: ")

# CHECKS IF THE FILE EXISTS
if os.path.isfile(ip_file) == True:
	
	selected_ip_file = open(ip_file, 'r')	
  
  # READS THE FILE AND TURNS IT INTO AN ARRAY
	ip_list = selected_ip_file.readlines()
  
  # MAKE SURE YOU CLOSE THE FILE
	selected_ip_file.close()
	
	for ip in ip_list:

		ip = ip.rstrip("\n")
		octet_list = ip.split('.')
		
		if (len(octet_list) == 4) and (1 <= int(octet_list[0]) <= 223) and (    int(octet_list[0]) != 127) and (int(octet_list[0]) != 169 or int(octet_list[    1]) != 254) and (0 <= int(octet_list[1]) <= 255 and 0 <= int(octet_list[2])     <= 255 and 0 <= int(octet_list[3]) <= 255):
			
			ping_reply = subprocess.call(["ping", ip, "-c", "2"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
			
			print(ping_reply)
			
			if ping_reply == 0:
				print("\n* {} is reachable :)\n".format(ip))
			else:
				print("\n* {} not reachable :( Check connectivity and try again.\n".format(ip))				
				sys.exit()
			continue
		
		else:
			print('\n* There is an invalid IP address in the file: {}: (\n'.format(ip))		
```
