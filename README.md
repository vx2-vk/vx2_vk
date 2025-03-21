FIFO

The simplest algorithm for replacing pages is this one. The operating system maintains a queue for all of the memory pages in this method, 
with the oldest page at the front of the queue. The first page in the queue is chosen for removal when a page has to be replaced.

#include < stdio.h >  
int main()  
{  
    int incomingStream[] = {4 , 1 , 2 , 4 , 5};  
    int pageFaults = 0;  
    int frames = 3;  
    int m, n, s, pages;   
    pages = sizeof(incomingStream)/sizeof(incomingStream[0]);   
    printf(" Incoming \ t Frame 1 \ t Frame 2 \ t Frame 3 ");  
    int temp[ frames ];  
    for(m = 0; m < frames; m++)  
    {  incomi
        temp[m] = -1;  
    }  
    for(m = 0; m < pages; m++)  
    {  
        s = 0;   
        for(n = 0; n < frames; n++)  
        {  
            if(incomingStream[m] == temp[n])  
            {  
                s++;  
                pageFaults--;  
            }  
        }  
        pageFaults++;  
        if((pageFaults <= frames) && (s == 0))  
        {  
            temp[m] = incomingStream[m];  
        }  
        else if(s == 0)  
        {  
            temp[(pageFaults - 1) % frames] = incomingStream[m];  
        }  
        printf("\n");  
        printf("%d\t\t\t",incomingStream[m]);  
        for(n = 0; n < frames; n++)  
        {  
            if(temp[n] != -1)  
                printf(" %d\t\t\t", temp[n]);  
            else  
                printf(" - \t\t\t");  
        }  
    }  
    printf("\nTotal Page Faults:\t%d\n", pageFaults);  
    return 0;  
}  

//LRU

AIM:

To write a c program to implement LRU page replacement algorithm

ALGORITHM :

1. Start the process

2. Declare the size

3. Get the number of pages to be inserted

4. Get the value

5. Declare counter and stack

6. Select the least recently used page by counter value

7. Stack them according the selection.

8.  Display the values

9. Stop the process

PROGRAM:
#include<stdio.h>
main()
{
int q[20],p[50],c=0,c1,d,f,i,j,k=0,n,r,t,b[20],c2[20];
printf("Enter no of pages:");
scanf("%d",&n);
printf("Enter the reference string:");
for(i=0;i<n;i++)
            scanf("%d",&p[i]);
printf("Enter no of frames:");
scanf("%d",&f);
q[k]=p[k];
printf("\n\t%d\n",q[k]);
c++;
k++;
for(i=1;i<n;i++)
            {
                        c1=0;
                        for(j=0;j<f;j++)
                        {
                                    if(p[i]!=q[j])
                                    c1++;
                        }
                        if(c1==f)
                        {
                                    c++;
                                    if(k<f)
                                    {
                                                q[k]=p[i];
                                                k++;
                                                for(j=0;j<k;j++)
                                                printf("\t%d",q[j]);
                                                printf("\n");
                                    }
                                    else
                                    {
                                                for(r=0;r<f;r++)
                                                {
                                                            c2[r]=0;
                                                            for(j=i-1;j<n;j--)
                                                            {
                                                            if(q[r]!=p[j])
                                                            c2[r]++;
                                                            else
                                                            break;
                                                }
                                    }
                                    for(r=0;r<f;r++)
                                     b[r]=c2[r];
                                    for(r=0;r<f;r++)
                                    {
                                                for(j=r;j<f;j++)
                                                {
                                                            if(b[r]<b[j])
                                                            {
                                                                        t=b[r];
                                                                        b[r]=b[j];
                                                                        b[j]=t;
                                                            }
                                                }
                                    }
                                    for(r=0;r<f;r++)
                                    {
                                                if(c2[r]==b[0])
                                                q[r]=p[i];
                                                printf("\t%d",q[r]);
                                    }
                                    printf("\n");
                        }
            }
}
printf("\nThe no of page faults is %d",c);
}


//LFU
Introduction to LFU page replacement :

The least frequently used(LFU) page-replacement algorithm requires that the page with the smallest count be replaced. 
The reason for this selection is that an actively used page should have a large reference count. 
A problem arises, however, when a page is used heavily during the initial phase of a process but then is never used again. 
Since it was used heavily, it has a large count and remains in memory even though it is no longer needed. 
One solution is to shift the counts right by1bit at regular intervals,forming an exponentially decaying average usage count.

C program for LFU page replacement :

 #include<stdio.h>
void print(int frameno,int frame[])
{
            int j;
            for(j=0;j<frameno;j++)
            printf("%d\t",frame[j]);
            printf("\n");
}         
int main()
{
            int i,j,k,n,page[50],frameno,frame[10],move=0,flag,count=0,count1[10]={0},
                        repindex,leastcount;
            float rate;
            printf("Enter the number of pages\n");
            scanf("%d",&n);
            printf("Enter the page reference numbers\n");
            for(i=0;i<n;i++)
            scanf("%d",&page[i]);
            printf("Enter the number of frames\n");
            scanf("%d",&frameno);
            for(i=0;i<frameno;i++)
            frame[i]=-1;
            printf("Page reference string\tFrames\n");
            for(i=0;i<n;i++)
            {
                        printf("%d\t\t\t",page[i]);
                        flag=0;
                        for(j=0;j<frameno;j++)
                        {
                                    if(page[i]==frame[j])
                                    {
                                                flag=1;
                                                count1[j]++;
                                                printf("No replacement\n");
                                                break;
                                    }
                        }
                        if(flag==0&&count<frameno)
                        {
                                    frame[move]=page[i];
                                    count1[move]=1;
                                    move=(move+1)%frameno;
                                    count++;
                                    print(frameno,frame);
                        }
                        else if(flag==0)
                        {
                                    repindex=0;
                                    leastcount=count1[0];
                                    for(j=1;j<frameno;j++)
                                    {
                                                if(count1[j]<leastcount)
                                                {
                                                            repindex=j;
                                                           leastcount=count1[j];
                                                }
                                    }
                                   
                                    frame[repindex]=page[i];
                                    count1[repindex]=1;
                                    count++;
                                    print(frameno,frame);
                        }
            }
            rate=(float)count/(float)n;
            printf("Number of page faults is %d\n",count);
            printf("Fault rate is %f\n",rate);
            return 0;
}
