#include <iostream>
#include <string>
using namespace std;

enum PatientType {
    SERIOUS,
    NON_SERIOUS,
    GENERAL_CHECKUP
};

struct Patient {
    string name;
    PatientType type;
};

class PriorityQueue {
private:
    Patient patients[5];
    int front;
    int rear;
    int size;
public:
    PriorityQueue() {
        front = -1;
        rear = -1;
        size = 5; // Set the size of the queue
    }
bool isEmpty() {
 return front == -1;
    }
bool isFull() {
 return rear == size - 1;
    }
void enqueue(string name, PatientType type) {
  if (isFull()) {
   cout << "Queue is full. Cannot enqueue more patients." << endl;
      }
  Patient patient;
  patient.name = name;
  patient.type = type;
    rear++;
    patients[rear] = patient;
    if (front == -1) {
    front = 0;
    }
for (int i = rear; i > front; i--) {
 if (patients[i].type < patients[i - 1].type) 
   {
    swap(patients[i], patients[i - 1]);
    } else 
      break;
 }
}
void dequeue() {
  if (isEmpty()) {
    cout << "Queue is empty. No patients to dequeue." << endl;
       }
cout << "Dequeued: " << patients[front].name << endl;
        if (front == rear) {
            front = rear = -1;
        } else {
            front++;
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty" << endl;
            return;
        }

        cout << "Discharge order:" << endl;
        for (int i = front; i <= rear; i++) {
            cout << patients[i].name << endl;
        }
    }
};

int main() {
    int ch;
    PriorityQueue p;
    string name;
    int typeInt;

    while (true) {
        cout << "-----Welcome to the hospital-----\n";
        cout << "What do you want?\n";
        cout << "1. Register a patient\n";
        cout << "2. Discharge a patient\n";
        cout << "3. Display discharge order\n";
        cout << "4. Exit\n";

        cin >> ch;

        switch (ch) {
            case 1:
                cout << "Enter the name of the patient: ";
                cin >> name;
                cout << "Enter the type of patient (0 - SERIOUS, 1 - NON_SERIOUS, 2 - GENERAL_CHECKUP): ";
                cin >> typeInt;

                if (typeInt < 0 || typeInt > 2) {
                    cout << "Invalid patient type. Please enter a valid type." << endl;
                    break;
                }

                p.enqueue(name, static_cast<PatientType>(typeInt));
                cout << "Patient registered in the hospital." << endl;
                break;

            case 2:
                p.dequeue();
                break;

            case 3:
                p.display();
                break;

            case 4:
                cout << "Thank you for using the hospital system." << endl;
                exit(0);

            default:
                cout << "Invalid choice. Please enter a valid option." << endl;
        }
    }

    return 0;
}