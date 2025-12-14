<h1 align="center">Laporan Praktikum 
  
  Modul 14 <br> GRAPH </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori Modul 13
A. Konsep Dasar GRAPH

Graph adalah struktur data non-linier yang merepresentasikan hubungan antar objek, terdiri dari himpunan tidak kosong atau sering di sebut node dan garis penghubung juga sering di sebut edge, yang secara formal dinotasikan sebagai G(V, E). Berdasarkan orientasi arah pada sisinya, graph diklasifikasikan menjadi Directed Graph atau graph berarah di mana hubungan memiliki tujuan spesifik, dan Undirected Graph atau juga graph tidak berarah di mana hubungan bersifat timbal balik. Selain arah, konsep fundamental lainnya meliputi weighted graph atau graph berbobot untuk merepresentasikan nilai seperti jarak, serta adjacency (ketetanggaan) yang menandakan hubungan langsung antara dua node melalui sebuah edge.Dalam implementasi pemrograman, graph umumnya direpresentasikan menggunakan Matriks Ketetanggaan atau Multi Linked List, di mana penggunaan Linked List lebih diutamakan dalam modul ini karena sifatnya yang dinamis dan efisien memori. Untuk memproses data di dalamnya, digunakan metode penelusuran traversal utama yaitu Breadth First Search (BFS) yang menelusuri graph secara melebar menggunakan struktur Queue, dan Depth First Search (DFS) yang menelusuri secara mendalam menggunakan struktur Stack. Pemahaman tentang representasi dan algoritma penelusuran ini menjadi dasar untuk aplikasi lanjutan seperti pencarian jalur terpendek atau Topological Sort.

## Guided Modul 14

### soal 1

```go
#include <iostream>
#include <queue>
#include <stack>

using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << "Node " << P->info << " terhubung dengan: ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

int main()
{
    Graph G;
    CreateGraph(G);
    InsertNode(G, 'A');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph (Adjacency List) ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Guided13.1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 

Program ini mengimplementasikan struktur data Undirected Graph atau sering di sebut graf tak berarah menggunakan bahasa C++ dengan representasi memori Adjacency List. Struktur dasar dibentuk melalui dua struct utama, yaitu ElmNode sebagai simpul yang memiliki pointer firstEdge untuk menunjuk ke senarai sisi, dan ElmEdge sebagai elemen penghubung yang menyimpan alamat simpul tujuan. Mekanisme manipulasi data mencakup fungsi InsertNode yang menambahkan simpul baru ke awal senarai, serta prosedur ConnectNode yang membangun relasi dua arah antar simpul dengan mengalokasikan sisi baru pada daftar tetangga kedua belah pihak. Visualisasi dan penelusuran graf difasilitasi oleh dua algoritma pencarian: prosedur PrintDFS menerapkan pendekatan rekursif untuk menelusuri graf secara mendalam dikenal Depth First Search (DFS), sedangkan prosedur PrintBFS memanfaatkan struktur data Queue dari pustaka standar untuk melakukan penelusuran melebar dikenal Breadth First Search (BFS), secara iteratif dari simpul awal ke seluruh tetangga yang terjangkau.

## Unguided Modul 14

### soal 1

```go
#include <iostream>
using namespace std;

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;        
    adrEdge firstEdge;  
    adrNode Next;       
};

struct ElmEdge {
    adrNode Node;       
    adrEdge Next;       
};

struct Graph {
    adrNode first;      
};


void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode AlokasiNode(infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->Next = NULL;
    return P;
}

adrEdge AlokasiEdge(adrNode Tujuan) {
    adrEdge E = new ElmEdge;
    E->Node = Tujuan;
    E->Next = NULL;
    return E;
}

void InsertNode(Graph &G, infoGraph X) {
    adrNode P = AlokasiNode(X);
    
    if (G.first == NULL) {
        G.first = P;
    } else {
        adrNode Q = G.first;
        while (Q->Next != NULL) {
            Q = Q->Next;
        }
        Q->Next = P;
    }
}

