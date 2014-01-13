# Memo

### Build image

```
docker build -t test/centos_64_python .
```

### Run container with listening ssh port

```
docker run -d -p 22 test/centos_64_python
```

### Connect via ssh

```
ssh -i ./id_rsa ore@IPADDR -p FORWARDING_PORT
ex: ssh -i ./id_rsa ore@172.17.42.1 -p 49155
```

IPADDR is the IP address of docker0 interface.
You can get to know FORWARDING_PORT following command.

```
docker port CONTAINER_ID 22
```

