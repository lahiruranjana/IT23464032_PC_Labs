![lab](/resources/pclogo.png)
## <div align="center">Lab 07</div>

## Objectives:  
* Write basic CUDA Code


## Exercise – 1 – Simple Calculation program from the Lecture

```
#include <cstdio>

// this kernal code runs on the device (nvidia co processor)
__global__ void add(int *a, int *b, int *c) {
		*c = *a + *b;
	}

// host - cpu
// device - gpu

	int main(void) {
		int a, b, c;	            // host copies of a, b, c
		int *d_a, *d_b, *d_c;	     // device copies of a, b, c
		int size = sizeof(int);

		// Allocate space for device copies of a, b, c
		cudaMalloc((void **)&d_a, size);
		cudaMalloc((void **)&d_b, size);
		cudaMalloc((void **)&d_c, size);

		// Setup input values
		a = 2;
		b = 7;

// 1. copy values from host to device
		// Copy inputs to device
		cudaMemcpy(d_a, &a, size, cudaMemcpyHostToDevice);
		cudaMemcpy(d_b, &b, size, cudaMemcpyHostToDevice);
// 2. launch the kernal

		// Launch add() kernel on GPU
		add<<<1,1>>>(d_a, d_b, d_c);

// 3. copy values from device to host

		// Copy result back to host
		cudaMemcpy(&c, d_c, size, cudaMemcpyDeviceToHost);

		printf("Result is %d\n", c);

		// Cleanup
		cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
		return 0;
	}
```


 

## Exercise – 2 – Calculation of the addition of two vectors - program from the Lecture using 512 Blocks and one Thread

```
#include <cstdio>
#include <cstdlib>

#define N 512

__global__ void add(int *a, int *b, int *c) {
		c[blockIdx.x] = a[blockIdx.x] + b[blockIdx.x];
   // each block will run only one addition
}

void random_ints(int* x, int size)
{
	int i;
	for (i=0;i<size;i++) {
		x[i]=rand()%100;
	}
}

int main(void) {
	int *a, *b, *c;		// host copies of a, b, c
	int *d_a, *d_b, *d_c;	// device copies of a, b, c
	int size = N * sizeof(int);

	// Alloc space for device copies of a, b, c
	cudaMalloc((void **)&d_a, size);
	cudaMalloc((void **)&d_b, size);
	cudaMalloc((void **)&d_c, size);

	// Alloc space for host copies of a, b, c and setup input values
	a = (int *)malloc(size); random_ints(a, N);
	b = (int *)malloc(size); random_ints(b, N);
	c = (int *)malloc(size);
        // Copy inputs to device
        cudaMemcpy(d_a, a, size, cudaMemcpyHostToDevice);
        cudaMemcpy(d_b, b, size, cudaMemcpyHostToDevice);

        // Launch add() kernel on GPU with N blocks
        add<<<N,1>>>(d_a, d_b, d_c);

        // Copy result back to host
        cudaMemcpy(c, d_c, size, cudaMemcpyDeviceToHost);

	for (int r=0; r<N; r++)
		printf("%d + %d = %d\n", a[r],b[r],c[r]);

        // Cleanup
        free(a); free(b); free(c);
        cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
        return 0;
    }
```

Exercise 3

## Exercise – 3 – Calculation of the addition of two vectors - program from the Lecture using one Blocks and 512 Threads

```
#include <cstdio>
#include <cstdlib>

#define N 512

__global__ void addT(int *a, int *b, int *c) {
    c[threadIdx.x] = a[threadIdx.x] + b[threadIdx.x];
}

void random_ints(int *x, int size) {
    for (int i = 0; i < size; i++) {
        x[i] = rand() % 100;
    }
}

int main(void) {
    int *a, *b, *c;          // host copies of a, b, c
    int *d_a, *d_b, *d_c;    // device copies of a, b, c
    int size = N * sizeof(int);

    // Allocate space for device copies of a, b, c
    cudaMalloc((void **)&d_a, size);
    cudaMalloc((void **)&d_b, size);
    cudaMalloc((void **)&d_c, size);

    // Allocate space for host copies of a, b, c and setup input values
    a = (int *)malloc(size);
    random_ints(a, N);
    b = (int *)malloc(size);
    random_ints(b, N);
    c = (int *)malloc(size);

    // Copy inputs to device
    cudaMemcpy(d_a, a, size, cudaMemcpyHostToDevice);
    cudaMemcpy(d_b, b, size, cudaMemcpyHostToDevice);

    // Launch add() kernel on GPU with N threads
    addT<<<1, N>>>(d_a, d_b, d_c);

    // Copy result back to host
    cudaMemcpy(c, d_c, size, cudaMemcpyDeviceToHost);

    // Display results
    for (int r = 0; r < N; r++)
        printf("%d) %d + %d = %d\n", r, a[r], b[r], c[r]);

    // Cleanup
    free(a);
    free(b);
    free(c);
    cudaFree(d_a);
    cudaFree(d_b);
    cudaFree(d_c);

    return 0;
}
```

## Exercise 4

Write a Cuda program to multiple two vectors. Use an arrangement as used in Exercise 4 for
generating random values for two arrays A, B.
a) Use array size as 10,000,000 for the data
b) For calculating C, use 512 threads per block. Have sufficient number of blocks to handle the
calculation of 10,000,000 elements. In essence we are trying to use both blocks and threads
together for the calculation.
In Cuda as you must have gathered by now we typically do not use a loop in the kernel (device)
code.
c) Print the last 1000 results that you get from the kernel

## Exercise 5

Extend the Exercise 5 and use a 2 dimensional matrix 10,000x 10,000 for A, B and C. For the
calculation simply multiply the adjacent element. e.g.

```C[4][3] = A[4][3] x B[4][3]```

Print the last thousand elements ```C[9,999][9,000] to C[9,999][9,999]```
