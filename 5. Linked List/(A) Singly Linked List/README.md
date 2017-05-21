# 1. A simple Java program for traversal of a linked list
```sh
import java.io.*;
import java.util.*;
class linkedlist //parent class
{
    Node head; 
    /* 
       Creation of Reference Variable of class Node. head --> null .Since it does not point  to any object or
       intialized to any object 
    */

    /* Inner class made static so that main can access it*/
    static class Node
    {
        int data;
        Node next; /* Creating reference variable not pointing to any object */
        /*Creating a parametrized constructor -- > Invoked when a object is created */
        Node(int d)
        {
          data = d;
          next = null;
        }
     }
     public void printlist()
     {
       Node n = head; //Assigning reference variable 'head' to Reference variable 'n' of class Node
       /*
            Head element normally points to the address of 
            the memory location where the object is stored.
        */
       while(n != null)  //Till the last node. loop runs until last element of a list
       {
         System.out.println(n.data + " ");
         n = n.next; /* Points to next element of the linkedlist  since they are connected to each other */
       }
     }
     /* Method to create simple linkedlist using 3 nodes */
     public static void main(String[] args)
     {
        // Start with a empty list
        linkedlist llist = new linkedlist();
        /*Pointing to reference to an object of class Node*/
        llist.head = new Node(1); // Creation of a new head node
        Node second; //Creation of reference variable of class node. Not pointing to any object. Default a null
        second = new Node(2);// Now pointing reference to an object of class Node. Now we create a second Node
        Node third; //creation of 3 rd node
        third = new Node(3); // Now pointing reference to an object. Creates third Node.
        /*Now we are going to print the element of a linkedlist*/

        /* Three nodes have been allocated  dynamically.
         We have refernces to these three blocks as first,
         second and third

         llist.head        second              third
            |                |                  |
            |                |                  |
        +----+------+     +----+------+     +----+------+
        | 1  | null |     | 2  | null |     |  3 | null |
        +----+------+     +----+------+     +----+------+ */

        /*Now creation of link between these nodes*/
        llist.head.next = second; 
        /* 
            it means list.head.next will point to the same object second is pointing to
            only one object but two references.
         */
 /*  Now next of first Node refers to second.  So they
          both are linked.

       llist.head        second              third
          |                |                  |
          |                |                  |
      +----+------+     +----+------+     +----+------+
      | 1  |  o-------->| 2  | null |     |  3 | null |
      +----+------+     +----+------+     +----+------+ */
        second.next = third; //link the second node with the 3rd node
        /*  Now next of second Node refers to third.  So all three
            nodes are linked.

         llist.head        second              third
            |                |                  |
            |                |                  |
        +----+------+     +----+------+     +----+------+
        | 1  |  o-------->| 2  |  o-------->|  3 | null |
        +----+------+     +----+------+     +----+------+ */
        llist.printlist();

     }
}

```
#### Output:
```sh
1
2
3
```
# 2. Inserting a node
A node can be added in three ways
1) At the front of the linked list
2) After a given node.
3) At the end of the linked list.
### Java program to demonstrate all insertion methods on linked list
```sh
// Linked List | Set 2 (Inserting a node)
// URL: http://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/
class linkedlist
{
  /*Head of the node*/
   Node head; // Reference variable of class Node not pointing to any object
   /*LinkedList node*/
   class Node
   {
     int data;
     Node next;
     // parametrized constructor
     Node(int d)
     {
       data = d;
       next = null;
     }
   }
   /*Insert a node at the front of the list*/
   public void push(int new_data)
   {
        /*1 & 2 Allocate the node and put in data*/
        /*Pointing reference variable to an object*/
        Node new_node = new Node(new_data);
        /*
          3. Make next of new node as the head
        */
        new_node.next =  head;
        /*
         4. Make head to point to the given the given node
        */
        head = new_node;
   }

   /* Insert a node after the given prev_node position*/
   public void insertAfter(Node prev_node,int new_data)
   {
      /* 1.Check if the give Node is NULL*/
      if(prev_node ==  null)
      {
        System.out.println("The given node cannot be NULL");
        return;
      }
      /* 2 & 3 Allocate the node and put data into it */
      Node new_node = new Node(new_data);
      /* 4. Make next of new_node as the next of prev_node */
      new_node.next = prev_node.next;
      /*5. Make next of prev_node as new_node*/
      prev_node.next = new_node;
   }

   /*Append a new node at the end*/
   public void append(int new_data)
   {
     /*1 & 2 Allocate and  put in the data*/
     Node new_node = new Node(new_data);
     /*3. If LinkedList is Empty, make the new node as head*/
     if(head ==  null)
     {
       head = new Node(new_data);
       return;
     }
     /*4. New node is going to be last node, so make next of it as NULL*/
     new_node.next = null;
     /*5. Traverse till the last node */
     Node last = head;
     while( (last.next)!=null)
     {
       last = last.next;
     }
     /* 6. Change last of next as the new node */
     last.next = new_node;
     return;
   }


   /*
      Function prints the contents of the linkedlist starting from the given node
   */
   public void printlist()
   {
     /*
        Create a reference variable tnode of class Node pointing to the same object of
        the reference variable head
     */
     Node tnode = head;
     while(tnode!=null) //until last  node
     {
       System.out.print(tnode.data+" ");
       tnode = tnode.next;
     }
   }

   /*
      Driver program to test above functions.
      Ideally this function should be in a separate user class.
      It is kept here to keep code compact.
   */
   public static void main(String[] args)
   {
      /* Start with the empty list*/
      linkedlist listl = new linkedlist();
      /*
        Insert '6'. So linkedlist becomes
        6-->NULL_LIST
      */
      listl.append(6);
      /*
        Insert 7 at the beginning. So linked list becomes
        7-->6-->NULL_LIST
      */
      listl.push(7);
      /*
        Insert 1 at the beginning so linkedlist becomes
        1-->7-->6-->NULL_LIST
      */
      listl.push(1);
      /*
        Insert 4 at the end so linked list becomes
        1-->7-->6-->4-->NULL_LIST
      */
      listl.append(4);
      /*
        Insert 8 after 7.So linked list becomes
        1-->7-->8-->6-->4-->NULL_LIST
      */
      listl.insertAfter(listl.head.next,8);
      System.out.println("Created Linked list is :");
      listl.printlist();
   }
}

```
#### Output:
Created Linked list is :
1 7 8 6 4
