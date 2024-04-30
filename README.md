# Modul 9 Reflection
**Salma Kurnia Dewi (2206026681)**

## 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
- Unary RPC: This is the simplest method, where the client sends a single request to the server and waits to receive a single response from the server. 
Unary RPC is typically used in simple request-response scenarios where no additional interaction with the request data is needed, such as retrieving specific data from the server or in authentication/authorization systems, form submissions.
- Server Streaming RPC: In this method, the client sends a single request and the server responds with a stream of data. 
The server sends data repeatedly through the same connection so that the sent data is pieces of data that form larger data. 
This method is typically used when the client needs the server to send a large amount of data, such as retrieving a large volume of data from a database or sending stock prices, news, or large datasets in pieces.
- Bi-Directional Streaming RPC: This method allows both parties, both the client and the server, to send a series of messages independently using a read-write stream in the same or opposite direction simultaneously. 
This is suitable for use when the client and server need to interact to send and receive data in real-time, such as chat services or in applications like collaborative editing or real-time games.

## 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
- Authentication: gRPC supports several authentication methods, such as SSL/TLS, OAuth2, token-based authentication, or as simple as username and password. 
When implementing a gRPC service in Rust, we need to verify the identity of the user or service. This can be achieved by using tokens like JWT or through integration with an OAuth2 system.
- Authorization: After the authentication process, appropriate permissions are required. gRPC supports several authorization methods, such as Role-Based Access Control (RBAC) and Attribute-Based Access Control (ABAC). 
Authorization management is also needed to regulate access to resources based on established roles or rules, and can be implemented through middleware.
- Data Encryption: Data transferred over the network needs to be encrypted to protect against tampering and eavesdropping. 
To secure a gRPC service, we can use SSL/TLS to encrypt the data transferred. In addition, each piece of data sent by both the server and the client needs to be separately encrypted to ensure the privacy of the data sent.

Unlike REST, gRPC enforces authentication/authorization/encryption multiple times for a single stream request, whereas for REST, a single request only needs validation once because the connection is closed after the response. 

## 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
      - Concurrency: Clients may send and receive many messages simultaneously, so concurrency must be considered when implementing bidirectional streaming in Rust gRPC. 
      Many clients can send and receive messages at the same time, so it’s necessary to manage responses from different clients accurately.
      - Error Handling: Rust has a strict error handling system, so error handling must be considered when implementing bidirectional streaming in Rust gRPC.
      - Message Ordering: There may be obstacles that occur during the process, so it’s necessary to ensure the order of messages remains consistent when implementing bidirectional streaming in Rust gRPC.
      - Connection Management: Handling unexpected connection termination and quickly restoring the connection is crucial because clients can connect and disconnect at any time.
      - Race Conditions and Data Synchronization: When creating a system with bidirectional streaming and gRPC, it can be challenging to ensure that race conditions do not occur and data synchronization is maintained.
      - Long-Lived Connections: Long-lived connections can complicate load balancing because many long-lived connections can form where the connection cannot be terminated due to gRPC, potentially burdening the server.

## 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Advantages:
1. ***Convenience***: `ReceiverStream` simplifies stream handling by providing a wrapper for `tokio::sync::mpsc::Receiver`, making it easier to work with asynchronous streams.
2. ***Compatibility***: `ReceiverStream` is compatible with `tonic::Streaming`, so it can be used to send stream responses in Rust gRPC services.
3. ***Integration***: `Tokio-Stream` is integrated with the Tokio ecosystem, which allows for working with streams asynchronously.
4. ***Transformation***: `ReceiverStream` can transform a tokio receiver into a stream that can be processed by tonic.
5. ***Asynchronous***: It accelerates data processing.

Disadvantages:
1. ***Error Handling***: `ReceiverStream` does not provide built-in error handling, so error handling must be implemented manually when using `ReceiverStream`. If an error occurs when receiving a message, `ReceiverStream` does not have a built-in mechanism that can help handle it.
2. ***Support***: `ReceiverStream` only supports one-way connections, so it is not suitable for bidirectional streaming in Rust gRPC services.
3. ***Complexity***: Due to asynchronous programming, it can be complex to implement.
4. ***Authentication and Authorization***: For each piece of data, authentication and authorization need to be performed, which can add to the complexity.

## 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
- Separate Definition Files: Define services and messages in separate .proto files so that message definitions can be reused by other services. This allows for better organization and reusability of code.
- Reusable Functions and Structs: Determine reusable functions and structs in different .rs files so they can be used by other services. This promotes code reuse and makes the codebase more manageable.
- Separate Implementation Files: Arrange the implementation of services and messages in different .rs files to facilitate maintenance and extensibility. This allows for the addition, modification, or deletion of functionalities without affecting other parts of your system.
- Separate Modules: Create separate modules between the Rust gRPC code and business logic. This enhances the modularity of the code and separates concerns, making the code easier to understand and maintain.
- External Libraries: Use external libraries for common functionalities that can be reused. This reduces the amount of code you need to write and maintain, and can also improve the performance of your application.
- Traits and Generics: Use traits and generics for flexible components to increase maintainability and extensibility. This allows you to write code that is more abstract and flexible, and can be reused in different contexts.
- Interface Implementation: Rust gRPC provides a way to improve maintainability and extensibility because changes and additions to features can be made more easily. With proto, an interface is created that can be implemented by a class in Rust, facilitating code extensibility.

## 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

## 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

## 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

## 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

## 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
