 <h1 align="center">Laporan Praktikum Modul 3&4 <br> ADT & SLL </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun - 103112430267</p>

## Dasar Teori Modul 3
Abstract Data Type (ADT) adalah landasan konseptual dalam pemrograman yang mendefinisikan suatu TYPE struktur data beserta serangkaian PRIMITIF atau operasi dasar yang dapat dilakukan terhadapnya. Konsepnya berfokus pada "apa" yang dilakukan oleh data dan bukan "bagaimana" ia diimplementasikan secara internal, menjadikannya definisi yang Statik. Abstract Data Type yang lengkap mencakup delapan kelompok primitif, mulai dari Konstruktor untuk membentuk nilai type baru, Selector untuk mengakses komponen, Destruktor atau Dealokator untuk membebaskan memori, hingga operator relasional dan aritmatika. Dalam praktikum ini, prinsip Information Hiding dari ADT diwujudkan dengan memisahkan implementasi menjadi dua modul utama yaitu Spesifikasi (.h) yang berisi deklarasi type dan prototipe fungsi, dan Realisasi (.c atau .cpp) yang berisi kode program aktual dari primitif-primitif tersebut.

## Dasar Teori Modul 4
Linked List merupakan salah satu struktur data dinamis yang sangat penting, direpresentasikan sebagai serangkaian elemen data yang saling berkait dan bersifat fleksibel karena dapat tumbuh atau mengerut sesuai kebutuhan memori. Dalam implementasinya, Linked List memanfaatkan Pointer untuk menghubungkan setiap elemen. Singly Linked List (SLL) adalah model paling sederhana yang hanya menggunakan satu arah pointer, memungkinkan pembacaan hanya ke arah maju. Setiap elemen atau node dalam SLL terdiri dari dua bagian yaitu Data dan Pointer next yang menunjuk ke alamat node berikutnya, di mana node terakhir akan menunjuk ke NULL atau Nil. Operasi dasar SLL, yang disebut primitif, mencakup CreateList atau inisialisasi, alokasi/dealokasi memori, berbagai metode Insert seperti: First, Last, After, operasi Delete seperti: First, Last, After, dan View/printInfo. Semua primitif ini diorganisir ke dalam file .h dan .cpp sesuai dengan kaidah ADT, memastikan pemisahan antara spesifikasi dan implementasi.

## Guided Modul 3

### soal 1
mahasiswa.h
```go
#ifndef MAHASISWA_H_ICLUDED
#define MAHASISWA_H_ICLUDED

struct mahasiswa
{
   char nim [10];
   int nilai1, nilai2; /* data */
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif

```
> ![Screenshot bagian x](output3/guided1.1.png)

mahasiswa.cpp
```go
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m).nim;
    cout << "input nilai = ";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) /2;
}
```
> ![Screenshot bagian x](output3/guided1.2.png)

main.cpp
```go
#include <iostream>
#include "mahasiswa.h"
using namespace std;


int main()
{
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata-rata = " << rata2(mhs);
    return 0;
}

```

> Output
> ![Screenshot bagian x](output3/guided1.3.png)
> Berikut SS VS Code dari Program Soal No 1

penjelasan singkat : 

Kode C++ ini mendemonstrasikan bagaimana konsep Abstract Data Type (ADT) diimplementasikan secara terstruktur untuk menerapkan prinsip Penyembunyian Informasi. Intinya, ADT mahasiswa dibagi menjadi tiga komponen file logis yaitu mahasiswa.h berfungsi sebagai kontrak ADT yang mendefinisikan struct dan mendeklarasikan prototipe juga fungsi-fungsi primitif seperti inputMhs, rata2, hanya menyatakan apa yang disediakan oleh ADT. mahasiswa.cpp menjadi badan yang menyediakan realisasi kode aktual dari primitif tersebut, menjelaskan bagaimana operasi input dan perhitungan dilakukan. Sementara itu, main.cpp bertindak sebagai program driver yang menggunakan ADT dengan hanya perlu menyertakan file .h dan memanggil fungsi secara langsung, tanpa perlu mengetahui detail implementasi di file .cpp, yang merupakan inti dari arsitektur modular yang bersih.


## Unguided Modul 3

### soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

ungaided1.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

#include <iostream>
#include <string>
#include <iomanip>

using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    int uts;
    int uas;
    int tugas;
    float nilaiAkhir;
};

const int MAX_MHS = 10;


void inputDataMhs(Mahasiswa &mhs);

float hitungNilaiAkhir(const Mahasiswa &mhs);

void tampilDataMhs(const Mahasiswa &mhs);

