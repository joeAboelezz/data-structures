# Data Structures using C++
## Fork this repositry and update your readme file to including your name, id and year.

// Created by Dr. Ahmed Said on 07/03/2025.
// youssef ahmed kamal id=231006924
#include <iostream>

typedef int ElementType;

class Node {
public:
    Node() {
        next = nullptr;
        prev = nullptr;
    };
    ElementType data;
    Node* next;
    Node* prev;
};

typedef Node* Position;

class DoublyList {
private:
    Position head;
    Position tail;
    int counter;
public:
    DoublyList() {
        head = nullptr;
        tail = nullptr;
        counter = 0;
    }
    void MakeNull();
    Position First();
    Position End();
    Position Next(Position p);
    Position Previous(Position p);
    void InsertAtEnd(ElementType x);
    void InsertAtStart(ElementType x);
    void InsertAt(ElementType x, Position p);
    void InsertAfter(ElementType x, Position p);
    void InsertBefore(ElementType x, Position p);
    void InsertSorted(ElementType x);
    void Delete(Position p);
    Position Locate(int x);
    ElementType Retrieve(Position p);
    void PrintList();
    int Length();
};

void DoublyList::MakeNull() {
    while (head != nullptr) {
        Position temp = head;
        head = head->next;
        delete temp;
    }
    tail = nullptr;
    counter = 0;
}

Position DoublyList::First() {
    return head;
}

Position DoublyList::Next(Position p) {
    return (p == nullptr) ? nullptr : p->next;
}

Position DoublyList::Previous(Position p) {
    return (p == nullptr) ? nullptr : p->prev;
}

Position DoublyList::End() {
    return tail;
}

void DoublyList::InsertAtStart(ElementType x) {
    Position newNode = new Node();
    newNode->data = x;
    newNode->next = head;
    newNode->prev = nullptr;
    if (head != nullptr) head->prev = newNode;
    head = newNode;
    if (tail == nullptr) tail = head;
    counter++;
}

void DoublyList::InsertAtEnd(ElementType x) {
    Position newNode = new Node();
    newNode->data = x;
    newNode->next = nullptr;
    newNode->prev = tail;
    if (tail != nullptr) tail->next = newNode;
    tail = newNode;
    if (head == nullptr) head = tail;
    counter++;
}

void DoublyList::InsertAt(ElementType x, Position p) {
    if (p == nullptr) {
        InsertAtEnd(x);
    }
    else if (p == head) {
        InsertAtStart(x);
    }
    else {
        Position newNode = new Node();
        newNode->data = x;
        newNode->prev = p->prev;
        newNode->next = p;
        if (p->prev != nullptr) p->prev->next = newNode;
        p->prev = newNode;
        counter++;
    }
}

void DoublyList::InsertAfter(ElementType x, Position p) {
    if (p == nullptr) {
        InsertAtEnd(x);
    }
    else {
        Position newNode = new Node();
        newNode->data = x;
        newNode->next = p->next;
        newNode->prev = p;
        if (p->next != nullptr) p->next->prev = newNode;
        p->next = newNode;
        if (p == tail) tail = newNode;
        counter++;
    }
}

void DoublyList::InsertBefore(ElementType x, Position p) {
    InsertAt(x, p);
}

void DoublyList::InsertSorted(ElementType x) {
    Position newNode = new Node();
    newNode->data = x;
    if (head == nullptr || head->data >= x) {
        InsertAtStart(x);
        return;
    }
    Position temp = head;
    while (temp->next != nullptr && temp->next->data < x) {
        temp = temp->next;
    }
    InsertAfter(x, temp);
}

void DoublyList::Delete(Position p) {
    if (p == nullptr) return;
    if (p == tail) tail = p->prev;
    if (p == head) head = p->next;
    if (p->prev != nullptr) p->prev->next = p->next;
    if (p->next != nullptr) p->next->prev = p->prev;
    delete p;
    counter--;
}

Position DoublyList::Locate(ElementType x) {
    Position p = head;
    while (p != nullptr) {
        if (p->data == x) return p;
        p = p->next;
    }
    return nullptr;
}

ElementType DoublyList::Retrieve(Position p) {
    return (p == nullptr) ? NULL : p->data;
}

void DoublyList::PrintList() {
    Position p = head;
    while (p != nullptr) {
        std::cout << p->data << " -> ";
        p = p->next;
    }
    std::cout << "NULL\n";
}

int DoublyList::Length() {
    return counter;
}

int main() {
    DoublyList list;
    list.InsertSorted(3);
    list.InsertSorted(1);
    list.InsertSorted(4);
    list.InsertSorted(2);
    list.InsertSorted(5);
    list.PrintList();
    return 0;
}
