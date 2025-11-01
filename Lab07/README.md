![lab](/resources/pclogo.png)
## <div align="center">Lab 07</div>

## Objectives:  
* Write advanced MPI programs 
* Use Broadcast, Scatter, Gather, Reduce and AllReduce


## Exercise 1

Take Exercise 3 from Lab 6,

Parallelize adding up numbers 1 to 10,000,000 using multiple nodes using MPI.

(a) Use MPI_ANY_TAG and MPI_ANY_SOURCE for your solution.
(b) Use Buffered Send MPI_Bsend() instead of MPI_Ssend()

## Exercise 2

Write a code to read an ascii file of 10,000 numbers in csv format and broadcast it to all the nodes to calculate the sum of these numbers.

1.	Use a random function in Excel to create a file of 10,000 random numbers
2.	Store the data as a csv file
3.	In rank = 0 read the csv file and load it to an array of 10,000 elements
4. 	broadcast the data to all nodes
5.	Get each code to add a subset of the numbers and return the total to the root node.
6. 	Display the total 

## Exercise 3

Use scatter to send the data to the worker nodes instead of broadcasting the data.  Get the results using the same approach.

## Exercise 4

Modify Exercise 3 by using the gather command to retrieve all the partial totals and calculate the partial totals to get the final totals.

## Exercise 5

Modify Exercise 4 by using the reduce command to calculate the final total.

## Exercise 6

Modify Exercise 5 by using the Allreduce command to calculate the final total, show that now the total is accessible by all nodes


## Exercise 7

Write a program to send 100 messages between two nodes, each time a random number needs to added to be appended to the array that is sent. (ping pong type of problem)

## Exercise 8

Write a program to pass a value in a ring like fashion, each node should add the rank to the array that is being passed.

It should stop when it goes past all nodes exactly two times.  The final result should be displayed.



