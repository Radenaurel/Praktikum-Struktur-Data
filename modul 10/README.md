<h1 align="center">Laporan Praktikum 
  
  Modul 10 <br> REKURSIF </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori Modul 10
A. Konsep Dasar REKURSIF & Struktur Data Tree

Pada modul ini, konsep dasar yang dipelajari berfokus pada dua hal utama yaitu penggunaan fungsi rekursif dan implementasi struktur data non-linear berbentuk Tree. Secara sederhana, rekursif adalah metode pemrograman di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan masalah. Agar fungsi ini tidak berjalan terus-menerus tanpa henti, rekursif wajib memiliki base case atau kondisi khusus yang memicu penghentian pemanggilan diri tersebut. Meskipun penggunaan rekursif bisa membuat kode program terlihat lebih bersih dan mudah dibaca karena memecah masalah besar menjadi bagian-bagian kecil, kita perlu berhati-hati karena metode ini memakan memori lebih banyak untuk menyimpan activation record setiap kali fungsi dipanggil. Selanjutnya, materi beralih ke struktur data Tree. Berbeda dengan array atau linked list yang bersifat linear, Tree adalah struktur data hierarkis yang terdiri dari node. Sebuah Tree pasti memiliki satu root sebagai simpul teratas, dan simpul-simpul di bawahnya disebut child yang bisa memiliki cabang lagi hingga mencapai leaf atau simpul yang tidak punya anak. Dalam praktikum ini, fokus utamanya adalah Binary Tree, yaitu pohon di mana setiap parent maksimal hanya boleh memiliki dua orang anak kiri dan kanan.

Secara spesifik, kita menerapkan Binary Search Tree. BST memiliki aturan penempatan data yang ketat agar pencarian data menjadi efisien yaitu semua data yang nilainya lebih kecil dari parent harus diletakkan di Left Subtree, sedangkan data yang lebih besar diletakkan di Right Subtree. Dengan aturan ini, operasi seperti insert, search, hingga delete dapat dilakukan dengan pola yang terstruktur. Misalnya, saat mencari angka, kita tinggal membandingkan nilainya dengan root, jika lebih kecil kita belok ke kiri, jika lebih besar kita belok ke kanan, terus berulang hingga data ditemukan atau mencapai ujung tree. Terakhir, untuk mengakses atau menampilkan data yang sudah tersusun dalam Tree, kita menggunakan teknik Traversal. Ada tiga metode utama yang dipelajari diantaranya: Pre-order dengah cetak Root dulu, baru ke Kiri, lalu Kanan, In-order dengan cara ke Kiri dulu, cetak Root, baru ke Kanan, dan Post-order dengan cara ke Kiri, ke Kanan, baru cetak Root terakhir. Menariknya, jika kita melakukan In-order traversal pada sebuah Binary Search Tree, hasil outputnya otomatis akan terurut dari nilai terkecil ke terbesar

## Guided Modul 10

### soal 1

```go
 #include <iostream>
 using namespace std;

 struct Node {
    int data;
    Node* next;
 };

bool isEmpty(Node *top)
{
    return top == nullptr;
}
 void push(Node *&top, int data)
 {
    Node *newNode = new Node(); 
    newNode->data = data;
    newNode->next = top;
    top = newNode;
 }

 int pop(Node *&top)
 {
    if (isEmpty(top))
    {
        cout << "Stack kosong, tidak bisa di pop!" << endl;
        return 0;
    }
 
 int poppedData = top->data;
 Node *temp = top;
 top = top->next;

 delete temp;
 return poppedData;
}

void show(Node *top) 
{
    if (isEmpty(top))
    {
        cout << "stack kosong." << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp ->data << "->'";
        temp = temp->next;
    }
    cout << "NULL" << endl;
    
}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi Stack: " << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan SIsa Stack: " << endl;
}

```


