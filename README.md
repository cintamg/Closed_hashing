# Closed_hashing
This is a program that is used to allocate memory locations for values in a hash table using hash function.
#include<stdio.h>
#include<stdlib.h>
#define SIZE 10
struct node
{
    int data;
    struct node *next;
};
struct node *head[SIZE]={NULL},*c;
struct pair
{
    int value;
    int key;
};
int max=0;
struct pair hash_table[SIZE];
void closeDisplay();
void closeInsert();
void closeSearch();
void openDisplay();
void openInsert();
void openSearch();
void main()
{
    printf("\nHash function : h(k)=k (mod 10)+1\n");
    int size,i,temp,ch,choice=0;
    while(choice!=3)
    {
    printf("\n");
    printf("1.Open hashing\n2.Closed hashing\n3.Exit\n");
    printf("Enter your choice : ");
    scanf("%d",&choice);
    switch(choice)
    {
    case 1:
    ch=0;
    while(ch!=4)
    {
    printf("\n");
    printf("1.Insert\n2.Search\n3.Display\n4.Exit\n");
    printf("Enter your choice\n");
    scanf("%d",&ch);
    switch(ch)
    {
    case 1:
       openInsert();
       break;
    case 2:
       openSearch();
       break;
    case 3:
       openDisplay();
       break;
    case 4:
       break;
    default:
        printf("Invalid choice\n");
    }
    }
    break;
    case 2:
    ch=0;
    while(ch!=4)
    {
    printf("\n");
    printf("1.Insert\n2.Search\n3.Display\n4.Exit\n");
    printf("Enter your choice\n");
    scanf("%d",&ch);
    switch(ch)
    {
    case 1:
       closeInsert();
       break;
    case 2:
       closeSearch();
       break;
    case 3:
       closeDisplay();
       break;
    case 4:
       break;
    default:
        printf("Invalid choice\n");
    }
    }
    break;
    case 3:
    break;
    default:
    printf("Invalid choice\n");
    }
    }
}
void closeDisplay()
{
    int i;
    printf("Index\tKey\n");
    for(i=1;i<=SIZE;i++)
        printf("%d\t%d\n",i,hash_table[i].value);
        printf("\n");
}
void closeInsert()
{
    max++;
    if(max<=SIZE)
    {
    int val,i,temp;
    printf("Enter the elements : ");
    scanf("%d",&temp);
    val=temp%SIZE+1;
    for(i=0;i<SIZE;i++)
    {
        if(temp==hash_table[i].value)
        {
            printf("Duplication\n");
            return;
        }
    }
    while(hash_table[val].value!=NULL)
        val=(val+1)%SIZE;
    hash_table[val].value=temp;
    hash_table[val].key=val;
    }
    else
        printf("Hash table overflow\n");
}
void closeSearch()
{
    int temp,index;
    int flag=0;
    printf("Enter the element : ");
    scanf("%d",&temp);
    index=temp%SIZE+1;
    do
    {
        if(hash_table[index].value==temp)
        {
            printf("%d found at index %d\n",hash_table[index].value,index);
            flag=1;
            break;
        }
        else
            index=(index+1)%SIZE;
    }while(index!=temp%SIZE+1);
    if(flag==0)
        printf("Element not found\n");
    printf("\n");
}
void openInsert()
{
    int i,key;
    printf("Enter the element : ");
    scanf("%d",&key);
    i=key%SIZE+1;
    struct node *newnode=(struct node*)malloc(sizeof(struct node));
    newnode->data=key;
    newnode->next=NULL;
    if(head[i]==NULL)
        head[i]=newnode;
    else
    {
        c=head[i];
        while(c->next!=NULL)
            c=c->next;
        c->next=newnode;
    }
}
void openSearch()
{
    int key,index;
    printf("Enter the element : ");
    scanf("%d",&key);
    index=key%SIZE+1;
    if(head[index]==NULL)
        printf("Element not found\n");
    else
    {
        for(c=head[index];c!=NULL;c=c->next)
        {
            if(c->data==key)
            {
                printf("%d found at index %d\n",key,index);
                break;
            }
        }
        if(c==NULL)
            printf("Element not found\n");
    }
}
void openDisplay()
{
    int i;
    printf("Index\tKey\n");
    for(i=1;i<=SIZE;i++)
    {
        printf("\n");
        if(head[i]==NULL)
        {
            printf("%d\t0",i);
            continue;
        }
        else
        {
            c=head[i];
            printf("%d\t%d",i,c->data);
            c=c->next;
            for(;c!=NULL;c=c->next)
                printf("->%d",c->data);
        }
    }
    printf("\n");
}
