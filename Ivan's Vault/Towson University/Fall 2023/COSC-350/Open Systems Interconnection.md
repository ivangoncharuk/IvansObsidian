#COSC-350 #fall2023 


[[COSC-350 Lecture 2]]
1. [[Transport Layer]]
2. [[Physical Layer]]
4. [[Link Layer]]
5. [[Network Layer]]


- **Application layer:** The Application layer is responsible for providing network services to applications, such as HTTP, FTP, and SMTP.
- **Transport layer:** The Transport layer is responsible for providing reliable end-to-end communication between applications.
- **Network layer:** The Network layer is responsible for routing packets between networks.
- **Data link layer:** The Data link layer is responsible for transmitting frames over a physical link.
- **Physical layer:** The Physical layer is responsible for transmitting bits over a physical medium.

![[five_layer_protocol_stack.png]]
- **Box 1:** This could be a router, which operates at the Network layer. Routers are responsible for routing packets between different networks.
- **Box 2:** This could be a switch, which operates at the Data link layer. Switches are responsible for forwarding frames between devices on the same network.
- **Box 3:** This could be a bridge, which also operates at the Data link layer. Bridges are used to connect two networks that use the same protocol.
- **Box 4:** This could be another router, or it could be a firewall, which operates at the Application layer. Firewalls are used to protect networks from unauthorized access.
- **Box 5:** This is the destination machine, which is running an HTTP server. The HTTP server operates at the Application layer.

- The HTTP request is sent from the Application layer of the source machine to the Application layer of the destination machine. 
- The Transport layer of the source machine breaks the HTTP request into segments and ensures that they are delivered to the destination machine in the correct order. 
- The Network layer of the source machine routes the segments to the destination machine. 
- The Data link layer of the source machine transmits the segments over the physical link. 
- The Physical layer of the source machine converts the digital bits of the segments into electrical signals that can be transmitted over the physical medium.

The intermediate devices in the network, such as routers and switches, also operate at different layers of the OSI model to provide different functions. For example, routers operate at the Network layer to route packets between different networks. Switches operate at the Data link layer to forward frames between devices on the same network.

The HTTP request will travel through all of these devices on its way to the destination machine. Each device will operate on the HTTP request at the appropriate layer of the OSI model.

Here is a more detailed explanation of each step in the process:

1. The user enters a URL into a web browser. The web browser is an application that operates at the Application layer.
2. The web browser sends an HTTP request to the server at the specified URL. The HTTP request is a message that asks the server to send a web page or other resource.
3. The HTTP request travels through the network, passing through routers, switches, and other devices. Each device operates on the HTTP request at the appropriate layer of the OSI model.
4. The HTTP request eventually reaches the server. The server is an application that operates at the Application layer.
5. The server receives the HTTP request and processes it. The server may retrieve the requested web page or other resource from its local storage, or it may generate a new web page on the fly.
6. The server sends an HTTP response back to the user's web browser. The HTTP response is a message that contains the requested web page or other resource.
7. The HTTP response travels through the network, passing through routers, switches, and other devices. Each device operates on the HTTP response at the appropriate layer of the OSI model.
8. The HTTP response eventually reaches the user's web browser.
9. The web browser receives the HTTP response and displays the web page or other resource to the user.

|Box|OSI Layer|
|---|---|
|1|Network|
|2|Data link|
|3|Data link|
|4|Network|
|5|Data link|
|6|Application|
|7|Transport|
|8|Network|
|9|Data link|
|10|Physical|
|11|Network|
|12|Data link|
|13|Physical|
|14|Network|
|15|Data link|