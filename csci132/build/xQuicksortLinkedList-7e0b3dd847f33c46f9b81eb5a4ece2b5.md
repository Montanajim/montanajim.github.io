# Quicksort - Linked Lists

Annotated

```java
/*
 * Quick Sort using Linked Lists
 * By James Goudy
 *
 * This program shows TWO different versions of QuickSort
 * for a singly linked list:
 *   1) A recursive version
 *   2) An iterative (loop-based) version that uses a Stack
 *
 * In main(), you can choose which version to run.
 */

package inst_quicksort_linklists;

import java.util.Stack;

// -----------------------------------------------------
// SortingAlgorithm interface
// -----------------------------------------------------
// An interface is like a "contract" that says:
// "Any class that implements me MUST have this method."
// Here, any sorting class must have a quickSort() method
// that takes the head of a linked list and returns
// the (new) head of the sorted list.
// -----------------------------------------------------
interface SortingAlgorithm {

    Node quickSort(Node head);
}

// -----------------------------------------------------
// Node class: a simple node for a singly linked list
// -----------------------------------------------------
// Each Node holds one integer (data) and a reference
// (pointer) to the next Node in the list.
// If next == null, this is the last node in the list.
// -----------------------------------------------------
class Node {

    int data;   // the value stored in this node
    Node next;  // reference to the next node in the list

    Node(int data)
    {
        this.data = data;
        this.next = null;
    }
}

// -----------------------------------------------------
// RecursiveQuickSortLinkedList
// -----------------------------------------------------
// This class uses a RECURSIVE version of QuickSort.
//
// Basic idea of QuickSort on a linked list:
// 1) Choose a pivot (here: the first node).
// 2) Split the list into:
//    - nodes with values LESS than the pivot
//    - nodes with values GREATER or EQUAL to the pivot
// 3) Recursively sort the two smaller lists.
// 4) Connect: less list + pivot + greater list
// -----------------------------------------------------
class RecursiveQuickSortLinkedList implements SortingAlgorithm {

    // Entry point for recursive QuickSort
    public Node quickSort(Node head)
    {
        // Base Case:
        // If the list is empty (head == null)
        // OR has only one element (head.next == null),
        // then it is already sorted.
        if (head == null || head.next == null) {
            return head;
        }

        // Use the first node as the pivot
        Node pivot = head;

        // These will be the heads and tails of two new lists:
        //  - less: nodes with data < pivot.data
        //  - greater: nodes with data >= pivot.data
        Node lessHead = null, lessTail = null;
        Node greaterHead = null, greaterTail = null;

        // Start from the node after the pivot
        Node current = head.next;

        // -------------------------------------------------
        // Partition loop:
        // Walk through the list, and put each node into
        // either the "less" list or the "greater" list.
        // -------------------------------------------------
        while (current != null) {
            if (current.data < pivot.data) {
                // Goes into the "less" list
                if (lessHead == null) {
                    // First node in the less list
                    lessHead = lessTail = current;
                } else {
                    // Append to the end of the less list
                    lessTail.next = current;
                    lessTail = current;
                }
            } else {
                // Goes into the "greater" list
                if (greaterHead == null) {
                    // First node in the greater list
                    greaterHead = greaterTail = current;
                } else {
                    // Append to the end of the greater list
                    greaterTail.next = current;
                    greaterTail = current;
                }
            }
            // Move to the next node in the original list
            current = current.next;
        }

        // -------------------------------------------------
        // Important cleanup step:
        // Make sure the less and greater lists have
        // proper endings (tails point to null).
        // This helps prevent accidental "cycles" in the list.
        // -------------------------------------------------
        if (lessTail != null) {
            lessTail.next = null;
        }
        if (greaterTail != null) {
            greaterTail.next = null;
        }

        // Recursively sort the two sublists:
        //  - lessHead: all nodes < pivot
        //  - greaterHead: all nodes >= pivot
        lessHead = quickSort(lessHead);
        greaterHead = quickSort(greaterHead);

        // Finally, stitch everything together:
        // less list + pivot + greater list
        return concatenate(lessHead, pivot, greaterHead);
    }

    // -----------------------------------------------------
    // concatenate()
    // -----------------------------------------------------
    // This helper method connects three pieces:
    // 1) less list (may be null)
    // 2) the pivot node (single node)
    // 3) greater list (may be null)
    //
    // Returns the head of the new combined list.
    // -----------------------------------------------------
    private Node concatenate(Node less, Node pivot, Node greater)
    {
        // Pivot should point to the start of the greater list
        pivot.next = greater;

        // If there is no "less" list, pivot is the new head
        if (less == null) {
            return pivot;
        }

        // Otherwise, walk to the end of the less list
        Node current = less;
        while (current.next != null) {
            current = current.next;
        }

        // Attach pivot (and greater) to the end of less
        current.next = pivot;

        // The head of the combined list is still "less"
        return less;
    }

    // -----------------------------------------------------
    // printList()
    // -----------------------------------------------------
    // Utility method to print the linked list in a friendly
    // format like: 8 -> 3 -> 7 -> null
    // -----------------------------------------------------
    public void printList(Node head)
    {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}

// ---------------------------------------------------------
// IterativeQuickSortLinkedList
// ---------------------------------------------------------
// This class uses an ITERATIVE version of QuickSort.
// Instead of using recursion, we use a Stack to keep
// track of which part (range) of the list we still
// need to process.
// ---------------------------------------------------------
class IterativeQuickSortLinkedList implements SortingAlgorithm {

    // -----------------------------------------------------
    // Range class:
    // A small helper class that stores a "sub-list" using
    // two pointers:
    //   start: first node in the range
    //   end:   one past the last node (EXCLUSIVE)
    //
    // The range is [start, end), meaning:
    //   start is included, end is NOT included.
    // -----------------------------------------------------
    private static class Range {
        Node start, end; // end is EXCLUSIVE
        Range(Node s, Node e) {
            start = s;
            end   = e;
        }
    }

    @Override
    public Node quickSort(Node head) {

        // Base case: empty or single-node list is already sorted
        if (head == null || head.next == null) {
            return head;
        }

        // -------------------------------------------------
        // Use a Stack to store the ranges we need to sort.
        // We start with the entire list: [head, null)
        // (null means "go all the way to the end").
        // -------------------------------------------------
        Stack<Range> stack = new Stack<>();
        stack.push(new Range(head, null)); // whole list: [head, null)

        // -------------------------------------------------
        // While there are still ranges to process
        // -------------------------------------------------
        while (!stack.isEmpty()) {
            Range r = stack.pop();
            Node start = r.start;
            Node end   = r.end;

            // If the range has 0 or 1 elements, it is already sorted.
            // Conditions:
            //  - start == null: empty
            //  - start == end: empty
            //  - start.next == end: exactly one element
            if (start == null || start == end || start.next == end) {
                continue;
            }

            // ---- Partition [start, end) around pivot = start ----
            Node pivot = start;
            Node lessH = null, lessT = null;        // "less than pivot" list
            Node greaterH = null, greaterT = null;  // "greater or equal" list

            // Start from the node after the pivot
            Node curr = pivot.next;

            // Walk through the range [pivot.next, end)
            while (curr != end) {
                Node next = curr.next; // Save next node before re-linking

                if (curr.data < pivot.data) {
                    // Goes in the "less" list
                    if (lessH == null) {
                        lessH = lessT = curr;
                    } else {
                        lessT.next = curr;
                        lessT = curr;
                    }
                } else {
                    // Goes in the "greater or equal" list
                    if (greaterH == null) {
                        greaterH = greaterT = curr;
                    } else {
                        greaterT.next = curr;
                        greaterT = curr;
                    }
                }

                // Move to the next node in the original range
                curr = next;
            }

            // ---- Re-link the nodes in sorted order within this range ----
            // We want: less list -> pivot -> greater list -> end

            // Attach pivot AFTER less list (if it exists)
            if (lessT != null) {
                lessT.next = pivot;
            }

            // Pivot should point to the start of the greater list
            pivot.next = greaterH;

            // If there is a greater list, its tail should point to end
            if (greaterT != null) {
                greaterT.next = end;
            } else {
                // No greater list: pivot should point directly to end
                pivot.next = end;
            }

            // newStart is the first node in this now-partially-sorted range
            Node newStart = (lessH != null) ? lessH : pivot;

            // ---- Fix list head or previous pointer ----
            // If this range started at the overall head of the list,
            // then we need to update the head.
            if (start == head) {
                head = newStart;
            } else {
                // Otherwise, find the node whose next was 'start'
                // and make it point to newStart.
                Node prev = head;
                while (prev != null && prev.next != start) {
                    prev = prev.next;
                }
                if (prev != null) {
                    prev.next = newStart;
                }
            }

            // ---- Push the two new subranges onto the stack ----
            // Right subrange: [pivot.next, end)
            if (pivot.next != null && pivot.next != end) {
                stack.push(new Range(pivot.next, end));
            }

            // Left subrange: [newStart, pivot)
            if (newStart != pivot) {
                stack.push(new Range(newStart, pivot));
            }
        }

        // When the stack is empty, everything is sorted
        return head;
    }

    // Utility: print list (same idea as above)
    public void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}

// ---------------------------------------------------------
// Inst_quicksort_linklists (Main Class)
// ---------------------------------------------------------
// This is the class with the main() method.
// It builds a sample linked list, lets you choose which
// QuickSort version to use (recursive or iterative),
// and then prints the original and sorted lists.
// ---------------------------------------------------------
public class Inst_quicksort_linklists {

    // -----------------------------------------------------
    // Helper: buildList()
    // -----------------------------------------------------
    // Takes a regular int[] array and builds a linked list
    // with the same values in the same order.
    // Returns the head of that new linked list.
    // -----------------------------------------------------
    private static Node buildList(int[] arr)
    {
        if (arr.length == 0) {
            return null;
        }

        // First node becomes the head
        Node head = new Node(arr[0]);
        Node curr = head;

        // Attach the rest of the nodes
        for (int i = 1; i < arr.length; i++) {
            curr.next = new Node(arr[i]);
            curr = curr.next;
        }

        return head;
    }

    // -----------------------------------------------------
    // Helper: printList()
    // -----------------------------------------------------
    // Another simple print method for convenience.
    // -----------------------------------------------------
    private static void printList(Node head)
    {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args)
    {
        // Sample data to be sorted
        int[] data = {8, 3, 7, 1, 9, 2, 6, 5};

        // --------------------------------------------------
        // CHOICE VARIABLE
        // --------------------------------------------------
        // 1 = use the RECURSIVE QuickSort
        // any other value = use the ITERATIVE QuickSort
        //
        // Try changing this to 1 and 2 and see how both
        // versions behave with the same data.
        // --------------------------------------------------
        int choice = 10;     // <<< change this to 1 for recursive, 2 for iterative

        SortingAlgorithm sorter;

        // Decide which sorting algorithm to use
        if (choice == 1) {
            System.out.println("Running Recursive QuickSort...");
            sorter = new RecursiveQuickSortLinkedList();
        } else {
            System.out.println("Running Iterative QuickSort...");
            sorter = new IterativeQuickSortLinkedList();
        }

        // Build the original linked list from the array
        Node list = buildList(data);

        System.out.println("Original List:");
        printList(list);

        // Sort the list using the selected algorithm
        Node sorted = sorter.quickSort(list);

        System.out.println("\nSorted List:");
        printList(sorted);
    }

}

```





