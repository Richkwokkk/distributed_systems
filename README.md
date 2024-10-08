# Java RMI Calculator Server

This project implements a simple calculator server using Java RMI (Remote Method Invocation). It consists of a server that maintains a stack for each client, allowing clients to perform basic arithmetic operations remotely.

## Project Structure

The project consists of four main Java files:

1. `src/main/java/RMI_Calculator/Calculator.java`: The remote interface that defines the operations supported by the calculator server.
2. `src/main/java/RMI_Calculator/CalculatorImplementation.java`: The implementation of the Calculator interface.
3. `src/main/java/RMI_Calculator/CalculatorServer.java`: The server class that sets up the RMI registry and binds the Calculator implementation.
4. `src/test/java/CalculatorClient.java`: A test client that demonstrates the functionality of the calculator server.

## Functionality

### Calculator.java
This interface defines the following remote methods:
- `pushValue(int val)`: Pushes an integer value onto the stack.
- `pushOperation(String operator)`: Performs an operation ("min", "max", "lcm", "gcd") on the values in the stack.
- `pop()`: Removes and returns the top value from the stack.
- `isEmpty()`: Checks if the stack is empty.
- `delayPop(int millis)`: Waits for the specified time before performing a pop operation.

### CalculatorImplementation.java
This class implements the Calculator interface. Key features include:
- Maintains a separate stack for each client using a ConcurrentHashMap.
- Implements all methods defined in the Calculator interface.
- Handles edge cases and throws appropriate exceptions.

### CalculatorServer.java
This class sets up the RMI server:
- Creates an instance of CalculatorImplementation.
- Sets up the RMI registry.
- Binds the Calculator implementation to the registry.

### CalculatorClient.java
This class serves as a test client:
- Connects to the RMI registry and looks up the Calculator remote object.
- Performs comprehensive tests for both single-client and multi-client scenarios.
- Tests all implemented methods: pushValue, pushOperation, pop, isEmpty, and delayPop.

## Bonus Marks

This implementation aims to achieve the bonus marks by implementing separate stacks for each client. In CalculatorImplementation.java, we use a ConcurrentHashMap to associate each client thread with its own stack. This ensures that:

1. Each client has its own independent stack.
2. Operations from one client do not interfere with the stacks of other clients.
3. The system can handle multiple clients concurrently without data races or inconsistencies.

The use of ConcurrentHashMap also provides thread-safety, making our implementation suitable for a multi-threaded environment.

## Running the Application

### Method 1: Manual Compilation and Execution

To run the application manually:

1. Compile all Java files.
2. Start the RMI registry if needed.
3. Run CalculatorServer.
4. Run CalculatorClient.

The client will perform a series of tests demonstrating the functionality of the calculator server in both single-client and multi-client scenarios.

### Method 2: Using Makefile

A Makefile is provided to simplify the compilation and execution process. To use the Makefile:

1. Ensure you have `make` installed on your system.
2. Open a terminal and navigate to the project root directory (where the Makefile is located).
3. Use the following commands:

   - To compile the project:
     ```
     make all
     ```

   - To run the server:
     ```
     make run-server
     ```

   - To run the client (in a separate terminal):
     ```
     make run-client
     ```

   - To clean the compiled files:
     ```
     make clean
     ```

Using the Makefile automates the compilation process and ensures that all files are compiled with the correct classpath and output directory settings.