adrNode FindNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->Next;
    }
    return NULL;
}

void ConnectNode(adrNode N1, adrNode N2) {
    if (N1 != NULL && N2 != NULL) {
        adrEdge E1 = AlokasiEdge(N2);
        E1->Next = N1->firstEdge;
        N1->firstEdge = E1;

        adrEdge E2 = AlokasiEdge(N1);
        E2->Next = N2->firstEdge;
        N2->firstEdge = E2;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        cout << "Node " << P->info << " terhubung dengan: ";
        
        adrEdge E = P->firstEdge;
        if (E == NULL) {
            cout << "(tidak ada)";
        }
        while (E != NULL) {
            cout << E->Node->info;
            if (E->Next != NULL) cout << ", ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}


int main() {
    Graph G;
    CreateGraph(G);

    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    InsertNode(G, 'F');
    InsertNode(G, 'G');
    InsertNode(G, 'H');

    adrNode A = FindNode(G, 'A');
    adrNode B = FindNode(G, 'B');
    adrNode C = FindNode(G, 'C');
    adrNode D = FindNode(G, 'D');
    adrNode E = FindNode(G, 'E');
    adrNode F = FindNode(G, 'F');
    adrNode G_node = FindNode(G, 'G');
    adrNode H = FindNode(G, 'H');

    ConnectNode(A, B);
    ConnectNode(A, C);

    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, G_node);

    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(G_node, H);

    cout << "=== REPRESENTASI GRAPH (Undirected) ===" << endl;
    PrintInfoGraph(G);

    return 0;
}

```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 
Program ini mengimplementasikan struktur data Undirected Graph atau Graph Tak Berarah menggunakan bahasa C++ dengan representasi memori Adjacency List. Struktur dasar dibentuk melalui dua struct utama, yaitu ElmNode sebagai simpul  yang menyimpan informasi data dan memiliki pointer firstEdge untuk menunjuk ke senarai sisi, serta ElmEdge sebagai elemen penghubung yang menyimpan alamat simpul tujuan. Mekanisme pembangunan graf dilakukan oleh fungsi InsertNode yang menambahkan simpul baru ke akhir senarai utama, sedangkan relasi antar simpul dibangun oleh prosedur ConnectNode. Prosedur ini bekerja dengan menciptakan hubungan timbal balik yaitu 2 arah, di mana edge baru dialokasikan dan disisipkan ke awal daftar tetangga pada kedua simpul yang terlibat. Visualisasi data dilakukan oleh prosedur PrintInfoGraph menggunakan teknik nested traversal, yang menelusuri setiap simpul induk dan mencetak seluruh simpul tetangga yang terhubung dengannya.

### soal 2

```go
#include <iostream>
using namespace std;

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;        
    adrEdge firstEdge;  
    adrNode Next;       
};

struct ElmEdge {
    adrNode Node;       
    adrEdge Next;       
};

struct Graph {
    adrNode first;     
};


void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode AlokasiNode(infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;    
    P->firstEdge = NULL;
    P->Next = NULL;
    return P;
}

adrEdge AlokasiEdge(adrNode Tujuan) {
    adrEdge E = new ElmEdge;
    E->Node = Tujuan;
    E->Next = NULL;
    return E;
}

void InsertNode(Graph &G, infoGraph X) {
    adrNode P = AlokasiNode(X);
    
    if (G.first == NULL) {
        G.first = P;
    } else {
        adrNode Q = G.first;
        while (Q->Next != NULL) {
            Q = Q->Next;
        }
        Q->Next = P;
    }
}

adrNode FindNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->Next;
    }
    return NULL;
}

