# Environment analysis when running ```npm run pcap ```

### My tool script => the first argument should be the PID of the process of interest

```
#!/bin/zsh

if [ -n "$1" ]; then # if the first parameter exists

	printf "\n"
	netstat -anv | head -n 2
	netstat -anv | grep $1

	printf "\n"
	echo "################################"
	ps -f $1

	printf "\n"
	lsof -p $1

else
	echo "No paramater found"

fi
```

### When running ``` npm run pcap ```, two processes are enabled
```
 PID TTY           TIME CMD
???? ttys001    0:00.27 npm   
???? ttys001    0:00.43 node index.js
```

### ```lsof -p ????```
I found files that associated communication between node and mongodb 

### SSL communication
Comm between node and mongodb towards the end after callng an endpoint rides on SSL????

## I am still working on basic bash scripting


