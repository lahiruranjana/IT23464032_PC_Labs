
![lab](/resources/pclogo.png)
## <div align="center">Lab 06</div>


## Objectives:  
* Write Recursive OpenMP programs
* Write MPI programs


## Exercise 0:

Please complete the in class activities we did in the MPI lecture given at https://github.com/SLIIT-FacultyOfComputing/SE4060-MPI-Part1 

## Exercise 1:
* Create a GitHub repo with your student id. If you already have one you can use it.
* Login to your GitHub account
* You have to do the exercises given in the repository and commit and push your solutions into it.

## Exercise 2:

Parallelize the following serial code for fibonacci series using task parallelization
```c
 int fib(int n) {
  int i, j;
  if (n<2)
    return n;
  else {
    i=fib(n-1);
    j=fib(n-2);
    return i+j;
  }
}
```
## Exercise 3:

Parallelize adding up numbers 1 to 10,000,000 using multiple nodes using MPI

## Exercise 4:

Parallelize the computation of Pi using the “Monte Carlo method” (See Lab03) using MPI



Find the calculation for 10,000,000 times.

## Exercise 5:

For both Exercise 1 and Exercise 2

1. Plot a graph that shows Time vs Number of Processors (You can keep the nodes to 2 and increase the number of processors to the number of total cores that are available)
2. Plot a graph that shows Speedup

## Exercise 6:

1. Write a simple program where the source and the destination doesn’t match.  You can take either message1.cc or message2.cc and modify the program.  What happens in this situation?
2. Rewrite message2.cc using Buffered Send (BSend) ensure that you do not replace the variables that you are using to send the data.

## Exercise 7:

Rewrite Exercise 3 by changing the receiving Tag to MPI_ANY_SOURCE, redo Exercise 3 and compare with the original results.

## Exercise 8:

Rewrite Exercise 6 by using Buffered Send (BSend).