> Output
> ![Screenshot bagian x](Output7/guided1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 

Program ini merupakan implementasi struktur data Binary Search Tree (BST) menggunakan bahasa C++. Struktur dasar pohon dibentuk melalui struct Node yang memiliki tiga elemen utama yaitu data bertipe integer, serta pointer kiri dan kanan yang berfungsi sebagai penghubung antar simpul secara hierarkis. Fungsi utama pembentuk pohon adalah insert, yang bekerja secara rekursif. Sesuai aturan BST, fungsi ini akan membandingkan nilai input dengan root, jika nilai lebih kecil maka akan menelusuri pointer kiri, dan jika lebih besar akan ke kanan, hingga menemukan posisi kosong (NULL) untuk menempatkan node baru. Selain penyisipan data, program ini dilengkapi fitur manipulasi data yang kompleks seperti hapus dan update. Fungsi hapus menangani tiga skenario penghapusan simpul, penghapusan leaf, simpul dengan satu anak, dan simpul dengan dua anak. Adapun fungsi update tidak sekadar mengubah nilai data, melainkan menggunakan mekanisme penghapusan nilai lama diikuti penyisipan nilai baru. Hal ini dilakukan untuk menjaga konsistensi urutan BST agar struktur pohon tidak rusak akibat perubahan nilai. Terakhir, program menampilkan data menggunakan tiga metode traversal rekursif yaitu preOrder, postOrder, dan inOrder yang secara otomatis menampilkan data dalam keadaan terurut.

## Unguided Modul 10

### soal 1

```go
#include <iostream>
#define Nil NULL 

using namespace std;

typedef int infotype;
typedef struct Node *address; 

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x); 
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil) {
        return Nil; 
    } else if (root->info == x) {
        return root; 
    } else {
        if (x < root->info) {
            return findNode(x, root->left);
        } else {
            return findNode(x, root->right); 
        }
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);           
        cout << root->info << " - ";   
        InOrder(root->right);         
    }
}

int main() {
    cout << "Hello World" << endl;

    address root = Nil; 

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); 
    insertNode(root, 7);

    InOrder(root);
    
    cout << endl;

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output7/guided1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 

Program ini merupakan implementasi struktur data Binary Search Tree (BST) yang disatukan dalam satu file sumber menggunakan bahasa C++. Struktur dasar pohon dibentuk melalui struct Node yang memiliki tiga elemen utama yaitu info bertipe integer, serta pointer left dan right yang berfungsi sebagai penghubung antar simpul secara hierarkis . Fungsi utama pembentuk pohon adalah insertNode, yang bekerja secara rekursif untuk menempatkan data pada memori yang dialokasikan . Sesuai aturan BST, fungsi ini akan membandingkan nilai input dengan root, jika nilai lebih kecil maka akan menelusuri pointer kiri, dan jika lebih besar akan ke kanan, hingga menemukan posisi kosong untuk menempatkan node baru. Dalam eksekusi program utama, terdapat input data bernilai ganda yaitu angka 6, namun logika penyisipan dirancang untuk hanya memproses nilai yang unik sehingga duplikasi data secara otomatis diabaikan. Terakhir, program menampilkan data menggunakan metode traversal rekursif InOrder yang secara otomatis mencetak seluruh elemen pohon dalam urutan yang terurut dari nilai terkecil hingga terbesar

### soal 2

```go
#include <iostream>
#define Nil NULL 

using namespace std;
typedef int infotype;
typedef struct Node *address; 

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x); 
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);           
        cout << root->info << " - ";   
        InOrder(root->right);         
    }
}

int hitungNode(address root) {
    if (root == Nil) {
        return 0; 
    } else {
        
        return 1 + hitungNode(root->left) + hitungNode(root->right);
    }
}

int hitungTotal(address root) {
    if (root == Nil) {
        return 0; 
    } else {
        return root->info + hitungTotal(root->left) + hitungTotal(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start; 
    } else {
        int leftDepth = hitungKedalaman(root->left, start + 1);
        int rightDepth = hitungKedalaman(root->right, start + 1);
        
        if (leftDepth > rightDepth) {
            return leftDepth;
        } else {
            return rightDepth;
        }
    }
}

int main() {
    cout << "Hello World" << endl;

    address root = Nil; 

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); 
    insertNode(root, 7);
    InOrder(root);
    cout << "\n";
    
    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah Node : " << hitungNode(root) << endl;
    cout << "total : " << hitungTotal(root) << endl;

    return 0;
}

