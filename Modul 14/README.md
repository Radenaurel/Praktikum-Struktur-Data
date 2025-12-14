<h1 align="center">Laporan Praktikum 
  
  Modul 14 <br> GRAPH </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori Modul 13
A. Konsep Dasar GRAPH


## Guided Modul 14

### soal 1

```go
 #include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Guided13.1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 

Program ini mengimplementasikan struktur data Multi-Linked List menggunakan bahasa C++, di mana terdapat hubungan hierarkis antara data parent dan data child. Struktur dasar dibentuk melalui dua struct berbeda yaitu ParentNode yang memiliki pointer childHead untuk menunjuk ke awal daftar anak, dan ChildNode sebagai elemen sub-list. Logika utama program terletak pada mekanisme penyisipan data, fungsi insertParent bekerja secara linear untuk menyambungkan simpul induk, sedangkan fungsi insertChild memiliki kompleksitas lebih tinggi karena harus melakukan pencarian  terlebih dahulu untuk menemukan simpul induk yang sesuai dengan parentInfo. Setelah induk ditemukan, simpul anak baru dialokasikan dan disambungkan ke akhir dari daftar anak milik induk tersebut. Visualisasi data dilakukan oleh prosedur printAll menggunakan teknik nested traversal, di mana program mencetak satu simpul induk, menelusuri seluruh anak yang dimilikinya hingga NULL, baru kemudian berpindah ke simpul induk berikutnya.

## Unguided Modul 14

### soal 1

```go
 #include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 
Program ini mengimplementasikan struktur data Multi-Linked List dengan skema Doubly Linked List yang diterapkan secara konsisten baik pada level parent maupun child. Struktur hierarkis dibentuk melalui struct elemen_list_induk yang tidak hanya menyimpan data integer dan pointer navigasi (, tetapi juga secara unik mewadahi struktur listanak di dalamnya, menciptakan relasi one-to-many di mana satu induk memiliki kontrol penuh atas daftar anaknya sendiri. Alur kerja utama dalam fungsi main mendemonstrasikan siklus hidup data: dimulai dengan inisialisasi list, dilanjutkan dengan alokasi dan penyisipan node induk bernilai 10, 20, dan 30 beserta node anak yang relevan anak 1-3 untuk induk 10, anak 4-5 untuk induk 20. Program juga menguji validitas manipulasi data melalui operasi penghapusan, spesifiknya menghapus anak pertama dari induk 10 dan menghapus induk terakhir yaitu node 30. Validasi akhir dilakukan oleh prosedur printInfo yang menjalankan mekanisme nested traversal penelusuran bersarang, di mana program menelusuri rantai induk satu per satu sembari mencetak sub-list anak yang terhubung pada setiap simpul induk tersebut.

### soal 2

```go
 #include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 2

penjelasan: 
Program ini mengimplementasikan struktur data Multi-Linked List dengan skema Doubly Linked List yang diterapkan secara konsisten baik pada level parent maupun child. Struktur hierarkis dibentuk melalui struct elemen_list_induk yang tidak hanya menyimpan data integer dan pointer navigasi (, tetapi juga secara unik mewadahi struktur listanak di dalamnya, menciptakan relasi one-to-many di mana satu induk memiliki kontrol penuh atas daftar anaknya sendiri. Alur kerja utama dalam fungsi main mendemonstrasikan siklus hidup data: dimulai dengan inisialisasi list, dilanjutkan dengan alokasi dan penyisipan node induk bernilai 10, 20, dan 30 beserta node anak yang relevan anak 1-3 untuk induk 10, anak 4-5 untuk induk 20. Program juga menguji validitas manipulasi data melalui operasi penghapusan, spesifiknya menghapus anak pertama dari induk 10 dan menghapus induk terakhir yaitu node 30. Validasi akhir dilakukan oleh prosedur printInfo yang menjalankan mekanisme nested traversal penelusuran bersarang, di mana program menelusuri rantai induk satu per satu sembari mencetak sub-list anak yang terhubung pada setiap simpul induk tersebut.

### soal 3

```go
 #include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 3

penjelasan: 
Program ini mengimplementasikan struktur data Multi-Linked List dengan skema Doubly Linked List yang diterapkan secara konsisten baik pada level parent maupun child. Struktur hierarkis dibentuk melalui struct elemen_list_induk yang tidak hanya menyimpan data integer dan pointer navigasi (, tetapi juga secara unik mewadahi struktur listanak di dalamnya, menciptakan relasi one-to-many di mana satu induk memiliki kontrol penuh atas daftar anaknya sendiri. Alur kerja utama dalam fungsi main mendemonstrasikan siklus hidup data: dimulai dengan inisialisasi list, dilanjutkan dengan alokasi dan penyisipan node induk bernilai 10, 20, dan 30 beserta node anak yang relevan anak 1-3 untuk induk 10, anak 4-5 untuk induk 20. Program juga menguji validitas manipulasi data melalui operasi penghapusan, spesifiknya menghapus anak pertama dari induk 10 dan menghapus induk terakhir yaitu node 30. Validasi akhir dilakukan oleh prosedur printInfo yang menjalankan mekanisme nested traversal penelusuran bersarang, di mana program menelusuri rantai induk satu per satu sembari mencetak sub-list anak yang terhubung pada setiap simpul induk tersebut.



