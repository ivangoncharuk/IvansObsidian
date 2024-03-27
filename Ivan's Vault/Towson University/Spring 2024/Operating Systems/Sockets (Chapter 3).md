---
tags:
  - COSC-439
  - spring2024
---

# Sockets

## What is a Socket?
Imagine a socket as a **mailbox** in the digital world. It's the endpoint where you can send or receive messages in a networked environment. Just like how every mailbox has a unique address, each socket has a unique identity defined by an IP address and a port number.

## Anatomy of a Socket Address
A socket address is like a specific **apartment number** on a long street (IP address) with a unique **door number** (port number). For example, `161.25.19.8:1625` refers to **apartment 161.25.19.8**, door number **1625**. This format ensures that messages are delivered to the correct application on a particular device in the network.

## Communication Via Sockets
Communication over a network happens between pairs of sockets, akin to a **phone call** between two unique phone numbers. Just as both callers must know each other's numbers, both ends of a network communication must know the socket addresses to exchange information.

## Ports: The Special Numbers
Ports are like **channels** on a TV. Just as channels below a certain number (like 1024) are reserved for specific broadcasts, ports below 1024 are well-known and designated for standard internet services. They ensure that common services are found at the same "channel" across all computers.

## The Loopback Address: 127.0.0.1
The special IP address `127.0.0.1`, known as the **loopback** address, is like calling your own phone. It's used to send a message from a computer to itself. This is useful for testing and development, ensuring that software can communicate internally without reaching out to the wider internet.

![[host_webserver_sockets.png| 600]]


## Code Example
```java
import java.net.*;
import java.io.*;

public class DateServer
{
    public static void main(String[] args) {
        try {
            // Create a server socket bound to port 6013
            ServerSocket sock = new ServerSocket(6013);
            
            // The server runs in an infinite loop, always listening for connections
            while (true) {
                // Listen for and accept a connection from a client
                Socket client = sock.accept();
                
                // Set up a PrintWriter to send data to the client
                PrintWriter pout = new PrintWriter(client.getOutputStream(), true);
                
                // Send the current date and time to the client
                pout.println(new java.util.Date().toString());
                
                // Close the client socket and go back to listening for new connections
                client.close();
            }
        }
        catch (IOException ioe) {
            // If an I/O error occurs, print the exception
            System.err.println(ioe);
        }
    }
}
```

### Explanation of the Code

The code defines a `DateServer` class with a `main` method, the entry point of the program.
It creates a `ServerSocket` on port 6013, which listens for incoming TCP connections.
In an infinite loop (`while (true)`), the server waits for a client to connect.
When a client connects, a `Socket` instance for the client is created (`sock.accept()`).
A `PrintWriter` is attached to the client's output stream, allowing the server to send data to the client.
The current date and time are sent to the connected client.
After sending the date, the server closes the client's socket and waits for the next connection.
If an `IOException` occurs, it is caught and printed to the error stream.

## Notes on Socket Types

- Connection-oriented (TCP): Reliable, connection-based communication (like making a phone call). Data is guaranteed to arrive in order and without errors.
- Connectionless (UDP): Unreliable, connectionless communication (like sending a letter). Data may be lost or arrive out of order, but it's faster due to less overhead.
- `MulticastSocket` class: This is used for sending data to multiple recipients simultaneously (like a radio broadcast). It extends `DatagramSocket` and is used for UDP communication that supports sending packets to a group of listeners.

The given `DateServer` uses a TCP socket because it requires a reliable, point-to-point connection that ensures the data (current date and time) is accurately delivered to the client.


# Pipes in Inter-Process Communication (IPC)


## Ordinary Pipes:
- Function as a conduit for IPC, allowing a one-way data flow between processes.
- Created by a parent process to communicate with a child process, forming a parent-child relationship.
- Behave in a standard producer-consumer fashion:
  - **Producer**: Writes to the write-end (`fd[1]`).
  - **Consumer**: Reads from the read-end (`fd[0]`).
- Are unidirectional, meaning data flows in a single direction.
- Referred to as anonymous pipes in Windows.

## Named Pipes
- Differ from ordinary pipes in that they can be accessed by any process, without requiring a parent-child relationship.
- Named Pipes are more powerful than ordinary pipes
- Communication is bidirectional
- No parent-child relationship is necessary between the communicating processes
- Several processes can use the named pipe for communication
- Provided on both UNIX and Windows systems Named pipes are created with the `CreateNamedPipe()` function in Windows.


![[pipe_parent_child.png| 800]]
## Diagram Explanation
- Shows an ordinary pipe with two endpoints, connected to both the parent and the child process.
- The parent has file descriptors `fd[0]` and `fd[1]`, where `fd[1]` is typically used to write data into the pipe.
- The child also has file descriptors `fd[0]` and `fd[1]`, where `fd[0]` is used to read data from the pipe.
- This setup facilitates a unidirectional flow of data from the parent to the child.


# Remote Procedure Call (RPC)

![[Remote Procedure Call (RPC)]]





