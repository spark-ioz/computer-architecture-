# computer-architecture-
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 1000000

int main()
{
    int arr[SIZE];
    long long sum = 0;
    clock_t start, end;
    double cache_time, nocache_time;

    // Initialize array
    for(int i = 0; i < SIZE; i++)
        arr[i] = i;

    // Cache-friendly access
    start = clock();

    for(int j = 0; j < 100; j++)
    {
        for(int i = 0; i < SIZE; i++)
        {
            sum += arr[i];
        }
    }

    end = clock();
    cache_time = ((double)(end - start)) / CLOCKS_PER_SEC;

    // Cache-unfriendly access
    start = clock();

    for(int j = 0; j < 100; j++)
    {
        for(int i = 0; i < SIZE; i++)
        {
            int index = rand() % SIZE;
            sum += arr[index];
        }
    }

    end = clock();
    nocache_time = ((double)(end - start)) / CLOCKS_PER_SEC;

    printf("Memory Access Latency Demonstration\n");
    printf("-------------------------------\n");
    printf("Cache-Friendly Access Time  : %f seconds\n", cache_time);
    printf("Random Access Time          : %f seconds\n", nocache_time);

    return 0;
}