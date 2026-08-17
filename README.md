#include <stdio.h>
#include <string.h>

typedef struct
{
    char opcode[10];
    char dest[5];
    char src1[5];
    char src2[5];
} Instruction;

int main()
{
    Instruction inst[] =
    {
        {"LW", "R1", "R2", ""},
        {"ADD", "R3", "R1", "R4"},
        {"SUB", "R5", "R3", "R6"},
        {"MUL", "R7", "R5", "R8"}
    };

    int n = 4;
    int stalls = 0, forwards = 0;

    printf("Instruction Sequence:\n\n");

    for(int i = 0; i < n; i++)
    {
        printf("I%d : %s %s %s %s\n",
               i+1,
               inst[i].opcode,
               inst[i].dest,
               inst[i].src1,
               inst[i].src2);
    }

    printf("\nHazard Detection and Resolution\n");
    printf("------------------------------\n");

    for(int i = 1; i < n; i++)
    {
        if(strcmp(inst[i-1].dest, inst[i].src1) == 0 ||
           strcmp(inst[i-1].dest, inst[i].src2) == 0)
        {
            printf("\nHazard between I%d and I%d on register %s\n",
                   i, i+1, inst[i-1].dest);

            if(strcmp(inst[i-1].opcode, "LW") == 0)
            {
                printf("Resolution : STALL inserted (Load-Use Hazard)\n");
                stalls++;
            }
            else
            {
                printf("Resolution : FORWARDING applied\n");
                forwards++;
            }
        }
    }

    printf("\n------------------------------\n");
    printf("Total Forwardings : %d\n", forwards);
    printf("Total Stalls      : %d\n", stalls);

    return 0;
}