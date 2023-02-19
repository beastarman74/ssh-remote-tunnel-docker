# ssh-remote-tunnel-docker
SSH remote tunnel docker.

https://hub.docker.com/r/beastarman/ssh-remote-tunnel








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


