---
title: "Server-Client Character Occurrence Counter"
date: 2023-02-13T11:00:00+03:00
draft: false
toc: true
images:
  - "https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Servermeme.png"
tags:
  - Java
  - Networking
  - TCP/IP
  - Server-Client
  - Character Counting
---

<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Servermeme.png" width=3000 height=500>

## Introduction

This project implements a server-client program in Java that counts the occurrences of a specific character in a given string. The client sends a character and a string to the server, which then processes the request and returns the number of occurrences. This program utilizes TCP as the transport protocol, ensuring reliable and secure communication between the server and client.

## Project Structure

The project consists of two main components:

1. Server (Server.java)
2. Client (Client.java)

### Server Class

The server is responsible for hosting the application and handling client requests. Key methods include:

1. `Projector_Master_server(int port)`: Initializes the server and manages the main flow.
2. `initiate_Server()`: Creates a ServerSocket object and starts listening for connections.
3. `Client_listener()`: Waits for and accepts client connections.
4. `Clinet_Reader()`: Reads and processes client input.

Here's a snippet of the `Projector_Master_server` method:

```java
public Projector_Master_server(int port) {
    try {
        this.port = port;
        initiate_Server();
        Client_listener();
        Clinet_Reader();
        System.out.println("Closing connection");
        closeConnections();
    } catch (BindException error) {
        System.err.println("A server is already running on the same port!");
        System.exit(2);
    } catch (SocketException error) {
        System.err.println("The client has disconnected");
        System.exit(0);
    } catch (IOException error) {
        System.err.println(error);
        System.err.println("Something went wrong with IO");
        System.exit(1);
    }
}
```

### Client Class

The client connects to the server, sends requests, and displays the results. Key methods include:

1. `Projector_Master_client(String ipAddress, int port)`: Initializes the client and manages the main flow.
2. `establishConnection()`: Connects to the server using the provided IP address and port.
3. `UserInput()`: Reads user input and sends it to the server.
4. `endConnection()`: Closes the connection with the server.

## String Occurrence Algorithm

The server uses a simple algorithm to count character occurrences:

```java
private int findNumberOfOccurrences(String text, char matching_char) {
    int char_numper = 0;
    for (int i = 0; i < text.length(); i++) {
        if (Character.toString(text.charAt(i)).equalsIgnoreCase(Character.toString(matching_char))) {
            char_numper++;
        }
    }
    return char_numper;
}
```

This method iterates through the input string, comparing each character (case-insensitive) with the target character and incrementing a counter for each match.

## Sample Output

### Server Output
<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Serverout.jpg" alt="Server Output" width="600">

### Client Output
<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/Clientout.jpg" alt="Client Output" width="600">

## Conclusion

This server-client program demonstrates effective use of Java networking capabilities to create a practical character counting tool. Key features include:

- Reliable communication using TCP/IP protocol
- Efficient character occurrence counting
- Proper error handling and connection management
- User-friendly interface for input and output

The program's architecture allows for easy expansion and modification, making it a solid foundation for more complex networking applications.