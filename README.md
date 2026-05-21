# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 

server.py

```


import socket
s = socket.socket()
s.bind(("localhost",8080))
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


client.py


```


import socket
s = socket.socket()
s.connect(("localhost",8080))
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


## OUTPUT

<img width="1156" height="251" alt="Screenshot 2026-05-21 205446" src="https://github.com/user-attachments/assets/bae6a78e-73f6-418f-b1b1-6850b2106485" />

1.UPLOAD OUTPUT:

<img width="1242" height="297" alt="Screenshot 2026-05-21 205454" src="https://github.com/user-attachments/assets/2ca02209-fcc8-4fa0-bbae-458dfe0fe0be" />

2.DOWNLOAD OUTPUT:

<img width="683" height="457" alt="Screenshot 2026-05-21 205624" src="https://github.com/user-attachments/assets/6c79a7c2-7e68-4a93-b319-b86e7153d122" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
