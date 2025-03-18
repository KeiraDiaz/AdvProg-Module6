# Module 6 - Concurrency

## Contents
1. **Reflections**
    - [Milestone 1](#reflection-1)
    - [Milestone 2](#reflection-2)
    - [Milestone 3](#reflection-3)
    - [Milestone 4](#reflection-4)
    - [Milestone 5](#reflection-5)


## Reflection 1: 
### Single-Threaded Web Server

In building a single-threaded web server, two main protocols are involved: **Hypertext Transfer Protocol (HTTP)** and **Transmission Control Protocol (TCP)**. These protocols operate on a **request-response** principle, meaning the server receives a request from the client and responds accordingly.  

**TCP** is a low-level protocol that defines how data is transferred between servers but does not specify the content of the data. On the other hand, **HTTP** is responsible for structuring the request and response content. HTTP data is transmitted over TCP.  

Initially, the program can only handle browser requests by using `TcpListener` to listen for connections on `127.0.0.1:7878`. Every time a connection is received, the program prints `"Connection established!"`.  

### Key Concepts:
- **`bind()`**: Associates a `TcpListener` with a specific address and port on the local machine, allowing it to listen for incoming connections.  
- **`unwrap()`**: Extracts the value from a `Result` or `Option`. If the result is `Ok` or `Some`, it returns the contained value. However, if the result is `Err` or `None`, calling `unwrap()` will cause the program to panic and terminate, indicating a critical error.  
- **`incoming()`**: Retrieves incoming connections on `TcpListener`, returning an iterator that yields `Result<TcpStream, Error>`. Each element represents a stream, which is an open connection between the client and server. The server processes these connections sequentially, handling one at a time.  

To define how the server should respond to browser requests, a function called **`handle_connection()`** is implemented. This function processes the incoming HTTP request, and at the end, the console displays the HTTP request message.  

Additionally, a **`BufReader`** is used to read lines from the `TcpStream` using the `lines()` method. The `http_request` variable collects the lines of the HTTP request received from the browser.