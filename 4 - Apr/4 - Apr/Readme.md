# Using a Docker file to create a docker container

- Create the Dockerfile
```
FROM kalilinux/kali-rolling:latest

RUN apt-get update  && apt-get install -y net-tools iputils-ping kali-tools-top10 smbclient

ENTRYPOINT ["/bin/bash"]
```

- Build an image  
```docker build -t p-cap .```

- Check if the image was created  
```docker images```

- Create aa container  
```docker run -it pcap:latest ```

- If you exit from the shell, you can restart the container again by:   
```docker start -ai container_name```
