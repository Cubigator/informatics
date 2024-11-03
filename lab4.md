```Dockerfile
FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y libaa-bin
RUN apt-get install -y iputils-ping

ENV TERM=xterm 
```

```
docker build . -t fire
```

```
docker run --name fire1 -it fire
docker run --name fire2 -it fire
```
![image](https://github.com/user-attachments/assets/de556217-2203-4c1d-97c8-b9c53f47310e)

![image](https://github.com/user-attachments/assets/505067cd-7a84-4f75-9d05-50dccb0bb0a0)

![image](https://github.com/user-attachments/assets/7ea7b73b-c101-42db-a4e9-bf1ec4a52c6c)

PINGGS:

![image](https://github.com/user-attachments/assets/f5420450-bd14-4136-9f3a-b5c2bdaeaa6c)

![image](https://github.com/user-attachments/assets/d0b2c036-7b78-4985-aa88-b43d5070dab5)

aafire:

![image](https://github.com/user-attachments/assets/4b53eafd-c66f-463e-8843-07e596814020)

![image](https://github.com/user-attachments/assets/315c6bfa-7c95-43f5-a70c-c63e39cc0112)