```


> Output
> ![Screenshot bagian x](Output7/guided1.png)
> Berikut SS VS Code dari Program Soal No 2

penjelasan: 

Program ini merupakan pengembangan dari implementasi ADT Binary Search Tree sebelumnya, dengan penambahan tiga fungsi analitik rekursif untuk mengevaluasi properti pohon. Fungsi pertama, hitungNode, bekerja dengan menjumlahkan setiap simpul yang ditemui ditambah hasil penelusuran dari sub-pohon kiri dan kanan, sehingga menghasilkan total simpul yang ada dalam BST . Fungsi kedua, hitungTotal, memiliki logika serupa namun mengakumulasikan nilai info dari setiap simpul, menjumlahkan seluruh data integer yang tersimpan dalam struktur pohon . Terakhir, fungsi hitungKedalaman dirancang untuk mengukur tinggi pohon dengan menelusuri lintasan terjauh dari akar ke daun; fungsi ini memanfaatkan parameter tambahan start sebagai akumulator level, di mana setiap pemanggilan rekursif akan menambah nilai kedalaman, dan pada akhirnya membandingkan kedalaman sub-pohon kiri dan kanan untuk mengambil nilai maksimum sebagai output akhir.


### soal 3

```go
 #include <iostream>
#define Nil NULL 

using namespace std;
typedef int infotype;
typedef struct Node *address; 

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x); 
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

void PreOrder(address root) {
    if (root != Nil) {
        cout << root->info << " - ";   
        PreOrder(root->left);          
        PreOrder(root->right);   
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);           
        cout << root->info << " - ";   
        InOrder(root->right);         
    }
}

void PostOrder(address root) {
    if (root != Nil) {
        PostOrder(root->left);         
        PostOrder(root->right);        
        cout << root->info << " - ";   
    }
}

int main() {
    cout << "Hello World" << endl;

    address root = Nil; 

    insertNode(root, 6);
    insertNode(root, 4); 
    insertNode(root, 7); 
    insertNode(root, 2); 
    insertNode(root, 5); 
    insertNode(root, 1); 
    insertNode(root, 3); 
    cout << "Tampilan PreOrder  : ";
    PreOrder(root);
    cout << endl;

    cout << "Tampilan InOrder   : ";
    InOrder(root);
    cout << endl;

    cout << "Tampilan PostOrder : ";
    PostOrder(root);
    cout << endl;

    return 0;
}
```


> Output
> ![Screenshot bagian x](Output7/guided1.png)
> Berikut SS VS Code dari Program Soal No 3

penjelasan: 

Program ini menyelesaikan persoalan nomor 3 dengan mengimplementasikan dua prosedur traversal tambahan, yaitu PreOrder dan PostOrder. Untuk mereplikasi struktur pohon yang sesuai dengan Ilustrasi Tree, fungsi utama dikonfigurasi untuk memasukkan data dengan urutan spesifik (6, 4, 7, 2, 5, 1, dan 3) agar terbentuk topologi pohon dengan root bernilai 6 . Prosedur PreOrder bekerja secara rekursif dengan mencetak simpul akar terlebih dahulu sebelum menelusuri sub-pohon kiri dan kanan, menghasilkan urutan output 6-4-2-1-3-5-7 . Sebaliknya, prosedur PostOrder menelusuri cabang kiri dan kanan hingga selesai baru kemudian mencetak simpul akar, yang menghasilkan urutan output 1-3-2-5-4-7-6 . Implementasi ini melengkapi metode InOrder sebelumnya, memberikan gambaran utuh mengenai berbagai strategi penelusuran data dalam struktur Binary Search Tree.
