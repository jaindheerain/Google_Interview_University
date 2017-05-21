# Linked List vs Array
Both Arrays and Linked List can be used to store linear data of similar types, but they both have some advantages and disadvantages over each other.

Following are the points in favour of Linked Lists.

(1)	The size of the arrays is fixed: So we must know the upper limit on the number of elements in advance. Also, generally, the allocated memory is equal to the upper limit irrespective of the usage, and in practical uses, upper limit is rarely reached.

(2)	Inserting a new element in an array of elements is expensive, because room has to be created for the new elements and to create room existing elements have to shifted.

For example, suppose we maintain a sorted list of IDs in an array id[].

id[] = [1000, 1010, 1050, 2000, 2040, …..].

And if we want to insert a new ID 1005, then to maintain the sorted order, we have to move all the elements after 1000 (excluding 1000).

Deletion is also expensive with arrays until unless some special techniques are used. For example, to delete 1010 in id[], everything after 1010 has to be moved.

So Linked list provides following two advantages over arrays
1)	Dynamic size
2)	Ease of insertion/deletion

Linked lists have following drawbacks:
1)	Random access is not allowed. We have to access elements sequentially starting from the first node. So we cannot do binary search with linked lists.
2)	Extra memory space for a pointer is required with each element of the list.
3) Arrays have better cache locality that can make a pretty big difference in performance.

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
```sh
Created Linked list is :
1 7 8 6 4
```
# 3. Deleting a node
To delete a node from linked list, we need to do following steps.
1) Find previous node of the node to be deleted.
2) Changed next of previous node.
3) Free memory for the node to be deleted.
### Java program to demonstrate deletion in singly linked list
```sh
class linkedlist
 {
      /*
        head -> reference variable of class Node
        head is not pointing to any object
      */
      Node head; // head of the linkedlist
      /*
        LinkedList node
      */
      class Node
      {
          int data;
          Node next;
          /*
              Creation of parametrized constructor
              Invoked when object is created
          */
          Node(int d)
          {
            data = d;
            next = null;
          }
      }

      /*
        Given an key, delete the first occurence of the key
        in the given linked list
      */
      public void deleteNode(int key)
      {
          /*
              Store the head node in a reference variable temp
              So that both poiting to the same object
          */
          Node temp = head;
          /*
              Creating ref variable prev of class Node
              and not pointing to an object
          */
          Node prev = null;
          /*
              If head node itself hold the key to be deleted
          */
          if(temp!=null && temp.data==key)
          {
            head = temp.next; // Changed head
            return;
          }
          /*
              Search for the key to be deleted,
              keep track of previous node as we
              need to change temp.next
          */
          while(temp!=null && temp.data!=key)
          {
              prev = temp;
              temp = temp.next;
          }
          /*
            At the end of the loop if the LinkedList contains the key then,
            temp --> Actually hold the key(reference)
          */
          /*
            If key was not present in the linked list
          */
          if(temp == null)
          {
            return;
          }
          /*
            Unlink the node to be deleted from the linked list
            In this case node to be deleted is temp
          */
          /*
            For example:
            LinkedList contains : 1-->2-->3-->4-->5
            Key to be deleted : 3
            While loop execution:
            1) temp!=null && 1!=key
               Now, prev = 1
                    temp = 2
            2) temp!=null && 2!=key
               Now, prev = 2
                    temp = 3
           3) temp!=null && 3==key --> Condition fails
           Now we can see 'temp', holds the key to be deleted
           After deletion linkedlist should look like below

           LinkedList contains: 1-->2-->4-->5
           You can see that prev.next is linked to temp.next
           so unlink the temp node
           prev.next = temp.next;
          */
          prev.next = temp.next;
      }
      /* Insert a node at the front of the linkedlist */
      public void push(int new_data)
      {
          Node new_node = new Node(new_data);
          new_node.next = head;
          head = new_node;
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
          while(tnode != null)
          {
            System.out.print(tnode.data+" ");
            tnode = tnode.next;
          }
      }

      /*
          Driver program to test the above function.
          Ideally function should be in seperate class.
          Its kept here for code compatibility
      */
      public static void main(String[] args)
      {
          linkedlist llist = new linkedlist();
          /*
            Every node_data is  added to the front of  the list
            i.e., they become the head
          */
          llist.push(5);
          llist.push(4);
          llist.push(3);
          llist.push(2);
          llist.push(1);
          /*
              Linked list contains 1-->2-->3-->4-->5-->NULL
          */
          System.out.println("Created Linked List is:");
          llist.printlist();
          System.out.println();
          /*
            Deletion of Node contains data 3
          */
          llist.deleteNode(3);
          System.out.println("Linked list after deletion:");
          llist.printlist();
      }
 }
```
#### Output:
```sh
Created Linked List is:
1 2 3 4 5
Linked list after deletion:
1 2 4 5
```
# 4. Delete a Linked List node at a given position
Given a singly linked list and a position, delete a linked list node at the given position.
#### Example:
```sh
Input: position = 1, Linked List = 8->2->3->1->7
Output: Linked List =  8->3->1->7

Input: position = 0, Linked List = 8->2->3->1->7
Output: Linked List = 2->3->1->7
```
#### Java program to delete a node in a linked list at a given position
```sh
/*
    Delete a Linked List node at a given position
*/
class linkedlist
{
    /*
      Creating a reference variable head of class Node.
      Not pointing to any object
    */
    Node head;
    /*LinkedList node*/
    class Node
    {
      int data;
      /*
        Creating a reference variable next of class Node.
        Not pointing to any object
      */
      Node next;
      /*
        Parametrized Constructor
        It gets invoked when an object gets created
      */
      Node(int d)
      {
        data = d;
        next = null;
      }
    }
    /*
      Now creating push() function to
      push elements at the end of the list
    */
    public void push(int node_data)
    {
      /*
          Creating a reference variable new_node
          of class Node pointing to an object
      */
      Node new_node = new Node(node_data);
      /*
          If the head -->Null
      */
      if(head == null)
      {
        // head is now pointing to an object
        head = new Node(node_data);
        return; //end the function
      }
      /*
          Now we have to push the new_node in the last positon
          of the linkedlist
      */
      Node lastnode = head; //both reference pointing to same object
      /*
          Now iterate the refernce variable to the last node.
      */
      while(lastnode.next!=null)
      {
        lastnode = lastnode.next;
      }
      /*
          suppose LinkedList contains 1-->2-->3-->4-->5
          lastnode = 1
          While loop execution
          1. lastnode.next(2)! = null
             lastnode = 3
          2. lastnode.next(4)! = null
             lastnode = 5
          3. lastnode.next == null (Loop condion FAILS)
          so lastnode = 5
      */
      /*
          Now new_node should become lastnode
          so next element of new_node should be a null
      */
      new_node.next = null;
      /*To link new_node to the lastnode*/
      lastnode.next = new_node;
    }

    /*
        Now we have to delete a node at a given positon
    */
    public void deleteNode(int pos)
    {
        /*
          If node to be deleted is a first node i.e. head
          You can end the function Assigning next element of
          nod as head
        */
        if(pos==0) //head
        {
          head = head.next;
          return; //ending the function here
        }
        /*
            For deleting a node we need two reference variable
            1. Node to be deleted (say key)
            2. Previous_Node (say prev_node)
            Finally we link
            prev_node.next = key.next (unlinking the key i.e.
            value to be deleted)
        */
        /*
            key is a reference variable
            pointing to the same object of head
        */
        Node key = head;
        Node prev = null;
        /* Now iterate to find the node to be deleted */
        for(int i=0;i<pos;i++)
        {
            if(i==pos)
            {
               //do nothing
            }
            else
            {
              prev = key;
              key = key.next;
            }
        }
        /*
            Now key contains the elements to be deleted
        */
        /*
            prev ->is the previous element of the key node
        */
        /*
            Suppose linkedlist contains: 1-->2-->3-->4-->5
            Now deletion at position 1  i.e. node 2
            key = 2 (node to be deleted)
            prev = 1
            After deletion linkedlist contains:1-->3-->4-->5
            Now prev.next mapped with key.next
            to unlink key(i.e node to be deleted)
            Map prev.next --with--> key.next
        */
        prev.next = key.next;
        return; //end function
    }
    /*
        Now print the elements of the linked list
    */
    void printlist()
    {
        /*
            tnode is a reference variable of class Node pointing
            to same object head is pointing to.
        */
        Node tnode =  head;

        while(tnode != null)
        {
          System.out.print(tnode.data+" ");
          tnode = tnode.next;
        }
        System.out.println();
    }
    /*
      Now the driver program
    */
    public static void main(String[] args)
    {
        linkedlist llist = new linkedlist();
        llist.push(1);
        llist.push(2);
        llist.push(3);
        llist.push(4);
        llist.push(5);
        System.out.println("Linked list contains:");
        llist.printlist();
        /*
            Linked list after the deletion of a node at position 0
        */
        llist.deleteNode(0);
        System.out.println("Linked list after the deletion of a node at position 0");

        llist.printlist();
        /*
          Linked list after deletion at position 2 (3rd element)
        */
        llist.deleteNode(2);

        System.out.println("Linked list after deletion at position 2 (3rd element)");

        llist.printlist();

    }
}

```
#### Output:
```sh
Linked list contains:
1 2 3 4 5
Linked list after the deletion of a node at position 0
2 3 4 5
Linked list after deletion at position 2 (3rd element)
2 3 5
```
