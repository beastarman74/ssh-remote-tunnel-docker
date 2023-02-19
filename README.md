# ssh-remote-tunnel-docker
SSH SSH remote tunnel docker.


https://hub.docker.com/r/beastarman/ssh-remote-tunnel

With thanks to https://hub.docker.com/r/nowsci/sshtunnel which helped me understand the method of starting a tunnel in a docker image.

This is a similar image but has only 100 ports exposed - 10000 - 100100 instead of exposing all ports. Having all ports exposed seemed to create a significant slow down in docker ps, portainer, and android docker apps when using multiple container tunnels.

example docker-compose file:









```
version: '3'
services:
  ssh-remote-tunnel:
#    build: .
    image: beastarman/ssh-remote-tunnel
    container_name: ssh-remote-tunnel
    ports:
      - "10001:10001" # change the required port within 
    volumes:
      - ssh-remote-tunnel-data:/data/:ro
 #     - ssh-key:/ssh
    environment:
      - TUNNELHOST=123.123.123.123 # or hostname
      - TUNNELPORT=22
      - LOCALHOST=123.123.123.123 # or hostname, or possibly container name if sharing same docker network
      - LOCALPORT=80
      - REMOTEPORT=10001
      - KEY=/data/sshkey-filename
      #     
    restart: always
    networks:
       sshtunnel: # change this and the below definition to match docker network of container if tunneling to container is required 

networks:
  sshtunnel:
     driver: bridge
     name: sshtunnel

volumes:
  ssh-remote-tunnel-data:
```