#endif 
```
> ![Screenshot bagian x](output3/ungaided1.h.png)

ungaided1.cpp
```go
#include "ungaided1.h"
#include <iostream>
#include <limits> 

void inputDataMhs(Mahasiswa &mhs) {
   
    cout << "  Input Nama : ";
    getline(cin >> ws, mhs.nama); 
    
    cout << "  Input NIM  : ";
    getline(cin, mhs.nim); 

    cout << "  Input UTS  : ";
    cin >> mhs.uts;
    cout << "  Input UAS  : ";
    cin >> mhs.uas;
    cout << "  Input Tugas: ";
    cin >> mhs.tugas;
    
    mhs.nilaiAkhir = hitungNilaiAkhir(mhs);
}

float hitungNilaiAkhir(const Mahasiswa &mhs) {
    float na = (0.3f * mhs.uts) + (0.4f * mhs.uas) + (0.3f * mhs.tugas);
    return na;
}

void tampilDataMhs(const Mahasiswa &mhs) {
    cout << left << setw(20) << mhs.nama 
         << setw(15) << mhs.nim
         << setw(8) << mhs.uts
         << setw(8) << mhs.uas
         << setw(8) << mhs.tugas
         << fixed << setprecision(2) << mhs.nilaiAkhir << endl;
}
```
> ![Screenshot bagian x](output3/ungaided1.cpp.png)

mainungaided1.cpp
```go
#include "ungaided1.h"
#include <limits> 

int main() {
    
    
    Mahasiswa daftarMhs[MAX_MHS];
    int jumlahMhs = 0;
    char lanjut;

    cout << "PROGRAM INPUT DAN NILAI AKHIR MAHASISWA" << endl;
   
    do {
        if (jumlahMhs >= MAX_MHS) {
            cout << "Batas maksimum mahasiswa (" << MAX_MHS << ") telah tercapai." << endl;
            break;
        }

        cout << "\n--- Input Mahasiswa Ke-" << jumlahMhs + 1 << " ---" << endl;
  
        inputDataMhs(daftarMhs[jumlahMhs]); 

        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        jumlahMhs++;

        cout << "Lanjut input data? (yak/tidak): ";
        cin >> lanjut;
    
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
        
    } while (lanjut == 'y' || lanjut == 'Y');

    cout << "DAFTAR NILAI AKHIR MAHASISWA (" << jumlahMhs << " dari " << MAX_MHS << ")" << endl;
    cout << left << setw(20) << "NAMA" 
         << setw(15) << "NIM"
         << setw(8) << "UTS"
         << setw(8) << "UAS"
         << setw(8) << "TUGAS"
         << "NILAI AKHIR" << endl;
    

    for (int i = 0; i < jumlahMhs; ++i) {
        tampilDataMhs(daftarMhs[i]); 
    }

    return 0;
}
```
> Output
> ![Screenshot bagian x](output3/mainungaided1.cpp.png)
> > Berikut SS VS Code dari Program Soal No 1

penjelasan singkat : 

Kode C++ ini adalah demonstrasi sukses implementasi Abstract Data Type (ADT) untuk mengelola sekumpulan data mahasiswa dalam sebuah array. Intinya, kami memisahkan tanggung jawab kode secara ketat: Mahasiswa.h mendefinisikan type dan primitif, sementara Mahasiswa.cpp menyediakan realisasi fungsi seperti hitungNilaiAkhir (menggunakan rumus 0.3⋅UTS+0.4⋅UAS+0.3⋅Tugas). Program utama (main.cpp) berfungsi sebagai driver yang mengelola array dan loop input, dan yang terpenting, ia menyertakan mekanisme pembersihan input buffer (cin.ignore) secara strategis. Keberhasilan ini tidak hanya membuktikan implementasi rumus yang benar, tetapi juga menjamin keandalan user input campuran string dan numerik di dalam loop yang berkelanjutan, menghasilkan output tabel nilai yang terstruktur dan akurat.


### soal 2

Buatlah ADT pelajaran sebagai berikut di dalam file “pelajaran.h”:



ungaided1.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

#include <iostream>
#include <string>
#include <iomanip>

using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    int uts;
    int uas;
    int tugas;
    float nilaiAkhir;
};

const int MAX_MHS = 10;


void inputDataMhs(Mahasiswa &mhs);

float hitungNilaiAkhir(const Mahasiswa &mhs);

void tampilDataMhs(const Mahasiswa &mhs);

#endif 
```
> ![Screenshot bagian x](output3/ungaided1.h.png)

