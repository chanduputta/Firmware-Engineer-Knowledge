Data Structures and Simple Algorithms 
========================= 
## **Linked List** 
* Definition: In order to avoid the linear overhead of deletion and insertion, it is possible to allow the table to be stored non-contiguously. Each structure of the linked list contains a table element and a pointer to a structure containing the element's successor, and the Next pointer of the last element points to NULL.
* node definition
```C
    typedef struct node
    {
        struct node *next;
        int num;
    }
    Node;
    typedef struct node* NodePtr;
```  
* Create linked list (with header)  
```C
NodePtr ListCreate(void)
{
    NodePtr Head = (NodePtr)malloc(sizeof(Node));
    if(NULL == Head)
    {
        printf("out of sapce");
        return NULL;
    }
    Head->num = 0;
    Head->next = NULL;
    return Head;
}
```
* Judging that the linked list is empty
```C
int IsListEmpty(NodePtr L)
{
    return L->next == NULL;
}
```
* insert a node
```
int ListInsertNode(NodePtr L,int x , NodePtr p)
{
    NodePtr new = (NodePtr)malloc(Node);
    if(new == NULL)
    {
        printf("out of sapce");
        return -1;
    }
    new->num = x;
    new->next = p->next;
    p->next = new;
    return 0;
}
```
* delete a node
```C
int ListDeleteNode(NodePtr L,int x)
{
    NodePtr p = L;
    while(p->next != NULL && p-next->num != x)
    {
        p = p->next;
        return -1;
    }
    if(p->next != NULL)
    {
        NodePtr Temp = p->next;
        p->next = Temp->next;
        free(Temp);
        return 0;
    }
    return -2;
}
```
* delete linked list
```C
void ListDelete(NodePtr L)
{
    NodePtr p = L->next;
    while(p != NULL)
    {
        NodePtr temp = p->next;
        free(p);
        p = temp;
    }
}
```

## **stack**
* Definition: The stack is a first-in-last-out structure, and the operation of the program is carried out in the stack space.
* create stack
```C
Stack StackCreate(void)
{
	NodePtr Head = (NodePtr)malloc(sizeof(Node));
	if(Head == NULL)
	{
		printf("No free space\n");
		return NULL;
	}
	Head->next = NULL;
	return Head;
}
```
* push
```C
int StackPush(Stack stack, int x)
{
	NodePtr new = (NodePtr)malloc(sizeof(Node));
	if(new == NULL)
	{
		printf("No free space\n");
		return -1;
	}
	new->num = x;
	new->next = stack->next;
	stack->next = new;
	return 0;
}
```
* pop out
```C
int StackPop(Stack stack)
{
	if(!IsStackEmpty(stack))
	{
		NodePtr Temp = stack->next;
		stack->next = Temp->next;
		free(Temp);
		return 0;
	}
	printf("Empty Stack\n");
	return -1;
}
```
* Get the data on the top of the stack
```C
int StackTop(Stack stack)
{
	if(IsStackEmpty(stack))
	{
		printf("Empty Stack\n");
		return 0;
	}
	return stack->next->num;
}
```
* destroy stack
```C
void StackDestory(Stack stack)
{
	NodePtr p = stack->next;
	while(p != NULL)
	{
		NodePtr Temp = p->next;
		free(p);
		p = Temp;
	}
}
```

## **Tree** 
* Basic knowledge 
* A tree is composed of N nodes and N-1 edges
* A node without a son is called a leaf node, and a node without a parent is called a root node.
* A path is a sequence from N1 to N(i 1). In this sequence, each node is the father of the next node, and the length of the path is the number of edges on the path. Every node has a path of length 0 to itself.
* The depth of any node is the length of the only path from the root node to the node, and the depth of the root node is 0.
* The height of any node is the length of the longest path from the node to a leaf, and the height of all leaves is 0.
* The depth of the tree is equal to the depth of its deepest leaf, the height of the tree is equal to the height of the root node, and the height of the tree is equal to the depth


