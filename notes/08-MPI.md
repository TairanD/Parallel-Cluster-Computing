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





