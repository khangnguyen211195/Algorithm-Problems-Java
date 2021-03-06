## Stack

```java
public class Stack {
	private int maxSize;
	private char[] stackArray;
	private int top;

	public Stack(int size) {
		this.maxSize = size;
		this.stackArray = new char[maxSize];
		this.top = -1;
	}

	public void push(char j) {
		if(isFull()) {
			System.out.println("This stack is already full");
		} else {
			top++;
			stackArray[top] = j;
		}
	}

	public char pop() {
		if(isEmpty()) {
			System.out.println("This stack is already empty");
			return '0';
		}else {
			int old_top = top;
			top--;
			return stackArray[old_top];
		}
	}

	public char peek() {
		return stackArray[top];
	}

	public boolean isEmpty() {
		return (top == -1);
	}

	public boolean isFull() {
		return (maxSize - 1 == top);
	}
}

public class App {

	public static void main(String[] args) {
		Stack theStack = new Stack(3);
		theStack.push(20);
		theStack.push(40);
		theStack.push(60);
		theStack.push(80);

		while(!theStack.isEmpty()) {
			long value = theStack.pop();
			System.out.println(value);
		}
		/*
		This stack is already full
		60
		40
		20
		*/

		System.out.println(reverseString("HELLO"));
		// OLLEH
	}

	public static String reverseString(String str) {
		int stackSize = str.length(); // get the max stack size
		Stack theStack = new Stack(stackSize);
		for(int j = 0; j < str.length(); j++) {
			char ch = str.charAt(j);
			theStack.push(ch);
		}

		String result = "";
		while(!theStack.isEmpty()) {
			char ch = theStack.pop();
			result = result + ch; // appending to the output
		}

		return result;
	}
}
```
----

## Queue

```java
public class Queue {
	private int maxSize; // Initializes the set number of slots
	private long[] queArray; // slots to maintain the data
	private int front; // this will be the index position for the element in the front
	private int rear; // going to be the index position for the lement at the back of the line
	private int nItems; // counter to maintain the nunber of items in our queue

	public Queue(int size) {
		this.maxSize = size;
		this.queArray = new long[size];
		front = 0; // index position of the first slot of the array
		rear = -1; // There is no item in the array yet to be considered as the last item.
		nItems = 0; // we don't have elements in the array yet
	}

	public void insert(long j) {
		if(rear == maxSize - 1) {
			rear = -1;
		}

		rear++;
		queArray[rear] = j;
		nItems++;
	}

	public long remove() { // remove item from the front of the queu
		long temp = queArray[front];
		front++;
		if(front == maxSize) {
			front = 0; // we can set front back to the 0th index so that we can utilize the entire array again.
		}

		nItems--;
		return temp;
	}

	public long peekFront() {
		return queArray[front];
	}

	public boolean isFull() {
		return (nItems == maxSize);
	}

	public void view() {
		System.out.print("[");
		for(int i = 0; i < queArray.length; i++) {
			System.out.print(queArray[i] + " " );
		}
		System.out.print("]");
	}
}

public class App {

	public static void main(String[] args) {
		Queue myQueue = new Queue(5);
		myQueue.insert(100);
		myQueue.insert(1000);
		myQueue.insert(14);
		myQueue.insert(12);
		myQueue.insert(44);
		myQueue.insert(33);
		myQueue.view();
	}
}

// [33 1000 14 12 44 ]
```

------


## Singly LinkedList

```java
public class Node {
	public int data;
	public Node next;

	public void displayNode() {
		System.out.println("{ " + data + " } ");
	}
}

public class SinglyLinkedList {
	private Node first;

	public SinglyLinkedList() {

	}

	public boolean isEmpty() {
		return (first == null);
	}

	// used to insert at the beginning of the list
	public void insertFirst(int data) {
		Node newNode = new Node();
		newNode.data = data;
		newNode.next = first;
		first = newNode;
	}

	public void insertLast(int data) {
		Node current = first;

		while(current.next != null) {
			current = current.next;
		}

		Node newNode = new Node();
		newNode.data = data;
		current.next = newNode;
	}

	public Node deleteFirst() {
		Node temp = first;
		first = first.next;
		return temp;
	}

	public void displayList() {
		System.out.println("List: (first --> last ");

		Node current = first;
		while(current != null) {
			current.displayNode();
			current = current.next;
		}
		System.out.println();
	}
}

public class App {

	public static void main(String[] args) {
		SinglyLinkedList myList = new SinglyLinkedList();
		myList.insertFirst(100);
		myList.insertFirst(52);
		myList.insertFirst(99);
		myList.insertFirst(88);
		myList.insertLast(99999);

		myList.displayList();
	}
}
/*
List: (first --> last
{ 88 }
{ 99 }
{ 52 }
{ 100 }
{ 99999 }
*/
```


