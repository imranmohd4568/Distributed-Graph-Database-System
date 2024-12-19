# Distributed-Graph-Database-System
This project involves the development of a comprehensive Distributed Graph Database System that incorporates multi-threading, inter-process communication (IPC), and load balancing. The system is built using POSIX-compliant C programs and operates with multiple client and server processes. The key components of the system include a client process, a load balancer, a primary server, two secondary servers, and a cleanup process. The system enables read and write operations on graph files stored as adjacency matrices and supports graph traversal via Breadth-First Search (BFS) and Depth-First Search (DFS).

## Development Highlights
### Developed a Load Balancer for Request Distribution

Implemented a single message queue for communication between clients, servers, and the load balancer.
Ensured efficient request routing by forwarding write requests to the primary server and distributing read requests to two secondary servers using an alternating logic (odd to server 1, even to server 2).
Incorporated concurrent request handling to ensure non-blocking communication with multiple clients.

### Developed Multi-threaded Server Processes for Concurrent Task Handling

Primary Server: Handles write requests by creating threads to process requests concurrently. Each thread reads input from shared memory, modifies graph files, and writes results back to the client.
Secondary Servers: Handle read requests and execute DFS and BFS traversals on graph files using multi-threaded traversal logic. For BFS, levels are processed sequentially but nodes at the same level are processed concurrently. For DFS, each unique path is processed using individual threads.

### Developed a Client Process for Graph Operations

Provided a menu-based client interface to allow users to add new graphs, modify existing graphs, and perform BFS or DFS traversals.
The client sends requests to the load balancer using a 3-tuple request format and creates shared memory segments for inter-process communication.
Incorporated a feedback mechanism where clients receive responses like "File successfully added" or "File successfully modified" after successful request completion.

### Implemented Synchronization and Concurrency Control

Used mutex locks and semaphores to manage concurrency during shared memory access and file updates.
Ensured proper synchronization to avoid race conditions during concurrent write operations and multi-threaded traversal in BFS and DFS.
Ensured parent-child thread synchronization by making parent threads wait for child threads to terminate.

### Developed a Cleanup Process for Graceful Termination

Designed a cleanup process that allows controlled shutdown of the system. Upon receiving the termination request from the user, the cleanup process informs the load balancer, which then informs all the servers to terminate gracefully after all pending client requests are serviced.
Ensured the proper deletion of shared memory segments, message queues, and termination of all processes without data loss or unfinished operations.
This project demonstrates expertise in distributed systems, multi-threaded programming, IPC (message queues and shared memory), and concurrency control mechanisms.
