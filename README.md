# thread1
thread program
2.	Write a multithreaded program that calculates various statistical values for a list of numbers. This program will be passed a series of numbers on the command line and will then create three separate worker threads. One thread will determine the average of the numbers, the second will determine the maximum value, and the third will determine the minimum value. For example, suppose your program is passed the integers 
90 81 78 95 79 72 85
The program will report
The average value is 82
The minimum value is 72
The maximum value is 95 
The variables representing the average, minimum, and maximum values will be stored globally. The worker threads will set these values, and the parent thread will output the values once the workers have exited. 


#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
 
void *avg(void *str);
void *min(void *ptr);
void *max(void *ptr);

double avg;        
int min;
int max;

typedef struct datastruct
{
    int size;
    int * values;
}datastruct;

main(int argc, char *argv[])
{
	printf("\n\nWelcome to paheeThredz, by Sean Staz\n\n");
    while(argc <=1)
    {
        printf("Incorrect input. No arguments entered.\n");
        printf("Please enter one or more inputs.\n");
        exit(0);
	}
    
    int i = 0;
    int copy[argc-1];
    for(i; i < (argc -1); i++)
    {
        copy[i] = atoi(argv[i+1]);
    }
        
    pthread_t thread1, thread2, thread3;
    const char *message1 = "This is Thread 1";
    const char *message2 = "This is Thread 2";
    const char *message3 = "This is Thread 3";
    int  t1, t2, t3;
 
    printf("Running: %s\n\n", argv[0]);
    
    datastruct ds = {argc - 1, copy};
 
   
    t1 = pthread_create(&thread1, NULL, (void *) avg, (void *) &ds);
    if(t1)
    {
        fprintf(stderr,"Error - pthread_create() return code: %d\n", t1);
        exit(EXIT_FAILURE);
    }
   
   