void ConnectNode(adrNode N1, adrNode N2) {
    if (N1 != NULL && N2 != NULL) {
        adrEdge E1 = AlokasiEdge(N2);
        E1->Next = N1->firstEdge;
        N1->firstEdge = E1;

        adrEdge E2 = AlokasiEdge(N1);
        E2->Next = N2->firstEdge;
        N2->firstEdge = E2;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        cout << "Node " << P->info << " terhubung dengan: ";
        
        adrEdge E = P->firstEdge;
        if (E == NULL) {
            cout << "(tidak ada)";
        }
        while (E != NULL) {
            cout << E->Node->info;
            if (E->Next != NULL) cout << ", ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}


void ResetVisited(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    if (N == NULL) return;

    N->visited = 1;
    cout << N->info << " ";


    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (E->Node->visited == 0) {
            PrintDFS(G, E->Node);
        }
        E = E->Next;
    }
}


int main() {
    Graph G;
    CreateGraph(G);

    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    InsertNode(G, 'F');
    InsertNode(G, 'G');
    InsertNode(G, 'H');

    adrNode A = FindNode(G, 'A');
    adrNode B = FindNode(G, 'B');
    adrNode C = FindNode(G, 'C');
    adrNode D = FindNode(G, 'D');
    adrNode E = FindNode(G, 'E');
    adrNode F = FindNode(G, 'F');
    adrNode G_node = FindNode(G, 'G');
    adrNode H = FindNode(G, 'H');

    ConnectNode(A, B);
    ConnectNode(A, C);

    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, G_node);

    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(G_node, H);

    cout << "=== INFORMASI GRAPH  ===" << endl;
    PrintInfoGraph(G);
    cout << endl;

    ResetVisited(G); 
    
    cout << "=== HASIL PENELUSURAN DFS ===" << endl;
    PrintDFS(G, A); 
    cout << endl;

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 2

penjelasan: 
Program ini mengimplementasikan struktur data Undirected Graph atau sering disebut Graph Tak Berarah menggunakan bahasa C++ dengan representasi memori Adjacency List. Struktur dasar dibentuk melalui dua struct utama, yaitu ElmNode sebagai simpul yang memiliki atribut visited untuk penandaan penelusuran dan pointer firstEdge untuk menunjuk ke senarai sisi, serta ElmEdge sebagai elemen penghubung yang menyimpan alamat simpul tujuan. Mekanisme manipulasi data mencakup fungsi InsertNode yang menambahkan simpul baru ke akhir senarai utama guna mempertahankan urutan penyisipan, sedangkan relasi antar simpul dibangun oleh prosedur ConnectNode yang menciptakan hubungan timbal balik yaitu dua arah dengan menyisipkan sisi baru ke awal daftar tetangga pada kedua simpul yang terlibat. Visualisasi dan penelusuran graf difasilitasi oleh prosedur PrintInfoGraph untuk menampilkan topologi jaringan, serta prosedur PrintDFS yang menerapkan algoritma rekursif untuk melakukan penelusuran mendalam (DFS) dari simpul awal hingga seluruh simpul yang terhubung dikunjungi.

### soal 3

```go
#include <iostream>
#include <queue> 

using namespace std;
typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;        
    adrEdge firstEdge;  
    adrNode Next;       
};

struct ElmEdge {
    adrNode Node;       
    adrEdge Next;       
};

struct Graph {
    adrNode first;      
};

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode AlokasiNode(infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;     
    P->firstEdge = NULL;
    P->Next = NULL;
    return P;
}

adrEdge AlokasiEdge(adrNode Tujuan) {
    adrEdge E = new ElmEdge;
    E->Node = Tujuan;
    E->Next = NULL;
    return E;
}

void InsertNode(Graph &G, infoGraph X) {
    adrNode P = AlokasiNode(X);
    
    if (G.first == NULL) {
        G.first = P;
    } else {
        adrNode Q = G.first;
        while (Q->Next != NULL) {
            Q = Q->Next;
        }
        Q->Next = P;
    }
}

adrNode FindNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->Next;
    }
    return NULL;
}

void ConnectNode(adrNode N1, adrNode N2) {
    if (N1 != NULL && N2 != NULL) {
        adrEdge E1 = AlokasiEdge(N2);
        E1->Next = N1->firstEdge;
        N1->firstEdge = E1;
        adrEdge E2 = AlokasiEdge(N1);
        E2->Next = N2->firstEdge;
        N2->firstEdge = E2;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        cout << "Node " << P->info << " terhubung dengan: ";
        
        adrEdge E = P->firstEdge;
        if (E == NULL) {
            cout << "(tidak ada)";
        }
        while (E != NULL) {
            cout << E->Node->info;
            if (E->Next != NULL) cout << ", ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}

void ResetVisited(Graph G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    if (N == NULL) return;

    N->visited = 1;         
    cout << N->info << " "; 

    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (E->Node->visited == 0) {
            PrintDFS(G, E->Node); 
        }
        E = E->Next;
    }
}

void PrintBFS(Graph G, adrNode N) {
    if (N == NULL) return;

    queue<adrNode> Q; 

    Q.push(N);
    N->visited = 1;

    while (!Q.empty()) {
        adrNode current = Q.front();
        Q.pop();
        cout << current->info << " ";
        adrEdge E = current->firstEdge;
        while (E != NULL) {
            if (E->Node->visited == 0) {
                E->Node->visited = 1;
                Q.push(E->Node);
            }
            E = E->Next;
        }
    }
}


int main() {
    Graph G;
    CreateGraph(G);
    InsertNode(G, 'A'); InsertNode(G, 'B'); InsertNode(G, 'C');
    InsertNode(G, 'D'); InsertNode(G, 'E'); InsertNode(G, 'F');
    InsertNode(G, 'G'); InsertNode(G, 'H');

    adrNode A = FindNode(G, 'A'); adrNode B = FindNode(G, 'B');
    adrNode C = FindNode(G, 'C'); adrNode D = FindNode(G, 'D');
    adrNode E = FindNode(G, 'E'); adrNode F = FindNode(G, 'F');
    adrNode G_node = FindNode(G, 'G'); adrNode H = FindNode(G, 'H');

    ConnectNode(A, B); ConnectNode(A, C);
    ConnectNode(B, D); ConnectNode(B, E);
    ConnectNode(C, F); ConnectNode(C, G_node);
    ConnectNode(D, H); ConnectNode(E, H);
    ConnectNode(F, H); ConnectNode(G_node, H);


    cout << "=== INFORMASI GRAPH ===" << endl;
    PrintInfoGraph(G);
    cout << endl;

    ResetVisited(G); 
    cout << "=== HASIL DFS  ===" << endl;
    PrintDFS(G, A); 
    cout << endl << endl;

    ResetVisited(G); 
    cout << "=== HASIL BFS  ===" << endl;
    PrintBFS(G, A); 
    cout << endl;

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output13/Unguided13.1.png)
> Berikut SS VS Code dari Program Soal No 3

penjelasan: 
Program ini mengimplementasikan struktur data Undirected Graph atau sering disebut Graph Tak Berarah menggunakan bahasa C++ dengan representasi memori Adjacency List. Struktur dasar dibentuk melalui dua struct utama, yaitu ElmNode sebagai simpul yang memiliki atribut visited untuk penandaan traversal dan pointer firstEdge untuk menunjuk ke senarai sisi, serta ElmEdge sebagai elemen penghubung yang menyimpan alamat simpul tujuan. Mekanisme manipulasi data mencakup fungsi InsertNode yang menambahkan simpul baru ke akhir senarai utama guna menjaga urutan input, sedangkan relasi antar simpul dibangun oleh prosedur ConnectNode yang menciptakan hubungan timbal balik dengan menyisipkan sisi baru ke awal daftar tetangga pada kedua simpul yang terlibat. Visualisasi dan penelusuran graf difasilitasi oleh dua algoritma pencarian utama yaitu prosedur PrintDFS menerapkan metode rekursif untuk melakukan penelusuran mendalam (DFS), sedangkan prosedur PrintBFS memanfaatkan struktur data Queue dari pustaka standar untuk melakukan penelusuran melebar (BFS) secara iteratif, di mana kedua proses tersebut didahului oleh fungsi ResetVisited untuk memastikan status kunjungan simpul kembali ke kondisi awal.
