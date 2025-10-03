 <h1 align="center">Laporan Praktikum Modul 2 <br> Pengenalan CPP Bag 2 </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori
Dalam studi Struktur Data, pondasi dimulai dengan memahami Array sebagai koleksi data sejenis yang tersimpan secara berurutan dan diakses melalui indeks. Konsep ini meluas hingga Array Dua Dimensi yang representasinya menyerupai tabel. Keterorganisasian data ini erat kaitannya dengan bagaimana program mengelola Memori, di mana setiap variabel memiliki alamat unik. Untuk berinteraksi langsung dengan alamat tersebut, kita menggunakan variabel Pointer, yang secara spesifik bertugas menyimpan alamat memori variabel lain. Memahami Pointer sangat esensial karena ia menjadi kunci dalam mekanisme pelewatan parameter pada fungsi yaitu ketika menggunakan Pemanggilan dengan Nilai, nilai variabel asli tidak akan berubah di luar fungsi ; namun, melalui Pemanggilan dengan Pointer atau Referensi, yang pada dasarnya melewatkan alamat variabel, fungsi memiliki kemampuan untuk mengubah nilai variabel aktual yang berada di luar cakupannya. Konsep-konsep dasar ini merupakan landasan kritis dalam pemrograman modular, yang bertujuan agar kode menjadi lebih terstruktur, mudah diuji, dan reusable.

## Guided

### soal 1
Call By Pointer
```go
#include <iostream>
using namespace std;

void tukaryagesya (int *px, int *py); 

int main()
{
    int a = 10, b = 20;

    cout << "Pas Sebelum ditukar: a = " << a << ", b = " << b << endl;
    
    tukaryagesya(&a, &b); 
    
    cout << "Pas Setelah ditukar: a = " << a << ", b = " << b << endl;
    
    return 0;
}


void tukaryagesya(int *px, int *py)
{
    
    int temp = *px; 
    
    
    *px = *py; 
    
    *py = temp; 
}

```

Kode C++ ini mendemonstrasikan mekanisme Pemanggilan dengan Pointer untuk menukar nilai dua variabel di luar fungsi utama. Intinya, saat fungsi tukar &a, &b dipanggil, ia tidak menerima nilai variabel 10 dan 20, melainkan alamat memori variabel a dan b. Di dalam fungsi tukar, operator Dereference (*) digunakan untuk mengakses lokasi memori asli tersebut, sehingga operasi penukaran *px = *py; dan *py = temp secara langsung memodifikasi nilai a dan b di dalam memori. Dengan cara ini, nilai variabel a dan b benar-benar tertukar setelah fungsi selesai dieksekusi, menghasilkan output a = 20, b = 10.

> Output
> ![Screenshot bagian x](output/Guided1.png)
> Berikut SS VS Code dari Program Soal No 1

### soal 2
Call By Reference

```go
#include <iostream>
using namespace std;


void tukar(int &x, int &y); 

int main()
{
    int a = 10, b = 20;
    
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    

    tukar(a, b); 
    
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    
    return 0;
}


void tukar(int &x, int &y) 
{
    int temp = x;
    x = y;
    y = temp;
}
```

Kode C++ ini mendemonstrasikan mekanisme Pemanggilan dengan Referensi untuk menukar nilai dua variabel yang berada di luar fungsi utama. Intinya, saat fungsi tukar a, b dipanggil, ia tidak menyalin nilai variabel a dan b; melainkan, melalui simbol reference (&) pada parameter formalnya, variabel x dan y menjadi alias yang merujuk pada variabel a dan b di lokasi memori yang sama. Di dalam fungsi tukar, semua operasi penukaran x = y; dan y = temp; secara langsung memodifikasi nilai a dan b di dalam memori. Dengan cara ini, nilai variabel a dan b benar-benar tertukar setelah fungsi selesai dieksekusi, menghasilkan output a = 20, b = 10.

> Output
> ![Screenshot bagian x](output/Guided2.png)
> Berikut SS VS Code dari Program Soal No 2




