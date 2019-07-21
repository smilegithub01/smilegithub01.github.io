---
layout: post
title: "add two number in node"
date: 2019-07-21 08:26:33
image: 'https://img-blog.csdn.net/20180211101233457?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29iZXJtaW5lZGVk/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70'
description: java 链表相加返回
category: 'webdev'
tags:
- node
- web
twitter_text:链表相加
introduction: 给出两个非空链表，表示两个非负整数（0-9） ，它们的每个节点都包含一个数字。请将两个链表节点两个数字值相加并将其作为此类链表头返回。
---

#  给定两个值为数字的链表，返回链表数字相加后的链表头节点

面试遇到的一道链表相关的笔试题

##  题目：

> 给出两个非空链表，表示两个非负整数（0-9） ，它们的每个节点都包含一个数字。请将两个链表节点两个数字值相加并将其作为此类链表头返回。
>
> ```java
> class Node {
> 	public int value;
> 	public Node next;
> 	public Node(int value, Node next) {
> 		this.value = value;
> 		this.next = next;
> 	}
>  }
> ```
>
> 给定 nodeA1(value=6,next=nodeA2),nodeA2(value=2,next=nodeA3),nodeA3(value=1,next=null),
>
> nodeB1(value=2,next=nodeB2),nodeB2(value=5,next=null)
>
> 要求返回的链表为
>
> nodeR1(value=6,next=nodeR2),nodeR2(value=4,next=nodeR3),nodeR3(value=6,next=null)



题目要求就是这样，并不是常见的那种一一对应的节点相加（和封面的图有些许差别），个人觉得并不是很严谨，所以结合自己的理解给出的解法如下，当然面试的时候得把自己的解决思路说出来，即使与标准答案有出入，但能体现你自己的思考问题和解决问题的思路就行

## 解法

``` java
public  Node addNode(Node nodeA,Node nodeB){
    	//默认链表A长一些，链表头取A
		Node nodeR = nodeA; 
		if (null == nodeA) {
			return nodeB;
		}else {
			nodeA = nodeA.next;
			while(null != nodeA) {
				if(null != nodeB) {
                    //要求0-9，没有明确说，这里取余方式
					nodeA.value = (nodeA.value + nodeB.value)%10;
					if(nodeA.next == null && null != nodeB.next) {
						nodeA.next = nodeB.next;
						return nodeR;
					}
					nodeB = nodeB.next;
					nodeA = nodeA.next;
				}else {
					return nodeR;
				}
				
			}
			return nodeR;
		}
	}
```

## 测试

```java
   /**
	 *   打印链表
	 * @param node
	 */
	public static void print(Node node) {
		if (node == null) {
			System.out.println("null");
		}{
			while(null != node) {
				System.out.print(node.value+"\t");
				node = node.next;
			}
			System.out.println();
		}
	}
```

```java
	public static void main(String[] args) {
			//6-2-1
			Node nodeA3 = new Node(1,null);
			Node nodeA2 = new Node(2, nodeA3);
			Node nodeA1 = new Node(6, nodeA2);
			
			//2-5
			Node nodeB2 = new Node(5, null);
			Node nodeB1 = new Node(2, nodeB2);
			System.out.println("input nodeA:");
			print(nodeA1);
			System.out.println("input nodeB:");
			print(nodeB1);
			Node nodeR = new AddNode().addNode(nodeA1, nodeB1);
			System.out.println("output nodeR");
			print(nodeR);
		}

```

##  结果

```shell
input nodeA:
6	2	1	
input nodeB:
2	5	
output nodeR
6	4	6
```



