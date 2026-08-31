#include <stdio.h>
#include <unistd.h>  // For sleep()

// Interrupt Service Routine
void ISR()
{
    printf("\n*** Interrupt Received ***\n");
    printf("Executing Interrupt Service Routine...\n");
    printf("I/O Operation Completed.\n");
    printf("Returning to Main Program...\n");
}

int main()
{
    int i;

    printf("Interrupt-Driven I/O Simulation\n\n");

    for(i = 1; i <= 10; i++)
    {
        printf("CPU executing task %d\n", i);

        sleep(1);

        // Simulate interrupt occurrence
        if(i == 5)
        {
            ISR();
        }
    }

    printf("All CPU tasks completed.\n");

    return 0;
}