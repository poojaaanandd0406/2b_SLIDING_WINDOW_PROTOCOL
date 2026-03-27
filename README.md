# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## server.py
 ```
import socket

# Step 1: Create socket and bind
server = socket.socket()
server.bind(('127.0.0.1', 12345))
server.listen(1)
print("Server is listening...")

# Step 2: Accept connection
conn, addr = server.accept()
print("Connected with", addr)

# Step 3: Ask how many frames to send
num_frames = int(input("Enter number of frames to send: "))
frames = list(range(num_frames))   # frames are just numbers [0,1,2,...]

# Step 4: Send frames one by one
for frame in frames:
    print(f"Sending frame: {frame}")
    conn.send(str(frame).encode())   # send frame
    ack = conn.recv(1024).decode()   # wait for ACK
    print(f"Received: {ack}")

print("All frames sent.")
conn.close()
```
## client
```
import socket

# Step 1: Connect to server
client = socket.socket()
client.connect(('127.0.0.1', 12345))

# Step 2: Receive frames one by one
while True:
    data = client.recv(1024).decode()
    if not data:   # connection closed
        break
    print(f"Frame received: {data}")
    client.send("ACK".encode())   # send acknowledgement

client.close()
```

## OUTPUT
<img width="1009" height="332" alt="image" src="https://github.com/user-attachments/assets/3dc59174-fa17-4278-ae4c-0cdd8d119f3e" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

