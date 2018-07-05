#include <iostream> 
using namespace std;

int flag=0;
typedef struct node* n;              //use n instead of--struct node*

struct node                          //defining linked list
{
    int data;
    struct node *next;
};

struct node *head=NULL;

void printfwd(n node)                //recursion (forward traversal)
{
    if(node==NULL)
    return;
    cout<<node->data;
    if(node->next!=NULL)
    cout<<"->";
    printfwd(node->next);
}

void printbwd(n node)                //recursion (backward traversal)
{
    if(node==NULL)
    return;
    printbwd(node->next);
    cout<<node->data;
    if(node!=head)
    cout<<"->";
}

void insert(int x)                 	 //insertion at the beginning
{
    struct node *temp=(struct node*)malloc(sizeof(struct node*));
    struct node *k=head;
    temp->data=x;
    if(head==NULL)
    {
        head=temp;
    }
    else
    {
        while(k->next!=NULL)
        k=k->next;
        k->next=temp;
    }
    temp->next=NULL;
}

void insert(int pos, int x )        //insertion at the nth position
{
    n temp=(n)malloc(sizeof(n));
    struct node *k=head;
    temp->data=x;
    if(pos==1)
    {
        temp->next=head;
        head=temp;
    }
    else
    {
        for(int i=1;i<pos-1;i++)
        k=k->next;
        temp->next=k->next;
        k->next=temp;
    }
    
    
}

void delet(int pos)                 //deletion at the nth position
{
    n temp=head;
    if(pos==1)
    {
        head=head->next;
        return;
    }
    for(int i=1 ; i<pos-1 ;i++ )
    temp=temp->next;
    temp->next=temp->next->next;
}

void display()                      //displaying the linked list
{
    struct node *temp=head;
    while(temp!=NULL)
    {
        cout<<temp->data;
        if(temp->next!=NULL)
        cout<<"->";
        temp=temp->next;
    }
    cout<<endl;
}

void reverse()                      //reversing the list
{
    n temp = head ;
    n ptemp = NULL ;
    n ntemp = head->next ;
    if(head->next == NULL)
    return;
    for( ; ; ntemp=ntemp->next)
    {
        temp->next = ptemp ;
        ptemp = temp ;
        temp = ntemp ;
        if(ntemp == NULL)
        break;
    }
    head = ptemp ;
}

void dremove()                      //remove duplicate elements from sorted linked list
{
    n temp = head ;
    n ntemp = head -> next;
    while(temp->next != NULL) 
    {
        if(temp->data == ntemp->data)
        {
            ntemp = ntemp -> next ;
            temp -> next = ntemp ;
            
        }
        else 
        {
            temp= temp->next;   
        }
    }
}

bool checkloop()                    //check for cycle
{
    int flag=0;
    n slow=head;
    n fast=head;
    while(fast && fast->next && fast->next->next)
    {
        slow=slow->next;
        fast=fast->next->next;
        if(slow==fast)
        return true;
    }
    slow=head;
    if(!flag)
    return false;
    while(slow!=fast)
    {
        slow=slow->next;
        fast=fast->next;
    }
    return slow;
}

void rotate()                       //rotating clockwise
{
    n temp=head;
    while(temp->next!=NULL)
    temp=temp->next;
    temp->next=head;
    head=temp;
    while(temp->next!=head)
    temp=temp->next;
    temp->next=NULL;
}

void anticlock()
{
    n temp=head;
    while(temp->next!=NULL)
    temp=temp->next;
    temp->next=head;
    head=head->next;
    temp->next->next=NULL;
}

int x=1;
void add1(n temp)                   //addng 1 to a no. represented as LL
{
    if(temp==NULL)
    return;
    
    add1(temp->next);
    
    temp->data+=x;
    x=temp->data/10;
    if(temp->data>=10)
    {
        temp->data%=10;
    }
    
    return;
}

int main ()
{
    
  insert(2);                //insertion at the beginning
  insert(3);
  insert(4);
  insert(6);
  display();                //displaying the linked list
  
  printfwd(head);           //recursion
  cout<<endl;
  
  printbwd(head);           //recursion
  cout<<endl;
  
  insert(4 ,5);             //insertion at the nth position
  display();
  
  delet(5);                 //deletion at the nth position
  display();
  
  reverse();                //reversing the list
  display();
  
  insert( 5 ,1 );
  display();
  
  reverse();
  display();
  
  insert( 3 , 3 );
  insert( 5 ,4 );
  insert( 8 ,5 );
  insert( 8 ,5 );
  display();
  
  cout<<checkloop();        //check for cycle
  cout<<endl;
  
  dremove();                //removing duplicate elements
  display();
  
  rotate();                 //rotating clockwise
  display();
  
  rotate();
  display();
  
  insert( 6, 9 );
  insert( 7, 9 );
  display();
  
  anticlock();              //rotating anticlockwise
  display();
  
  anticlock();
  display();
  
  add1(head);               //addng 1 to a no. represented as LL
  display();
  
  return 0;
}
