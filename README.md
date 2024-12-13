student_marks_pr1.txt


def main():
    from collections import Counter

    all_students = {"Amit", "Priya", "Rahul", "Sneha", "Arjun", "Neha", "Karan", "Pooja", "Rohan", "Aarti"}
    marks = {"Amit": 85, "Priya": 78, "Rahul": 92, "Sneha": 85, "Arjun": 76, "Neha": 0, "Karan": 0, "Pooja": 85, "Rohan": 0}

    scores = [mark for mark in marks.values() if mark > 0]
    average_score = sum(scores) / len(scores)
    highest_score, lowest_score = max(scores), min(scores)
    absent_count = len(all_students) - len(marks)
    highest_frequency_marks = [mark for mark, freq in Counter(scores).items() if freq == max(Counter(scores).values())]

    print("Average score of class:", average_score)
    print("Highest score of class:", highest_score)
    print("Lowest score of class:", lowest_score)
    print("Count of students who were absent for the test:", absent_count)
    print("Marks with highest frequency:", highest_frequency_marks)

if __name__ == "__main__":
    main()


bank_balance_pr2&3.txt

bank_balance = 0

def dep(amnt):
    global bank_balance
    bank_balance += amnt
    return bank_balance

def wid(amnt):
    global bank_balance
    if bank_balance >= amnt:
        bank_balance -= amnt
        return bank_balance
    else:
        print("Not enough money to withdraw")

trans_log = input("Enter the transaction log: ")
print("Transaction log:", trans_log)

entry_list = trans_log.split(', ')
print("Entry list:", entry_list)

for entry in entry_list:
    sep_entrylist = entry.split(' ')
    op = sep_entrylist[0]
    amnt = int(sep_entrylist[1])

    if op == 'D':
        dep(amnt)
    elif op == 'W':
        wid(amnt)

print("Bank Balance:", bank_balance)



linear_sentinal_pr_4.txt



student_list=[10,40,45,67,89,34,56,78,73,90,1,37]

def linear_search(student_list,key):
    for i in range(len(student_list)):
        if student_list[i] == key:
            return i
    return -1

index = linear_search(student_list,40)
if index==-1:
    print("element not found")
else:
    print("element found at index(linear)", index)

def sentinal_search(student_list,key):
    last=student_list[-1]
    student_list[-1]=key
    i=0
    while student_list[i] != key:
        i += 1
    if i != len(student_list)-1:
        return i
    else:
        if last == key:
            return len(student_list) - 1
    return -1

index = sentinal_search(student_list,37)
if index==-1:
    print("element not found")
else:
    print("element found at index(sentinal)", index)



 binary_fib_seaech_pr5&6.txt

 def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return False

def fibonacci_search(arr, target):
    fib2, fib1 = 0, 1
    fibM = fib2 + fib1
    n = len(arr)

    while fibM < n:
        fib2, fib1 = fib1, fibM
        fibM = fib2 + fib1

    offset = -1

    while fibM > 1:
        i = min(offset + fib2, n - 1)

        if arr[i] < target:
            fibM, fib1, fib2 = fib1, fib2, fib1 - fib2
            offset = i
        elif arr[i] > target:
            fibM, fib1, fib2 = fib2, fib1 - fib2, fib2 - fib1
        else:
            return True

    return fib1 and offset + 1 < n and arr[offset + 1] == target

def main():
    roll_numbers = sorted([23, 45, 12, 67, 34, 89, 10, 56, 78, 90])
    search_roll = int(input("Enter roll number to search: "))
    print("Binary Search: Student attended training program:", binary_search(roll_numbers, search_roll))
    print("Fibonacci Search: Student attended training program:", fibonacci_search(roll_numbers, search_roll))

if __name__ == "__main__":
    main()

icecream_pr7.txt


#include <iostream>
using namespace std;

struct Node {
    int studentID;
    Node* next;
};

void insert(Node*& head, int studentID) {
    Node* newNode = new Node{studentID, head};
    head = newNode;
}

void display(Node* head) {
    while (head) {
        cout << head->studentID << " ";
        head = head->next;
    }
    cout << endl;
}

Node* intersection(Node* setA, Node* setB) {
    Node* result = nullptr;
    while (setA) {
        Node* tempB = setB;
        while (tempB) {
            if (setA->studentID == tempB->studentID) insert(result, setA->studentID);
            tempB = tempB->next;
        }
        setA = setA->next;
    }
    return result;
}

Node* unionSet(Node* setA, Node* setB) {
    Node* result = nullptr;
    while (setA) { insert(result, setA->studentID); setA = setA->next; }
    while (setB) {
        Node* temp = result;
        bool found = false;
        while (temp) {
            if (temp->studentID == setB->studentID) { found = true; break; }
            temp = temp->next;
        }
        if (!found) insert(result, setB->studentID);
        setB = setB->next;
    }
    return result;
}