## Circular LinkedList

```java
public class Node {
	public int data;
	public Node next;

	public void displayNode() {
		System.out.println("{ " + data + " } ");
	}
}

public class CircularLinkedList {
	private Node first;
	private Node last;

	public CircularLinkedList() {
		first = null;
		last = null;
	}

	private boolean isEmpty() {
		return first == null;
	}

	public void insertFirst(int data) {
		Node newNode = new Node();
		newNode.data = data;

		if(isEmpty()) {
			last = newNode;
		}

		newNode.next = first; // newNode --> old first
		first = newNode;
	}

	public void insertLast(int data) {
		Node newNode = new Node();
		newNode.data = data;

		if(isEmpty()) {
			first = newNode;
		} else {
			last.next = newNode; // the next value of the last node will point to the new node
			last = newNode; // we make the new node we create be the last one in the list
		}
	}

	public int deleteFirst() {
		int temp = first.data;

		if(first.next == null) {
			last = null;
		}

		first = first.next; // first will point to old's next value
		return temp;
	}

	public void displayList() {
		System.out.println("List (first --> last)");
		Node current = first;
		while(current != null) {
			current.displayNode();
			current = current.next;
		}
		System.out.println();
	}
}



	public class App {
		public static void main(String[] args) {
			CircularLinkedList myList = new CircularLinkedList();
			myList.insertFirst(100);
			myList.insertFirst(50);
			myList.insertFirst(99);
			myList.insertFirst(88);
			myList.insertLast(999999);

			myList.displayList();
		}
	}
/*
List (first --> last)
{ 88 }
{ 99 }
{ 50 }
{ 100 }
{ 999999 }
*/
```

-------

## Doubly LinkedList

```java
public class Node {
	public int data;
	public Node next;
	public Node previous;

	public void displayNode() {
		System.out.print("{ " + data + " }");
	}
}

public class DoublyLinkedList {
	private Node first;
	private Node last;

	public DoublyLinkedList() {
		this.first = null;
		this.last = null;
	}

	public boolean isEmpty() {
		return first == null;
	}

	public void insertFirst(int data) {
		Node newNode = new Node();
		newNode.data = data;

		if(isEmpty()) {
			last = newNode; // if empty, last will refer to the new Node being created
		} else {
			first.previous = newNode;
		}

		newNode.next = first; // the new node's next field will point to the old first
		this.first = newNode;
	}

	public void insertLast(int data) {
		Node newNode = new Node();
		newNode.data = data;

		if(isEmpty()) {
			first = newNode;
		} else {
			last.next = newNode; // assigning old last to newNode
			newNode.previous = last;
		}

		this.last = newNode; // the linkedList's last field should point to the new node
	}

	// Assume non-empty list
	public Node deleteFirst() {
		Node temp = first;
		if(first.next == null) { // there is only one item in the list
			last = null;
		} else {
			first.next.previous = null;
		}

		first = first.next; // we are assigning the reference of the node following the old first node to the first field in the linked list object
		return temp; // return the deleted old first node;
	}

	// assume non-empty list
	public Node deleteLast() {
		Node temp = last;
		if(first.next == null) { // we only have one node in this list
			first = null;
		} else {
			last.previous.next = null; // the last node's previous node's next field will point to null
		}

		last = last.previous;
		return temp;
	}

	// assume non-empty list
	public boolean insertAfter(int key, int data) { // key is the node's data we looking for to insert a new data
		Node current = first; // we start from the beginning of the list
		while(current.data != key) {
			current = current.next;
			if(current == null) {
				return false;
			}
		}

		Node newNode = new Node();
		newNode.data = data;

		if(current == last) {
			current.next = null;
			last = newNode;
		} else {
			newNode.next = current.next; // new node's next field should point to the node ahead of the current node
			current.next.previous = newNode; // the node ahead of current, it's previous field should point to the new node
		}

		newNode.previous = current;
		current.next = newNode;

		return true;
	}

	// assume non-empty list
	public Node deleteKey(int key) {
		Node current = first;
		while(current.data != key) {
			current = current.next;
			if(current == null) {
				return null;
			}
		}

		if(current == first) {
			first = current.next; // make the first field point to the node following current since current
		} else {
			current.previous.next = current.next;
		}

		if (current == last) {
			last = current.previous;
		} else {
			current.next.previous = current.previous;
		}

		return current;
	}

	public void displayForward() {
		System.out.print("List (first --> last): ");
		Node current = first; // start from the beginning
		while(current != null) {
			current.displayNode(); // call the display method of the node
			current = current.next; // move to the next node
		}
		System.out.println();
	}

	public void displayBackwrard() {
		System.out.print("List (last --> first): ");
		Node current = last; // start from the beginning
		while(current != null) {
			current.displayNode(); // call the display method of the node
			current = current.previous; // move to the previous node
		}
		System.out.println();
	}
}


public class App {

	public static void main(String[] args) {
		DoublyLinkedList theList = new DoublyLinkedList();
		theList.insertFirst(22);
		theList.insertFirst(44);
		theList.insertFirst(66);
		theList.insertLast(11);
		theList.insertLast(33);
		theList.insertLast(55);
		theList.displayForward();
		theList.displayBackwrard();
		theList.deleteFirst();
		theList.deleteLast();
		theList.deleteKey(11);
		theList.displayForward();
		theList.insertAfter(22, 77);
		theList.insertAfter(33, 88);
		theList.displayForward();
	}
}


/*
List (first --> last): { 66 }{ 44 }{ 22 }{ 11 }{ 33 }{ 55 }
List (last --> first): { 55 }{ 33 }{ 11 }{ 22 }{ 44 }{ 66 }
List (first --> last): { 44 }{ 22 }{ 33 }
List (first --> last): { 44 }{ 22 }{ 77 }{ 33 }{ 88 }
*/
```


