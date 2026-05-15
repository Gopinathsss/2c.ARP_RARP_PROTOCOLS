# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
#arp_client
```
import socket

# Create socket
s = socket.socket()

# Connect to server
s.connect(('localhost', 8000))

print("Connected to ARP Server")

while True:

    # Get IP address
    ip = input("\nEnter Logical IP Address (or exit): ")

    # Send IP
    s.send(ip.encode())

    # Exit condition
    if ip.lower() == "exit":
        print("Connection Closed")
        break

    # Receive MAC
    mac = s.recv(1024).decode()

    print("MAC Address :", mac)

# Close socket
s.close()

```
#arp_server
```
import socket

# Create socket
s = socket.socket()

# Bind host and port
s.bind(('localhost', 8000))

# Listen for connection
s.listen(5)

print("ARP Server Waiting for Connection...")

# Accept connection
c, addr = s.accept()

print("Connected to:", addr)

# ARP Table
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA",
    "192.168.1.1": "AA:BB:CC:DD"
}

while True:

    # Receive IP
    ip = c.recv(1024).decode()

    # Exit condition
    if ip.lower() == "exit":
        print("ARP Client Disconnected")
        break

    print("\nRequested IP Address:", ip)

    # Search MAC address
    if ip in address:
        mac = address[ip]

        c.send(mac.encode())

        print("MAC Address Sent:", mac)

    else:
        c.send("IP Address Not Found".encode())

        print("Invalid IP Address")

# Close sockets
c.close()
s.close()
```

## PROGRAM - RARP
#rarp_client
```
import socket

# Create socket
s = socket.socket()

# Connect to server
s.connect(('localhost', 9000))

print("Connected to RARP Server")

while True:

    # Get MAC address
    mac = input("\nEnter MAC Address (or exit): ")

    # Send MAC
    s.send(mac.encode())

    # Exit condition
    if mac.lower() == "exit":
        print("Connection Closed")
        break

    # Receive IP
    ip = s.recv(1024).decode()

    print("Logical IP Address :", ip)

# Close socket
s.close()
```
#rarp_server
```
import socket

# Create socket
s = socket.socket()

# Bind host and port
s.bind(('localhost', 9000))

# Listen for connection
s.listen(5)

print("RARP Server Waiting for Connection...")

# Accept connection
c, addr = s.accept()

print("Connected to:", addr)

# RARP Table
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99",
    "AA:BB:CC:DD": "192.168.1.1"
}

while True:

    # Receive MAC
    mac = c.recv(1024).decode()

    # Exit condition
    if mac.lower() == "exit":
        print("RARP Client Disconnected")
        break

    print("\nRequested MAC Address:", mac)

    # Search IP address
    if mac in address:
        ip = address[mac]

        c.send(ip.encode())

        print("IP Address Sent:", ip)

    else:
        c.send("MAC Address Not Found".encode())

        print("Invalid MAC Address")

# Close sockets
c.close()
s.close()
```
## OUPUT - ARP
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/83972c26-7b7a-4003-97f7-0fdbd5d0d58a" />
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/b999712f-550e-41f3-821f-28e2135a663f" />

## OUPUT -RARP
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/abf2bb3c-d7d2-434a-b0b6-229b7495f033" />
<img width="1359" height="753" alt="image" src="https://github.com/user-attachments/assets/90f21abd-1c37-458f-95b7-ba7713fbcc6d" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
