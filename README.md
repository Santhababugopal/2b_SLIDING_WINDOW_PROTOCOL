# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To write  a python program to perfrom sliding window protocal
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
CLIENT:
```
import socket

c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
L = list(range(size))
print("Total frames to send:", len(L))

s = int(input("Enter Window Size: "))

i = 0
while i < len(L):
    st = i + s
    frames_to_send = L[i:st]
    print(f"Sending frames: {frames_to_send}")

    c.send(str(frames_to_send).encode())

    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received: {ack}")

    i += s

c.close()
```
SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr=s.accept()
print(f"Connected to {addr}")


while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break


    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())


conn.close()
s.close()
```
## OUPUT
CLIENT:
![Screenshot 2025-03-12 104251](https://github.com/user-attachments/assets/3462854f-8056-4abe-a716-ddcc427745e0)
SERVER:
![Screenshot 2025-03-12 104325](https://github.com/user-attachments/assets/bf6ce979-4cf1-4b0e-9427-b02cf1e103d7)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
