# Binary-tree-sequence-to-chain-
二叉树顺序存储、链式存储及之间转化与遍历。

## 二叉树顺序存储、链式存储及之间转化与遍历。



**二叉树的存储可用顺序存储方式和链式存储方式，其中顺序存储时存储地址相邻，空间利用率高，但不易进行元素的增删等操作。而链式存储方式的元素可随意存放，但其存储空间所占为数据元素和指针所占空间，存储空间利用率低。**



**数据图如下**



![在这里插入图片描述](https://img-blog.csdnimg.cn/2020042816244280.png)



**完整程序--转化算法如下**


```cpp
#include<iostream>
typedef char datatype;//将队列的节点类型设置为字符型 
using namespace std;

typedef struct node
{
	datatype data;
	struct node* rchild, * lchild;
}BTNode, * BinTree;

typedef struct elem
{
	datatype data;
	int lchild, rchild;
	int tag;//标记是否已申请节点 
	BTNode* link;
}element;

/*函数声明*/
element* CreateBinaryTree(int n);//创建顺序结构二叉树 
BinTree exchange(element* ele, int n);//二叉树线性结构转为二叉结构 
void PreOrder(BTNode* p);//前序遍历 (递归)
void InOrder(BTNode* p);//中序遍历 (递归) 
void PostOrder(BTNode* p);//后续遍历(递归) 

int main()
{
	BinTree root;
	element* ele;
	int n;
	cout << "创建树的节点为：";
	cin >> n;
	cout << endl;
	ele = CreateBinaryTree(n);
	root = exchange(ele, n);
	PreOrder(root);
	InOrder(root);
	PostOrder(root);
}

//创建顺序结构二叉树 
element* CreateBinaryTree(int n)
{
	element* ele = new element[n];
	for (int i = 0; i < n; i++)
	{
		cout << "依次输入第" << i << "个节点的数据 左子树 右子树";
		cin >> ele[i].data >> ele[i].lchild >> ele[i].rchild;
		ele[i].tag = 0;
		ele[i].link = NULL;
		cout << endl;
	}
	return ele;
}

//二叉树线性结构转为二叉结构
BinTree exchange(element* ele, int n)
{
	int i, j;
	BTNode* p, * rchild, * lchild;
	for (int i = 0; i < n; i++)
	{
		if (ele[i].tag == 0)
		{
			p = new BTNode;
			ele[i].link = p;
			ele[i].tag = 1;
			p->data = ele[i].data;
		}
		else
		{
			p = ele[i].link;
		}
		if (ele[i].lchild != -1)//如果当前节点左子树存在 
		{
			j = ele[i].lchild;
			lchild = new BTNode;
			ele[j].link = lchild;
			ele[j].tag = 1;
			lchild->data = ele[j].data;
			p->lchild = lchild;
		}
		else
		{
			p->lchild = NULL;
		}
		if (ele[i].rchild != -1)//如果当前节点右子树存在 
		{
			j = ele[i].rchild;
			rchild = new BTNode;
			ele[j].link = rchild;
			ele[j].tag = 1;
			rchild->data = ele[j].data;
			p->rchild = rchild;
		}
		else
		{
			p->rchild = NULL;
		}
	}
	return ele[0].link;
}

//前序遍历 (递归)
void PreOrder(BTNode* p)
{
	if (p != NULL)
	{
		cout << p->data;
		PreOrder(p->lchild);
		PreOrder(p->rchild);
	}
}

//中序遍历 (递归) 
void InOrder(BTNode* p)
{
	if (p != NULL)
	{
		InOrder(p->lchild);
		cout << p->data;
		InOrder(p->rchild);
	}
}

//后续遍历(递归) 
void PostOrder(BTNode* p)
{
	if (p != NULL)
	{
		PostOrder(p->lchild);
		PostOrder(p->rchild);
		cout << p->data;
	}
}

```

**数据图的运行结果**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200428162110724.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200428161948299.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FzYmJ2,size_16,color_FFFFFF,t_70)
如有问题，欢迎指正。

相关参考资料《数据结构》---周颜军