ungaided1.cpp
```go
#include "ungaided1.h"
#include <iostream>
#include <limits> 

void inputDataMhs(Mahasiswa &mhs) {
   
    cout << "  Input Nama : ";
    getline(cin >> ws, mhs.nama); 
    
    cout << "  Input NIM  : ";
    getline(cin, mhs.nim); 

    cout << "  Input UTS  : ";
    cin >> mhs.uts;
    cout << "  Input UAS  : ";
    cin >> mhs.uas;
    cout << "  Input Tugas: ";
    cin >> mhs.tugas;
    
    mhs.nilaiAkhir = hitungNilaiAkhir(mhs);
}

float hitungNilaiAkhir(const Mahasiswa &mhs) {
    float na = (0.3f * mhs.uts) + (0.4f * mhs.uas) + (0.3f * mhs.tugas);
    return na;
}

void tampilDataMhs(const Mahasiswa &mhs) {
    cout << left << setw(20) << mhs.nama 
         << setw(15) << mhs.nim
         << setw(8) << mhs.uts
         << setw(8) << mhs.uas
         << setw(8) << mhs.tugas
         << fixed << setprecision(2) << mhs.nilaiAkhir << endl;
}
```
> ![Screenshot bagian x](output3/ungaided1.cpp.png)

mainungaided1.cpp
```go
#include "ungaided1.h"
#include <limits> 

int main() {
    
    
    Mahasiswa daftarMhs[MAX_MHS];
    int jumlahMhs = 0;
    char lanjut;

    cout << "PROGRAM INPUT DAN NILAI AKHIR MAHASISWA" << endl;
   
    do {
        if (jumlahMhs >= MAX_MHS) {
            cout << "Batas maksimum mahasiswa (" << MAX_MHS << ") telah tercapai." << endl;
            break;
        }

        cout << "\n--- Input Mahasiswa Ke-" << jumlahMhs + 1 << " ---" << endl;
  
        inputDataMhs(daftarMhs[jumlahMhs]); 

        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        jumlahMhs++;

        cout << "Lanjut input data? (yak/tidak): ";
        cin >> lanjut;
    
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); 
        
    } while (lanjut == 'y' || lanjut == 'Y');

    cout << "DAFTAR NILAI AKHIR MAHASISWA (" << jumlahMhs << " dari " << MAX_MHS << ")" << endl;
    cout << left << setw(20) << "NAMA" 
         << setw(15) << "NIM"
         << setw(8) << "UTS"
         << setw(8) << "UAS"
         << setw(8) << "TUGAS"
         << "NILAI AKHIR" << endl;
    

    for (int i = 0; i < jumlahMhs; ++i) {
        tampilDataMhs(daftarMhs[i]); 
    }

    return 0;
}
```
> Output
> ![Screenshot bagian x](output3/mainungaided1.cpp.png)
> > Berikut SS VS Code dari Program Soal No 1

penjelasan singkat : 

Kode C++ ini adalah demonstrasi sukses implementasi Abstract Data Type (ADT) untuk mengelola sekumpulan data mahasiswa dalam sebuah array. Intinya, kami memisahkan tanggung jawab kode secara ketat: Mahasiswa.h mendefinisikan type dan primitif, sementara Mahasiswa.cpp menyediakan realisasi fungsi seperti hitungNilaiAkhir (menggunakan rumus 0.3⋅UTS+0.4⋅UAS+0.3⋅Tugas). Program utama (main.cpp) berfungsi sebagai driver yang mengelola array dan loop input, dan yang terpenting, ia menyertakan mekanisme pembersihan input buffer (cin.ignore) secara strategis. Keberhasilan ini tidak hanya membuktikan implementasi rumus yang benar, tetapi juga menjamin keandalan user input campuran string dan numerik di dalam loop yang berkelanjutan, menghasilkan output tabel nilai yang terstruktur dan akurat.




## Referensi
Lippman, S. B., Lajoie, J., & Moo, B. E. (2012). C++ Primer (5th ed.). Addison-Wesley Professional.

Stroustrup, B. (1994). The Design and Evolution of C++. Addison-Wesley Publishing Company.

Stroustrup, B. (2013). The C++ Programming Language (4th ed.). Addison-Wesley Professional.

Modul Praktikum & Institusional
Telkom University. (n.d.). Modul 2 Pengenalan Bahasa C++ (Bagian Kedua). Fakultas Informatika.

The C++ Resources Network. (n.d.). C++ Tutorials. Retrieved October 3, 2025, from https://www.cplusplus.com/doc/tutorial/

The C++ Standard Library. (n.d.). C++ reference. Retrieved October 3, 2025, from https://en.cppreference.com/w/cpp/

Microsoft. (n.d.). struct (C++). Microsoft Learn. Retrieved October 3, 2025, from https://learn.microsoft.com/en-us/cpp/cpp/struct-cpp

