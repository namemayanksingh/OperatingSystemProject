# OperatingSystemProject
This  project is to calculate the average turnaround time and waiting time using the LRTF Algorithm using system calls.
#include <stdio.h>
struct lrtf
{
int Std_ID; int FoodTime; int WT; int TAT;
};

void accept(struct lrtf list[], int s); void show(struct lrtf list[], int s); void processing(struct lrtf list[], int s); void WT(struct lrtf list[], int n); void TAT(struct lrtf list[], int n);
int main()
{ struct lrtf data[20]; int n,i;
char c='n';
do
{
printf("Number of Students:  ");
scanf("%d", &n);
accept(data, n);
processing(data, n);
WT(data,n);
TAT(data,n);
show(data, n);
printf("Press 'y' to continue....");
scanf("%s",&c);
}while(c=='y');
return 0;
}

void accept(struct lrtf list[80], int s)
{
int i;
for (i = 0; i < s; i++)
{
printf("\n\nEnter data for Student #%d", i + 1);

printf("\nEnter Student id : ");
scanf("%d", &list[i].Std_ID);

printf("Enter time taken for food [ time in minutes as unit ]: ");
scanf("%d", &list[i].FoodTime);
}

}

void show(struct lrtf list[80], int s)
{
int i,AvgWT=0,AvgTAT=0;
int TWT=0,TotalTAT=0;
printf("\n\n\t\t\t\tOutput according to LRTF\n");
printf("\n\t\t\t\t|===============================================================|");
printf("\n\t\t\t\t|Student id\tFoodTime\tWT\tTAT  |");
printf("\n\t\t\t\t|===============================================================|");
for (i = 0; i < s; i++)
{
printf("\n\t\t\t\t|%d\t\t%d\t\t%d\t\t%d\t\t|", list[i].Std_ID, list[i].FoodTime,list[i].WT,list[i].TAT);
printf("\a\n\t\t\t\t|---------------------------------------------------------------|");
TWT= TWT+list[i].WT;
TotalTAT= TotalTAT+list[i].TAT;
}
printf("\n\n\t\t\t\tTotal Waiting Time is: = %d",TWT);
printf("\n\t\t\t\tTotal Turn around Time is: = %d\n\n",TotalTAT);
printf("\n\n\t\t\t\tAverage Waiting Time is: = %d",TWT/s);
printf("\n\t\t\t\tAverage Turn around Time is: = %d\n\n",TotalTAT/s);
}

void processing(struct lrtf list[80], int s)
{
int i, j;
struct lrtf temp;

for (i = 0; i < s - 1; i++)
{
for (j = 0; j < (s - 1-i); j++)
{
if (list[j].FoodTime < list[j + 1].FoodTime)
{
temp = list[j];
list[j] = list[j + 1];
list[j + 1] = temp;
}
else if(list[j].FoodTime == list[j + 1].FoodTime)
{
if(list[j].Std_ID > list[j + 1].Std_ID)
{
temp = list[j];
list[j] = list[j + 1];
list[j + 1] = temp;
}
}
}
}
}


void WT(struct lrtf list[80], int n)
{
int j,total;
list[0].WT=0;
for(j=1;j<n;j++)
{
list[j].WT=list[j-1].WT+list[j-1].FoodTime;
}
}


void TAT(struct lrtf list[80], int n)
{
int j,total;

for(j=0;j<n;j++)
{
list[j].TAT=list[j].WT+list[j].FoodTime;
}
}
