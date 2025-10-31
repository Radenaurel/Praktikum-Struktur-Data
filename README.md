<h1 align="center">Laporan Praktikum Modul 7 <br> STACK </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori Modul 7
A. Konsep Dasar STACK

1. Konsep Dasar Stack
Stack merupakan salah satu bentuk struktur data yang beroperasi berdasarkan prinsip tumpukan, di mana prinsip operasi yang digunakan adalah Last In First Out (LIFO). Ini berarti bahwa elemen yang terakhir kali masuk ke dalam tumpukan adalah elemen yang pertama kali dapat diambil. Dalam representasi Linked List, Stack terdiri dari elemen-elemen yang saling terkait, namun akses data hanya dapat dilakukan pada elemen paling awal saja, yang disebut "Top". Struktur Stack dapat diimplementasikan menggunakan representasi pointer atau representasi tabel.

2. Operasi Primitif Stack
Terdapat dua operasi utama dalam Stack: Push atau penyisipan dan Pop atau pengambilan.
- Push Operasi menyisipkan elemen baru pada tumpukan data. Dalam implementasi Stack menggunakan pointer, operasi ini identik dengan operasi insert first pada Linked List biasa. Dalam representasi tabel, Push dilakukan dengan menggeser indeks TOP ke indeks berikutnya (TOP = TOP + 1) dan memasukkan data pada indeks TOP yang baru.
- Pop Operasi pengambilan data yang selalu dilakukan pada elemen paling atas (Top). Dalam implementasi pointer, Pop mirip dengan operasi delete first. Setelah data diambil, indeks TOP akan bergeser ke indeks sebelumnya (TOP = TOP - 1), tanpa harus menghilangkan informasi dari indeks TOP sebelumnya.

4. Implementasi dan Aplikasi
Implementasi Stack harus dilengkapi dengan beberapa fungsi primitif untuk memastikan manajemen Stack berjalan dengan benar, termasuk createStack() untuk inisialisasi, isEmpty() untuk pengecekan status, dan fungsi pencarian. Perbedaan utama antara representasi pointer dan tabel terletak pada manajemen memori; representasi pointer memerlukan alokasi dan dealokasi memori, sedangkan representasi tabel tidak memerlukannya karena menggunakan array berindeks yang ukurannya sudah terbatas. Struktur data Stack sering diaplikasikan dalam komputasi, salah satunya untuk pemrosesan ekspresi matematika (infix ke postfix atau prefix) dan manajemen memori panggilan fungsi (call stack).


## Guided Modul 6

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
> ![Screenshot bagian x](Output6/guided1.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan: 

Program C++ ini berfungsi untuk mengimplementasikan struktur data Stack menggunakan representasi Linked List dan menguji operasi dasar Last In First Out (LIFO). Program mendefinisikan struktur Node dengan pointer next dan menggunakan pointer top untuk menandai elemen teratas tumpukan. Logika utamanya terletak pada dua operasi primitif: push, yang menyisipkan elemen baru selalu di posisi top, dan pop, yang mengambil dan menghapus elemen dari posisi top. Fungsi show digunakan untuk menampilkan seluruh isi Stack dimulai dari TOP, sementara fungsi isEmpty memastikan operasi tidak dilakukan pada Stack kosong. Fungsi main menguji operasi ini secara berurutan: menyisipkan elemen 30, 20, 10, menampilkan Stack, dan menghapus satu elemen teratas.

# Daftar Pustaka

Putra, D. P., Herlambang, A. D., & Rachmadi, A. (2023). Pengembangan Aplikasi Web IDE berbasis Mobile sebagai Alat Bantu Proses Pembelajaran Pemrograman Web Kelas X TKJ di SMK Cendika Bangsa. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 7(7), 3260-3267.

Ma’arif, A. (2021). Dasar pemrograman bahasa C++ [Buku ajar]. Universitas Ahmad Dahlan.

Indahyati, Uce., Rahmawati Yunianita. (2020). "BUKU AJAR ALGORITMA DAN PEMROGRAMAN DALAM BAHASA C++". Sidoarjo: Umsida Press. Diakses pada 10 Maret 2024 melalui https://doi.org/10.21070/2020/978-623-6833-67-4.

Guna, L. A. (2022). Implementasi Prosedur dan Fungsi Dalam Bahasa Pemrograman Python. Jurnal Portal Data, 2(1). Diakses melalui https://ejurnal-bpptik.kominfo.go.id/index.php/jpd/article/view/118.

[1.1] Suryadi, B., & Herlambang, T. S. (2018). Implementasi Str
