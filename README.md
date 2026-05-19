# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download

## AIM :

To write a Python program for socket for HTTP for web page upload and download

## Algorithm:

1.Start the program.

2.Get the frame size from the user

3.To create the frame based on the user request.

4.To send frames to server from the client side.

5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.

6.Stop the program

## Program:

Server.py

```

import socket

s = socket.socket()
s.bind(("localhost",3024))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
   
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
       f = open("index.html","r")
       data = f.read()
       f.close()

       response = "HTTP/1.1 200 OK\n\n" + data
       c.send(response.encode())

    elif "POST" in request:
       data = request.split("\n\n")[1]

       f = open("upload.txt","w")
       f.write(data)
       f.close()

       c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    
    c.close()

```

Client.py

```

import socket

s = socket.socket()
s.connect(("localhost",3024))

ch = input("1.Download 2.Upload : ")

if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())


s.close()


```

## OUTPUT:

<img width="1480" height="435" alt="image" src="https://github.com/user-attachments/assets/10dff5ca-9467-4179-b0ed-90e661f89d2c" />

<img width="1482" height="443" alt="image" src="https://github.com/user-attachments/assets/68cce941-3226-4a63-8c99-478b623b15ef" />


## Result:

Thus the socket for HTTP for web page upload and download created and executed successfully.
