# COMP3036J Parallel and Cluster Computing: MPI Dockerised Implementations
## Author: Nima Afraz


In this lab, you will learn how to use MPI (Message Passing Interface) to perform parallel computation across multiple Docker containers. You will compile and run an MPI C program that calculates the sum of an array distributed across multiple processes.

## Prerequisites
- Docker installed on your machine

## Setup

### Step 1: Create the MPI Program

Save the following code as `array_sum.c`. This program will calculate the sum of an array using MPI.

```c
#include <mpi.h>
#include <stdio.h>
#include <stdlib.h>

int compute_sum(int *array, int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += array[i];
    }
    return sum;
}

int main(int argc, char** argv) {
    MPI_Init(&argc, &argv);
    int world_size, world_rank;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    int n = 100; // Total number of elements
    int local_n = n / world_size; // Elements per process
    int *local_array = malloc(sizeof(int) * local_n);

    for (int i = 0; i < local_n; i++) {
        local_array[i] = i + world_rank * local_n + 1;
    }

    int local_sum = compute_sum(local_array, local_n);
    printf("Local sum for process %d is %d\n", world_rank, local_sum);

    int total_sum = 0;
    MPI_Reduce(&local_sum, &total_sum, 1, MPI_INT, MPI_SUM, 0, MPI_COMM_WORLD);

    if (world_rank == 0) {
        printf("Total sum = %d\n", total_sum);
    }

    free(local_array);
    MPI_Finalize();
    return 0;
}
```

### Step 2: Dockerfile

Create a Dockerfile with the following content to set up the environment.

```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y mpich
WORKDIR /app
COPY . /app
RUN mpicc -o array_sum array_sum.c
CMD ["mpiexec", "-n", "4", "./array_sum"]
```

### Step 3: Build and Run

Build the Docker image using the following command:

```bash
docker build -t mpi-array-sum .
```

### Step 4: Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: '3.8'
services:
  mpi-master:
    image: mpi-array-sum
    depends_on:
      - mpi-worker1
      - mpi-worker2
      - mpi-worker3
    environment:
      - "OMPI_MCA_btl_vader_single_copy_mechanism=none"
  mpi-worker1:
    image: mpi-array-sum
    environment:
      - "OMPI_MCA_btl_vader_single_copy_mechanism=none"
  mpi-worker2:
    image: mpi-array-sum
    environment:
      - "OMPI_MCA_btl_vader_single_copy_mechanism=none"
  mpi-worker3:
    image: mpi-array-sum
    environment:
      - "OMPI_MCA_btl_vader_single_copy_mechanism=none"
```

Run the containers with:

```bash
docker-compose up
```

## Modify the existing MPI setup to implement a parallel bucket sort algorithm.
Bucket sort was one of the sorting algorithms you studied in Data Structures and Algorithms in stage 2. In a parallel setting, bucket sort can be implemented by distributing data into buckets corresponding to different MPI ranks (processes), sorting each bucket locally, and then collecting the sorted data.

You should create a new C program (parallel_bucket_sort.c) to implement the bucket sort algorithm using MPI, where the number of buckets is the same as the number of MPI ranks (Docker Containers).