-----

##  Linear Search and Binary Search

```java
package algo.linearsearch;

public class App {

	public static void main(String[] args) {
		System.out.println(recursiveLinearSearch(new int[] {4, 48, 4, 28, 34, 76, 9, 3}, 0, 28));
		/*
		 index at: 0
		 index at: 1
		 index at: 2
		 3
		*/

		System.out.println(binarySearch(new int[] {1,2,3,4,7,9,12,18}, 12)); // 6
		System.out.println(recursiveBinarySearch(new int[] {1,2,3,4,7,9,12,18}, 0, 7, 9)); // 5
	}

	public static int linearSearch(int [] a, int x) {
		for(int i = 0; i < a.length; i++) {
			if(a[i] == x) {
				return i;
			}
		}

		return -1;
	}

	public static int recursiveLinearSearch(int [] a, int i, int x) {
		if( i > a.length - 1) { // if evaluates to true, x was not found in the array
			return -1;
		} else if (a[i] == x) {
			return i;
		} else {
			System.out.println("index at: " + i);
			return recursiveLinearSearch(a, i + 1, x);
		}
	}

	public static int binarySearch(int [] a, int x) {
		int p = 0;
		int r = a.length - 1;

		while(p <= r) {
			int q = (p + r)/ 2;
			if(x < a[q]) r = q - 1;
			else if (x > a[q]) p = q + 1;
			else return q;
		}

		return -1;
	}

	public static int recursiveBinarySearch(int [] a, int p, int r, int x) {
		int q = (p + r)/2;
		if (p > r) return -1;
		else if (x < a[q]) return recursiveBinarySearch(a, p, q - 1, x);
		else if(x > a[q]) return recursiveBinarySearch(a, q + 1, r, x);
		else return q;
	}
}

```


-----


## Selection Sort

```java
public class App {

	public static void main(String[] args) {
			int[] myArray = selectionSort(new int[] {9,8,3,13,87,12,99});
			for(int i = 0; i < myArray.length; i++) {
				System.out.println(myArray[i]);
			}

			/*
			  3
				8
				9
				12
				13
				87
				99
			 */
	}

	public static int [] selectionSort(int a[]) {
		for(int i = 0; i < a.length; i++) {
			int minimum = i;
			for(int j = i+1; j < a.length; j++) {
				if(a[j] < a[minimum]) { //i we find a smaller value
					minimum = j;
				}
			}
			int temp = a[i];
			a[i] = a[minimum];
			a[minimum] = temp;
		}
		return a;
	}
}

```

----

## Insertion Sort

