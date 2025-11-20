# Quicksort - Linked Lists



```java
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Main.java to edit this template
 */
package inst_quicksort_linklists;
import java.util.Stack;

interface SortingAlgorithm {
    Node quickSort(Node head);
}

// Simple node for a singly linked list
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class RecursiveQuickSortLinkedList implements SortingAlgorithm {

    // QuickSort Entry Point
    public Node quickSort(Node head) {
        // Base Case
        if (head == null || head.next == null) {
            return head;
        }

        // Partition using head as pivot
        Node pivot = head;
        Node lessHead = null, lessTail = null;
        Node greaterHead = null, greaterTail = null;

        Node current = head.next;

        while (current != null) {
            if (current.data < pivot.data) {
                if (lessHead == null) lessHead = lessTail = current;
                else { lessTail.next = current; lessTail = current; }
            } else {
                if (greaterHead == null) greaterHead = greaterTail = current;
                else { greaterTail.next = current; greaterTail = current; }
            }
            current = current.next;
        }

        // Prevent accidental list cycles
        if (lessTail != null) lessTail.next = null;
        if (greaterTail != null) greaterTail.next = null;

        // Recursively sort sublists
        lessHead = quickSort(lessHead);
        greaterHead = quickSort(greaterHead);

        // Stitch together: less + pivot + greater
        return concatenate(lessHead, pivot, greaterHead);
    }

    // Helper: combine lists
    private Node concatenate(Node less, Node pivot, Node greater) {
        pivot.next = greater;

        if (less == null) return pivot;

        Node current = less;
        while (current.next != null) {
            current = current.next;
        }
        current.next = pivot;

        return less;
    }

    // Utility: print list
    public void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}



class IterativeQuickSortLinkedList implements SortingAlgorithm  {

    private static class Range {
        Node start, end;
        Range(Node s, Node e) { start = s; end = e; }
    }

    public Node quickSort(Node head) {

        if (head == null || head.next == null) return head;

        Stack<Range> stack = new Stack<>();
        stack.push(new Range(head, null)); // null end = process until null

        while (!stack.isEmpty()) {
            Range r = stack.pop();
            Node start = r.start;
            Node end = r.end;

            if (start == end || start == null) continue;

            // Partition
            Node pivot = start;
            Node lessH = null, lessT = null;
            Node greaterH = null, greaterT = null;

            Node curr = start.next;

            while (curr != end) {
                if (curr.data < pivot.data) {
                    if (lessH == null) lessH = lessT = curr;
                    else { lessT.next = curr; lessT = curr; }
                } else {
                    if (greaterH == null) greaterH = greaterT = curr;
                    else { greaterT.next = curr; greaterT = curr; }
                }
                curr = curr.next;
            }

            // Terminate lists
            if (lessT != null) lessT.next = null;
            if (greaterT != null) greaterT.next = end;

            // Stitch pivot into correct place
            pivot.next = greaterH;

            // Push new ranges to stack (reverse order so left processed first)
            if (greaterH != null) stack.push(new Range(greaterH, end));
            if (lessH != null) {
                stack.push(new Range(lessH, pivot));
            } else {
                start = pivot; // nothing smaller
            }

            // If this range was the whole list, update head
            if (r.start == head) head = (lessH != null ? lessH : pivot);
        }

        return head;
    }

    public void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}


public class Inst_quicksort_linklists {

    // Helper: build a linked list from an array
    public static Node buildList(int[] arr) {
        if (arr.length == 0) return null;
        Node head = new Node(arr[0]);
        Node curr = head;
        for (int i = 1; i < arr.length; i++) {
            curr.next = new Node(arr[i]);
            curr = curr.next;
        }
        return head;
    }

    // Helper: print list
    public static void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args)
    {
        int[] data = {8, 3, 7, 1, 9, 2, 6, 5};

        // ------------------------------------------------------
        // CHOICE VARIABLE
        // 1 = recursive quicksort
        // 2 = iterative quicksort
        // ------------------------------------------------------
        int choice = 1;     // <<< change this to 2 for iterative

        SortingAlgorithm sorter;

        if (choice == 1) {
            System.out.println("Running Recursive QuickSort...");
            sorter = new RecursiveQuickSortLinkedList();
        } else {
            System.out.println("Running Iterative QuickSort...");
            sorter = new IterativeQuickSortLinkedList();
        }

        // Build original list
        Node list = buildList(data);

        System.out.println("Original List:");
        printList(list);

        // Sort using selected algorithm
        Node sorted = sorter.quickSort(list);

        System.out.println("\nSorted List:");
        printList(sorted);
    }
    
}

```