int countNeither(Node* setA, Node* setB, int totalStudents) {
    int count = 0;
    for (int i = 1; i <= totalStudents; ++i) {
        bool inA = false, inB = false;
        Node* tempA = setA, * tempB = setB;
        while (tempA && !inA) if (tempA->studentID == i) inA = true, tempA = tempA->next;
        while (tempB && !inB) if (tempB->studentID == i) inB = true, tempB = tempB->next;
        if (!inA && !inB) ++count;
    }
    return count;
}

int main() {
    Node *setA = nullptr, *setB = nullptr;
    insert(setA, 1); insert(setA, 2); insert(setA, 3); insert(setA, 5);
    insert(setB, 3); insert(setB, 4); insert(setB, 5); insert(setB, 6);

    cout << "Set A (Vanilla Lovers): "; display(setA);
    cout << "Set B (Butterscotch Lovers): "; display(setB);

    cout << "Students who like both Vanilla and Butterscotch: "; 
    display(intersection(setA, setB));

    cout << "Students who like either Vanilla or Butterscotch or both: "; 
    display(unionSet(setA, setB));

    cout << "Number of students who like neither Vanilla nor Butterscotch: " 
         << countNeither(setA, setB, 6) << endl;

    return 0;
}


paranthises_pr8&10.txt

#include<iostream>
using namespace std;
#define size 30

int main() {
    char stk[size], exp[size], ans;
    int top;
    
    do {
        top = -1;
        cout << "Enter the expression\t";
        cin >> exp;
        
        for (int i = 0; exp[i] != '\0'; i++) {
            if (exp[i] == '(' || exp[i] == '[' || exp[i] == '{') {
                top++;
                stk[top] = exp[i];
            }
            else if (exp[i] == ')') {
                if (stk[top] == '(') {
                    top--;
                }
                else {
                    cout << "Given expression is not well parenthesized" << endl;
                    return 0;
                }
            }
            else if (exp[i] == ']') {
                if (stk[top] == '[') {
                    top--;
                }
                else {
                    cout << "Given expression is not well parenthesized" << endl;
                    return 0;
                }
            }
            else if (exp[i] == '}') {
                if (stk[top] == '{') {
                    top--;
                }
                else {
                    cout << "Given expression is not well parenthesized" << endl;
                    return 0;
                }
            }
        }
        
        if (top == -1) {
            cout << "Given Expression is well Parenthesized" << endl;
        }
        else {
            cout << "Given expression is not well parenthesized" << endl;
        }
        
        cout << "Do You Want to continue??\t";
        cin >> ans;
        
    } while (ans == 'y');
    
    return 0;
}



job_queue_pr9.txt

#include <iostream>
#define MAX 10
using namespace std;
struct queue
{       int data[MAX];
	int front,rear;
};
class Queue
{    struct queue q;
   public:
      Queue(){q.front=q.rear=-1;}
      int isempty();
      int isfull();
      void enqueue(int);
      int delqueue();
      void display();
};
int Queue::isempty()
{
	return(q.front==q.rear)?1:0;
}
int Queue::isfull()
{    return(q.rear==MAX-1)?1:0;}
void Queue::enqueue(int x)
{q.data[++q.rear]=x;}
int Queue::delqueue()
{return q.data[++q.front];}
void Queue::display()
{   int i;
    cout<<"\n";
    for(i=q.front+1;i<=q.rear;i++)
	     cout<<q.data[i]<<" ";
}
int main()
{      Queue obj;
	int ch,x;
	do{    cout<<"\n 1.Insert Job\n 2.Delete Job\n 3.Display\n 4.Exit\n Enter your choice : ";
	       cin>>ch;
	switch(ch)
	{  case 1: if (!obj.isfull())
		   {   cout<<"\n Enter data : \n";
			cin>>x;
			obj.enqueue(x);
			cout<<endl;
		   }
	          else
		      cout<< "Queue is overflow!!!\n\n";
	           break;
	   case 2: if(!obj.isempty())
			    cout<<"\n Deleted Element = "<<obj.delqueue()<<endl;
		    else
			{   cout<<"\n Queue is underflow!!!\n\n";  }
		    cout<<"\nRemaining Jobs : \n";
		    obj.display();
	           break;
	  case 3: if (!obj.isempty())
	        {  cout<<"\n Queue contains : \n";
		       obj.display();
	        }
	        else
		         cout<<"\n Queue is empty!!!\n\n";
	       break;
	  case 4: cout<<"\n Exiting Program.....";
        }
      }while(ch!=4);
return 0;
}





    

