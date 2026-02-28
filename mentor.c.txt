#include<stdio.h>
#include<string.h>

int main() {

    FILE *file;
    char line[300];
    int lineNumber = 0;
    int mainFound = 0;

    file = fopen("test.c", "r");

    if(file == NULL) {
        printf("Error opening file\n");
        return 1;
    }

    printf("Mini Code Mentor\n\n");

    while(fgets(line, sizeof(line), file)) {

        lineNumber++;

        if(strstr(line, "main()") != NULL)
            mainFound = 1;

        if(strstr(line, "printf") != NULL) {

            int len = strlen(line);

            if(line[len-2] != ';') {

                printf("Error at line %d\n", lineNumber);
                printf("Missing semicolon\n");
                printf("Fix: Add ; at end\n\n");

            }
        }
    }

    if(mainFound == 0) {
        printf("main() function missing\n");
    }

    fclose(file);

    printf("Analysis complete\n");

    return 0;
}