## Unguided

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:
1 2 3
4 5 6
7 8 9

Matriks Hasil Transpose:
1 4 7
2 5 8
3 6 9


```go
#include <iostream>
using namespace std;

const int uMatriks = 3;

void tampilkanMatriks(int matriks[uMatriks][uMatriks]) {
    for (int i = 0; i < uMatriks; i++) {
        for (int j = 0; j < uMatriks; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl; 
    }
}

int main() {
  
    int matriksAwal[uMatriks][uMatriks] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int matriksTranspose[uMatriks][uMatriks];

    for (int i = 0; i < uMatriks; i++) {
        for (int j = 0; j < uMatriks; j++) {
            matriksTranspose[j][i] = matriksAwal[i][j];
        }
    }

    cout << "Matriks Awal:\n";
    tampilkanMatriks(matriksAwal);

    cout << "\nMatriks Hasil Transpose:\n";
    tampilkanMatriks(matriksTranspose);

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/Ungaided1yagesya.png)
> Ss VS Code Soal Unguided no 1


Penjelasan Singkat:
Kode C++ ini mendemonstrasikan bagaimana kita bisa membuat program yang efisien untuk melakukan operasi Transpose Matriks berukuran 3×3 menggunakan Array Dua Dimensi. Program ini bertujuan untuk mengubah baris menjadi kolom dan sebaliknya pada matriksAwal dan menyimpan hasilnya pada matriksTranspose. Kode ini juga menggunakan Prosedur tampilkanMatriks (void) untuk mencetak isi matriks, yang mendukung konsep modularitas dan membuat kode utama lebih rapi dan mudah digunakan kembali (reusable). Secara keseluruhan, kode ini membuktikan bahwa operasi transpose dalam pemrograman hanyalah masalah membalik posisi indeks setiap elemen data saat disalin dari array sumber ke array tujuan.
 
### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25

```go
#include <iostream>
using namespace std;

void kuadratkan(int &bilangan); 

int main() {
    int nilai = 5;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}

void kuadratkan(int &bilangan) {
    bilangan = bilangan * bilangan;
}
```

> Output
> ![Screenshot bagian x](output/Ungaided2yagesya.png)

penjelasan singkat : 
Kode C++ ini mendemonstrasikan mekanisme Pemanggilan dengan Referensi untuk menukar nilai variabel a dan b di luar fungsi utama. Fungsi tukar didefinisikan dengan menggunakan simbol & pada parameter formalnya int &x, int &y, yang menyebabkan x dan y menjadi alias untuk variabel asli a dan b. Saat tukar a, b; dipanggil, semua operasi penukaran yang terjadi pada x dan y di dalam fungsi x = y; dan y = temp; secara langsung memengaruhi dan mengubah nilai variabel asli di lokasi memori yang sama. Hasilnya, nilai a dan b berhasil tertukar secara permanen a = 20, b = 10. Mekanisme ini adalah cara yang efisien untuk memodifikasi data sumber di luar fungsi tanpa perlu menggunakan operator pointer "*".


## Referensi
Lippman, S. B., Lajoie, J., & Moo, B. E. (2012). C++ Primer (5th ed.). Addison-Wesley Professional.

Stroustrup, B. (1994). The Design and Evolution of C++. Addison-Wesley Publishing Company.

Stroustrup, B. (2013). The C++ Programming Language (4th ed.). Addison-Wesley Professional.

Modul Praktikum & Institusional
Telkom University. (n.d.). Modul 2 Pengenalan Bahasa C++ (Bagian Kedua). Fakultas Informatika.

The C++ Resources Network. (n.d.). C++ Tutorials. Retrieved October 3, 2025, from https://www.cplusplus.com/doc/tutorial/

The C++ Standard Library. (n.d.). C++ reference. Retrieved October 3, 2025, from https://en.cppreference.com/w/cpp/

Microsoft. (n.d.). struct (C++). Microsoft Learn. Retrieved October 3, 2025, from https://learn.microsoft.com/en-us/cpp/cpp/struct-cpp
