# Message Passing Interface (MPI)

## 1 - MPI
MPI is a library that we can use in C, which provides the necessary functions and constants to allow us to convert serial
code to parallel. Primarily, it enables us to have processes communicate with each other much more easily.

MPI defines the standards of how message passing can be achieved in parallel programming:
1. The protocol for sending messages
2. the syntax of the function calls
3. some data types that can be used when sending information


## 2 - Using MPI
### 2.1 - Include the required header file
Include the “mpi.h" library file: `#include<mpi.h>`, which is only available when an MPI implementation has been installed
on the system.

### 2.2 - Initialize the MPI environment
MPI is initialized with a single function call to a function named **MPI_Init**. It requires two parameters:
```
MPI_Init( int* argc, char*** argv)
```
Two common approaches to set up is:
1. Pass pointers to the parameters of the main function.
2. Pass the value NULL for both parameters.

### 2.3 - Find out about the processes
Parallel programming involves multiple processors to calculate different pieces of data. MPI requires two types of information
under this condition:
1. How many processes are running this program?
2. Which number process am I (the user)?

Each can be found out using a function call.

#### 2.3.1 - How many processes?
Function **MPI_Comm_size** is used to get this information, which requires two parameters:
``` 
MPI_Comm_size( MPI_Comm communicator, int* size)
```
where the first one is a constant supplied by the MPI library MPI_COMM_WORLD, and the second one is a pointer to an 
int variable created by us. The answer will be put into this variable.

#### 2.3.2 - Which number am I?
When we know how many processes there are, we will know their numbers:
- If there are n processes, then they will be numbered 0 to _n-1_.
We need to know which process we are, so we will know that task to perform. Function MPI_Comm_rank can do this for us:
``` 
MPI_Comm_rank( MPI_Comm communicator, int* rank)
```
The two parameters are very similar to the previous function.

### 2.4 - Communicate
Communication between processes is crucial. Yet, we will elaborate this later.


### 2.5 - Clean up the MPI environment
The last step in an MPI program should be to clean up the environment. We use the MPI_Finalize function for this.

### 2.6 Example (No Communication)
```
#include<mpi.h>
#include<stdio.h>

int main(int argc, char **argv){
    int procCount;
    int procRank;
    
    MPI_Init(&argc, &argv);
    
    MPI_Comm_size(MPI_COMM_WORLD, &procCount);
    MPI_Comm_rank(MPI_COMM_WORLD, &procRank);
    
    printf("Hello, I am process %d out of %d\n", procNum, procCount);
    
    MPI_Finalize();
    return 0;
}
```


## 3 - Working with MPI
When working with C, we usually use the gcc compiler. 
Additionally, the executable programs can be directly executed in a terminal.

With MPI, we must use different command to compile, and to execute.

### 3.1 - Compiling MPI Programs
Instead of `gcc`, we use `mpicc`. For example, we use `mpicc example.c -o example` to create an executable named `example`.

### 3.2 - Executing MPI Programs
When we execute an MPI program, we need to tell the system how many processors/cores to use.
Command `mpirun` can do this for us, which requires some arguments on the command line:
- the number of program copies (-n X) where X is how many copies to execute.
- the name of compiled program to be executed.

E.g. `mpirun -n 2 example`

## 4 - MPI Communication (Point to Point)
The easiest method of communication between processes is point to point:
- one process calls a function to send data
- the other process calls a function to receive data.
The function calls must be paired. These function calls are **blocking**.

### 4.1 Send Data
We use `MPI_Send` function to send data:
```
MPI_Send(void* data, int count, MPI_Datatype datatype, int destination,
int tag, MPI_Comm communicator)
```
where:
- `data` is a pointer to the information that we want to send
- `count` is how many pieces of information we want to send
- `datatype` is the type of the data
- `destination` is the number of the process to send to
- `tag` can be used to describe different types of messages
- The final argument will be the constant `MPI_COMM_WORLD`

For example, the following code will send a single int value to the process numbered 0:
``` 
int someNumber = result_of_calculation();
MPI_Send( &someNumber, 1, MPI_INT, 0, MPI_ANY_TAG, MPI_COMM_WORLD );
```

### 4.2 Receiving Data
To receive data, we use the MPI_Recv function:
``` 
MPI_Recv( void* data, int count, MPI_Datatype datatype, int destination,
int tag, MPI_Comm communicator, MPI_Status* status)
```
where:
- `data` is a pointer to the information that we want to receive
- `count` is how many pieces of information we want to receive
- `datatype` is the type of the data
- `destination` is the number of the process to receive from. The penultimate argument will be the constant `MPI_COMM_WORLD`.
- `tag` can be used to describe different types of messages. For the final argument we will use the constant `MPI_STATUS_IGNORE`.

``` 
int data[3];
MPI_Recv( data, 3, MPI_INT, 1, MPI_ANY_TAG, MPI_COMM_WORLD, MPI_STATUS_IGNORE );
```
This function will receive all three int values from the process numbered 1.

### 4.3 Who Does What Task?

When using MPI, we are writing a single program that can be executed as multiple processes.
But if the code for the program is the same, then how do we have them do different work?
We must decide and include logic to allow the program to choose.
This is often based on **the number of the process**.

For example:
``` 
int main(int argc, char **argv){
    int procRank, procSize;
    
    MPI_Init(&argc, &argv);
    MPI_Comm_size(MPI_COMM_WORLD, &procSize);
    MPI_Comm_rank(MPI_COMM_WORLD, &procRank);
    
    srand( time(NULL) + procRank );
    int r = rand() % 1000;
    printf("Process %d generated the number %d\n", procRank, r);
    int temp;
    if (procRank == 1){
        MPI_Send(&r, 1, MPI_INT, 0, 0, MPI_COMM_WORLD);
        printf("Process %d is sending the number %d to 0\n", procRank, r);
    } else {
        MPI_Recv(&temp, 1, MPI_INT, 1, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
        printf("Received %d from process 1\n", temp);
        r = r + temp;
        printf("The sum of the numbers was %d\n", r);
    }
    MPI_Finalize();
    return 0;
}
```












