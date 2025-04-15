#include <stdio.h>
#include <sys/stat.h>
#include <unistd.h>

int main() {
    struct stat fileStat;
    char filename[100];

    printf("Enter file name: ");
    scanf("%s", filename);

    if (stat(filename, &fileStat) < 0) {
        perror("stat() error");
        return 1;
    }

    printf("File Size: %ld bytes\n", fileStat.st_size);
    printf("Number of Links: %ld\n", fileStat.st_nlink);
    printf("File inode: %ld\n", fileStat.st_ino);
    printf("File Permissions: %o\n", fileStat.st_mode & 0777);
    printf("Last accessed: %ld\n", fileStat.st_atime);

    return 0;
}







#include <stdio.h>

int main() {
    int n, i;
    int bt[20], wt[20], tat[20];
    float avg_wt = 0, avg_tat = 0;

    printf("Enter total number of processes: ");
    scanf("%d", &n);

    printf("Enter Burst Time for each process:\n");
    for(i = 0; i < n; i++) {
        printf("P[%d]: ", i+1);
        scanf("%d", &bt[i]);
    }

    wt[0] = 0; // First process has 0 waiting time

    for(i = 1; i < n; i++) {
        wt[i] = wt[i-1] + bt[i-1];
    }

    for(i = 0; i < n; i++) {
        tat[i] = wt[i] + bt[i];
        avg_wt += wt[i];
        avg_tat += tat[i];
    }

    printf("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time\n");
    for(i = 0; i < n; i++) {
        printf("P[%d]\t%d\t\t%d\t\t%d\n", i+1, bt[i], wt[i], tat[i]);
    }

    printf("\nAverage Waiting Time = %.2f", avg_wt/n);
    printf("\nAverage Turnaround Time = %.2f", avg_tat/n);

    return 0;
}