Non Annotated

```java
/*

Quick Sort using Linked Lists
By James Goudy

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

    Node(int data)
    {
        this.data = data;
        this.next = null;
    }
}

class RecursiveQuickSortLinkedList implements SortingAlgorithm {

    // QuickSort Entry Point
    public Node quickSort(Node head)
    {
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
                if (lessHead == null) {
                    lessHead = lessTail = current;
                } else {
                    lessTail.next = current;
                    lessTail = current;
                }
            } else {
                if (greaterHead == null) {
                    greaterHead = greaterTail = current;
                } else {
                    greaterTail.next = current;
                    greaterTail = current;
                }
            }
            current = current.next;
        }

        // Prevent accidental list cycles
        if (lessTail != null) {
            lessTail.next = null;
        }
        if (greaterTail != null) {
            greaterTail.next = null;
        }

        // Recursively sort sublists
        lessHead = quickSort(lessHead);
        greaterHead = quickSort(greaterHead);

        // Stitch together: less + pivot + greater
        return concatenate(lessHead, pivot, greaterHead);
    }

    // Helper: combine lists
    private Node concatenate(Node less, Node pivot, Node greater)
    {
        pivot.next = greater;

        if (less == null) {
            return pivot;
        }

        Node current = less;
        while (current.next != null) {
            current = current.next;
        }
        current.next = pivot;

        return less;
    }

    // Utility: print list
    public void printList(Node head)
    {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}


class IterativeQuickSortLinkedList implements SortingAlgorithm {

    private static class Range {
        Node start, end; // end is EXCLUSIVE
        Range(Node s, Node e) {
            start = s;
            end   = e;
        }
    }

    @Override
    public Node quickSort(Node head) {

        if (head == null || head.next == null) {
            return head;
        }

        Stack<Range> stack = new Stack<>();
        stack.push(new Range(head, null)); // whole list: [head, null)

        while (!stack.isEmpty()) {
            Range r = stack.pop();
            Node start = r.start;
            Node end   = r.end;

            // 0 or 1 element in this range
            if (start == null || start == end || start.next == end) {
                continue;
            }

            // ---- Partition [start, end) around pivot = start ----
            Node pivot = start;
            Node lessH = null, lessT = null;
            Node greaterH = null, greaterT = null;

            Node curr = pivot.next;

            while (curr != end) {
                Node next = curr.next; // save before re-linking

                if (curr.data < pivot.data) {
                    if (lessH == null) {
                        lessH = lessT = curr;
                    } else {
                        lessT.next = curr;
                        lessT = curr;
                    }
                } else {
                    if (greaterH == null) {
                        greaterH = greaterT = curr;
                    } else {
                        greaterT.next = curr;
                        greaterT = curr;
                    }
                }
                curr = next;
            }

            // ---- Re-link: less -> pivot -> greater -> end ----
            if (lessT != null) {
                lessT.next = pivot;
            }
            pivot.next = greaterH;
            if (greaterT != null) {
                greaterT.next = end;
            } else {
                // no greater list
                pivot.next = end;
            }

            Node newStart = (lessH != null) ? lessH : pivot;

            // ---- Fix list head or previous pointer ----
            if (start == head) {
                head = newStart;
            } else {
                // find node whose next was 'start' and re-point it
                Node prev = head;
                while (prev != null && prev.next != start) {
                    prev = prev.next;
                }
                if (prev != null) {
                    prev.next = newStart;
                }
            }

            // ---- Push subranges: right then left ----
            // Right: [pivot.next, end)
            if (pivot.next != null && pivot.next != end) {
                stack.push(new Range(pivot.next, end));
            }
            // Left: [newStart, pivot)
            if (newStart != pivot) {
                stack.push(new Range(newStart, pivot));
            }
        }

        return head;
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



public class Inst_quicksort_linklists {

    // Helper: build a linked list from an array
    private static Node buildList(int[] arr)
    {
        if (arr.length == 0) {
            return null;
        }
        Node head = new Node(arr[0]);
        Node curr = head;
        for (int i = 1; i < arr.length; i++) {
            curr.next = new Node(arr[i]);
            curr = curr.next;
        }
        return head;
    }

    // Helper: print list
    private static void printList(Node head)
    {
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
        int choice = 10;     // <<< change this to 2 for iterative

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

