![lab](/resources/pclogo.png)
## <div align="center">Lab 01</div>

## Objectives:  
* Using a AWS EC2 Linux Instance
* Accessing AWS EC2 Linux instance through ssh
* Installing OpenMP library
* Compiling a simple OpenMP program

## Exercise 0:

1. Create a GitHub repo with your student id.  If you already have one you can use it.
2. Login to your GitHub account
3. Run the following link to close Lab01 to your Github account https://classroom.github.com/a/G-2YsTYL
4. You have to do the exercises given in the repository and commit and push your solutions into it.

## Exercise 1:
Use the provided AWS Cloud Foundation course provided and complete the Lab 03 - Introduction to EC2 Lab in Module 06

![lab2](/resources/ec2lab.png)

1. Provide Screen shots of you completing the lab (Have at least 10 screen shots at different stages of your Lab)

## Exercise 2:


Complete the following program in the same Lab Instance

```c
#include <stdio.h>
#include <unistd.h>

int main() {
  char hostname[100];
  int ncpus;

  gethostname(hostname,100);
  ncpus = sysconf(_SC_NPROCESSORS_ONLN);
  printf("Hello World, I am running on host %s with %d logical cpus\n", hostname, ncpus);
  return 0;
}
```

6.	Compile the above program using the gcc C compiler - gcc (```gcc exercise01 -otest.o```)
7.	Run the above program in the AWS Linux Instance
8.	How many logical cores are there?
9.  Answer these questions in a text file called exercise02.txt
10. Commit and push the code to your repo.

```
git add .
git commit -m "<put a message here>"
git push
```
This is how you should commit your code back to your repo.  Please remember to this at the end of your lab session.  You can go back and continue to work on your solution within the given deadline.  If you are going to use a different folder to work on your program you can always get your code from your repo using the ```git clone``` command that you used earlier

## Exercise 3:


Complete the following program in the same Lab Instance, you will have to install openmp in your linux enviroment.

```c
#include <stdio.h>
#include <omp.h>

int main() {
    // Start of parallel region
    #pragma omp parallel
    {
        int thread_id = omp_get_thread_num();     // Get the current thread ID
        int total_threads = omp_get_num_threads(); // Get total number of threads

        printf("Hello from thread %d out of %d threads!\n", thread_id, total_threads);
    }

    return 0;
}
```
To compile your program
```
gcc -fopenmp hello.c -o hello
./hello
```

Commit the code and add the output to a file output.txt 

## Exercise 4:

Complete the self assessment quiz for Module 6

Attach a screen shot of your completed self assessment for Module 6 and commit it

