数据结构与简单算法
=======================

## **链表**
* 定义 ：为了避免删除与插入时的线性开销，可以允许表不是连续存储的。链表的每一个结构均包含表元素和指向包含该元素后继元的结构的指针，最后一个元素的Next指针指向NULL。
* 节点定义
```C
    typedef struct node
    {
        struct node *next;
        int num;
    }
    Node;
    typedef struct node* NodePtr;
```  
* 创建链表（带表头）  
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
* 判断链表为空
```C
int IsListEmpty(NodePtr L)
{
    return L->next == NULL;
}
```
* 插入一个节点
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
* 删除一个节点
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
* 删除链表
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

## **栈**
* 定义:栈是一种先入后出的结构，程序的运行就是放在栈空间进行的。
* 创建栈
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
* 入栈
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
* 出栈
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
* 获取栈顶数据
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
* 销毁栈
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
* Basic knowledge *
* A tree is composed of N nodes and N-1 edges * A node without a son is called a leaf node, and a node without a parent is called a root node. * A path is a sequence from N1 to N(i 1). In this sequence, each node is the father of the next node, and the length of the path is the number of edges on the path. Every node has a path of length 0 to itself. * The depth of any node is the length of the only path from the root node to the node, and the depth of the root node is 0. * The height of any node is the length of the longest path from the node to a leaf, and the height of all leaves is 0. * The depth of the tree is equal to the depth of its deepest leaf, the height of the tree is equal to the height of the root node, and the height of the tree is equal to the depth


