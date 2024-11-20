# Hello

This project demonstrates a simple HTTP server implemented in Rust. It features a multi-threaded request handling mechanism using a custom thread pool implementation. The server can handle basic GET requests and simulate delayed responses to illustrate thread management.

## Features

- **Custom Thread Pool**: Efficiently manages a fixed number of threads to process incoming connections.
- **HTTP Request Handling**:
  - Serves static HTML files.
  - Simulates delays for specific routes.
  - Responds with `404 Not Found` for unsupported routes.
- **Graceful Shutdown**: Ensures all threads are properly terminated when the server exits.
# Getting Started

### Prerequisites

Ensure you have the following installed:
- [Rust](https://www.rust-lang.org/): Rust programming language and Cargo package manager.

### Clone the Repository

```bash
git clone https://github.com/your-username/hello.git
cd hello
```

### Build and Run the Server

1. **Build the project**:
   ```bash
   cargo build --release
   ```

2. **Run the server**:
   ```bash
   cargo run
   ```

3. The server will start listening on `127.0.0.1:7878`.
## Project Structure

### Main Components

- **`main.rs`**:
  - Sets up the server to listen on a specified address.
  - Initializes the custom thread pool.
  - Handles incoming HTTP requests.

- **`lib.rs`**:
  - Implements a thread pool for managing worker threads.
  - Defines the behavior of workers and their lifecycle.

### HTML Files

The server expects the following HTML files in the project root:
- `hello.html`: Served for the `/` and `/sleep` routes.
- `404.html`: Served for unsupported routes.
## Routes

| Route       | Description                                               |
|-------------|-----------------------------------------------------------|
| `/`         | Returns the contents of `hello.html`.                     |
| `/sleep`    | Simulates a 5-second delay, then returns `hello.html`.     |
| Any other   | Returns a `404 Not Found` response with `404.html`.        |
## Thread Pool Implementation

The thread pool is designed to efficiently manage resources:
- A **channel** is used to send jobs to worker threads.
- **Workers** wait for jobs and execute them as they arrive.
- When the thread pool is dropped, it ensures that all workers shut down gracefully.
## Example Output

When a request is handled:
```text
Worker 0 got a job; executing.
Worker 1 got a job; executing.
Worker 2 disconnected; shutting down.
```
## License

This project is licensed under the [CC-BY 4.0 License](https://github.com/SonikSeven/hello/blob/main/LICENSE.txt).