```java
package insertionsort;

public class App {

	public static void main(String[] args) {
		int myArray[] = insertionSort(new int[] {9,8,99,110,8,87,637,8, 3, 13, 87, 12, 99});
		for(int i = 0; i < myArray.length; i++) {
			System.out.println(myArray[i]);
		}

		/*
		  9
			12
			13
			87
			87
			99
			99
			110
			637
		 */

	}

	public static int[] insertionSort(int [] a) {
		for(int i = 1; i < a.length; i++) {
			int element = a[i]; // element variable contains the data we intend on bringing over to the sorted area
			int j = i - 1; // j variable points to the index position of the last value in the sorted area

			while(j >= 0 && a[j] > element) {
				a[j+1] = a[j];
				j--;
			}
			a[j+1] = element;
		}

		return a;
	}

}

```

-----

## Merge Sort

```java
public class MergeSort {

	public static void sort(int inputArray[]) {
		sort(inputArray, 0, inputArray.length - 1);
	}

	public static void sort(int inputArray[], int start, int end) {
		if(end <= start) {
			return; // we're done traversing the array
		}

		int mid = (start + end)/ 2;
		sort(inputArray, start, mid); // sort left half
		sort(inputArray, mid + 1, end); // sort right half
		merge(inputArray, start, mid, end); // merge sorted results into the inputArray
	}

	public static void merge(int inputArray[], int start, int mid, int end) {
		int tempArray[] = new int [end - start + 1];

		// index counter for the left side of the array
		int leftSlot = start;

		// index counter for the right side of the array
		int rightSlot = mid + 1;

		int k = 0;

		while(leftSlot <= mid && rightSlot <= end) {
			if(inputArray[leftSlot] < inputArray[rightSlot]) {
				tempArray[k] = inputArray[leftSlot];
				leftSlot++;
			} else {
				tempArray[k] = inputArray[rightSlot];
				rightSlot++;
			}
			k++;
		}

		if(leftSlot <= mid) { // consider the right side done being sorted. Left must be sorted already
			while(leftSlot <= mid) {
				tempArray[k] = inputArray[leftSlot];
				leftSlot++;
				k++;
			}
		} else if(rightSlot <= end) {
			while(rightSlot <= end) {
				tempArray[k] = inputArray[rightSlot];
				rightSlot++;
				k++;
			}
		}

		// copy over the temp array into the appropriate slots of the inputArray
		for(int i = 0; i < tempArray.length; i++) {
			inputArray[start + i] = tempArray[i];
		}
	}
}


public class App {

	public static void main(String[] args) {
		int[] inputArray = { 9, 7, 3, 1 , 6, 3, 2, 6, 8 , 9, 2, 3 , 0};
		MergeSort sorter = new MergeSort();

		sorter.sort(inputArray);

		for(int i = 0; i < inputArray.length; i++) {
			System.out.println(inputArray[i]);
		}

		/*
		 	0
			1
			2
			2
			3
			3
			3
			6
			6
			7
			8
			9
			9
		 */

	}

}
```


----


## Quick Sort

```java
import java.util.Arrays;

public class App {

	public static void main(String[] args) {
		int[] inputArray = {12, 81, 74, 43, 1098, 0, 8, 92, 17, 754, 912, 0, 6, 4};
		quickSort(inputArray, 0, inputArray.length - 1);

		System.out.println(Arrays.toString(inputArray));
		// [0, 0, 4, 6, 8, 12, 17, 43, 74, 81, 92, 754, 912, 1098]
	}

	public static void quickSort(int [] inputArray, int start, int end) {
		if(start < end) {
			int pp = partition(inputArray, start, end); // give the index position of the correctly placed value in the array
			quickSort(inputArray, start, pp - 1); // sorts the left half of the range
			quickSort(inputArray, pp + 1, end); // sorts the right half of the range
		}
	}

	public static int partition(int [] inputArray, int start, int end) {
		int pivot = inputArray[end];

		// in the first iteration, i starts from -1
		int i = start - 1;
		for(int j = start; j <= end - 1; j++) {
			if(inputArray[j] <= pivot) {
				i++;
				// we are swapping below
				int ival = inputArray[i];
				int jval = inputArray[j];
				inputArray[i] = jval;
				inputArray[j] = ival;
			}
		}

		// put the pivot value in the correct slot next
		int ival = inputArray[i + 1];
		inputArray[end] = ival;
		inputArray[i + 1] = pivot; // here, pivot value is placed in the correct slot of the array.

		return i + 1;
	}

}

```
