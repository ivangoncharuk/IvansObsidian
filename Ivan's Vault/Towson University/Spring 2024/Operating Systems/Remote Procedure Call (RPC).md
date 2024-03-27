---
tags:
  - spring2024
  - COSC-439
---
## Overview
RPC is like a magical intercom system that allows you to request services from a different room in a large building (networked systems). It abstracts the complexity of the underlying communication.

## How It Works
- **Stubs**: Think of a stub as a personal assistant. On the client side, the stub is responsible for finding the correct room (server) and explaining what you need (marshalling parameters). On the server side, it's the assistant that understands your request, unpacks it, and carries out the task (procedure).

- **Service Differentiation**: Just like different departments in a building have unique extension numbers, RPC uses ports to differentiate services.

- **Data Representation**: The External Data Representation (XDR) format is like a universal translator, ensuring that everyone in the building (different architectures) understands your request, regardless of the language they speak (big-endian or little-endian).

- **Reliability**: Remote communication via RPC is more prone to failure than just walking over to another room. The messages are designed to be delivered exactly once, providing more reliability than just hoping your message gets there "at most once".

- **Matchmaker Service**: The OS provides a matchmaking service, like a receptionist who connects calls, to help the client find the server.

## Execution of RPC Flowchart

![[Pasted image 20240212114822.png | 700]]

The flowchart illustrates the RPC message exchange process:
  1. **User Request**: A user on the client side requests a service (RPC message) to be performed.
  2. **Kernel Call**: The client's kernel sends this request to a matchmaker to find out where to send the RPC (to get the port number).
  3. **Matchmaker Response**: The matchmaker, upon receiving the message, looks up the server's details and responds with the port number `P`.
  4. **Kernel Update**: The client's kernel updates the RPC message with the correct port and sends it off.
  5. **Server Processing**: A daemon listening on the server side receives the message and processes the request.
  6. **Server Response**: Once processed, the server's daemon sends back the result to the client's kernel, which in turn passes it back to the user.

The image shows this as a back-and-forth communication between a client and server, facilitated by an intermediary matchmaker.

