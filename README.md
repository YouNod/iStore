#include<stdio.h>

#include<stdlib.h>

#include<string.h>

struct stud_node
{

	int num;
	char name[20];
	int score;
	struct stud_node *next;
};

struct stud_node *Creat_Stu_Doc();

struct stud_node *DeleteDoc(struct stud_node *head,int min_score);

void Ptrint_Stu_Doc(struct stud_node *head);

void main()
{

	struct stud_node *head;
	int min_score;

	head=Creat_Stu_Doc();
	scanf("%d",&min_score);
	head=DeleteDoc(head,min_score);
	Ptrint_Stu_Doc(head);
}


struct stud_node *Creat_Stu_Doc()
{

	int num,score;
	char name[20];
	int size=sizeof(struct stud_node);	
	struct stud_node *head,*tail,*pt;	
	head=tail=NULL;		
	
	scanf("%d",&num);
	while(num!=0)
	{
		
		pt=(struct stud_node *)malloc(size);
		scanf("%s%d",&name,&score);
		
		pt->num=num;
		strcpy(pt->name,name);
		pt->score=score;
		pt->next=NULL;
		
		if(head==NULL)head=pt; 
		else tail->next=pt;	
		
		tail=pt;
		scanf("%d",&num);
	}
	return head;
} 

struct stud_node *DeleteDoc(struct stud_node *head,int min_score)
{

	struct stud_node *p1,*p2;
	while(head->score<min_score)
	{
		p2=head;
		head=head->next;
		free(p2);
	}
	
	if(head==NULL)return NULL;
	
	p1=head;
	p2=head->next;
	while(p2!=NULL)
	{
		if(p2->score<min_score)
		{
			p1->next=p2->next; 
			free(p2);
		}
		else
		{
			p1=p2;
			p2=p2->next;
		}
	}//最后一个链结是不是无法删去？ 
	return head;
}

void Ptrint_Stu_Doc(struct stud_node *head)
{

	struct stud_node *p;
	if(head==NULL)return;
	for(p=head;p;p=p->next)
	{
		printf("%d %s %d",p->num,p->name,p->score);
	
	}//最后一项可能没写上 
}

 
