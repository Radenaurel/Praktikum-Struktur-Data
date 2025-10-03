 <h1 align="center">Laporan Praktikum Modul 2 <br> Pengenalan CPP Bag 2 </h1>
<p align="center">Raden Aurel Aditya Kusumawaningyun- 103112430267</p>

## Dasar Teori
Dalam studi Struktur Data, pondasi dimulai dengan memahami Array sebagai koleksi data sejenis yang tersimpan secara berurutan dan diakses melalui indeks. Konsep ini meluas hingga Array Dua Dimensi yang representasinya menyerupai tabel. Keterorganisasian data ini erat kaitannya dengan bagaimana program mengelola Memori (RAM), di mana setiap variabel memiliki alamat (address) unik. Untuk berinteraksi langsung dengan alamat tersebut, kita menggunakan variabel Pointer, yang secara spesifik bertugas menyimpan alamat memori variabel lain. Memahami Pointer sangat esensial karena ia menjadi kunci dalam mekanisme pelewatan parameter pada fungsi: ketika menggunakan Pemanggilan dengan Nilai (Call by Value), nilai variabel asli tidak akan berubah di luar fungsi ; namun, melalui Pemanggilan dengan Pointer atau Referensi (Call by Reference), yang pada dasarnya melewatkan alamat variabel, fungsi memiliki kemampuan untuk mengubah nilai variabel aktual yang berada di luar cakupannya. Konsep-konsep dasar ini merupakan landasan kritis dalam pemrograman modular, yang bertujuan agar kode menjadi lebih terstruktur, mudah diuji, dan reusable.

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

Kode C++ ini mendemonstrasikan mekanisme Pemanggilan dengan Pointer untuk menukar nilai dua variabel di luar fungsi utama. Intinya, saat fungsi tukar &a, &b dipanggil, ia tidak menerima nilai variabel 10 dan 20, melainkan alamat memori variabel a dan b. Di dalam fungsi tukar, operator Dereference (*) digunakan untuk mengakses lokasi memori asli tersebut, sehingga operasi penukaran (*px = *py; dan *py = temp) secara langsung memodifikasi nilai a dan b di dalam memori. Dengan cara ini, nilai variabel a dan b benar-benar tertukar setelah fungsi selesai dieksekusi, menghasilkan output a = 20, b = 10.

> Output
> ![Screenshot bagian x](output/UngadedTest.png)
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
> ![Screenshot bagian x](output/UngaidedAritmatika.png)
> Berikut SS VS Code dari Program Soal No 2




## Unguided

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan bertipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```go
#include <iostream>
#include <iomanip> 
using namespace std;

int main() {
    double bilangan1, bilangan2; 

    cout << " === Kalkulator Desimal === " << endl;

    cout << "Masukkan bilangan ke-1 : ";
    cin >> bilangan1;
    cout << "Masukkan bilangan ke-2 : ";
    cin >> bilangan2;

    cout << fixed << setprecision(2);

    cout << "\n=== Hasil Operasi Bilangan Desimal ===" << endl;
    cout << "Penjumlahan : " << bilangan1 + bilangan2 << endl;
    cout << "Pengurangan : " << bilangan1 - bilangan2 << endl;
    cout << "Perkalian   : " << bilangan1 * bilangan2 << endl;

    if (bilangan2 != 0) {
        cout << "Pembagian   : " << bilangan1 / bilangan2 << endl;
    } else {
        cout << "Pembagian   : Error! Pembagi tidak boleh nol." << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/Ungaided1yagesya.png)
> Ss VS Code Soal Unguided no 1


Penjelasan Singkat:
Program ini menggunakan tipe data double yang digunakan untuk bilangan desimal seperti float tapi lebih presisi untuk menerima dua input dari pengguna. Semua operasi aritmatika dilakukan dengan rumus operasi yang saya buat dan hasilnya dicetak langsung menggunakan cout. Ditambahkan pengecekan if untuk mencegah program error jika pengguna memasukkan angka nol sebagai pembagi. Penggunaan <iomanip> dan setprecision(2) digunakan agar output angka desimal terlihat rapi dan memiliki 2 angka dibelakang koma.

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100.

Contoh: 79 : tujuh puluh Sembilan

```go
#include <iostream>
#include <string>
using namespace std;

string sebutAngka(int angka) {
   
    string satuan[] = {"Nol", "Satu", "Dua", "Tiga", "Empat", "Lima", "Enam", "Tujuh", "Delapan", "Sembilan"};
    string hasil = "";

    if (angka < 11) {
        
        hasil = satuan[angka];
    } else if (angka < 20) {
      
        if (angka == 10) return "Sepuluh";
        else if (angka == 11) return "Sebelas";
        else return satuan[angka % 10] + " Belas";
    } else if (angka <= 99) {
        
        int puluhan = angka / 10;
        int sisa = angka % 10;

        if (puluhan == 2) hasil += "Dua Puluh";
        else if (puluhan == 7) hasil += "Tujuh Puluh"; 
        else hasil += satuan[puluhan] + " Puluh";

        if (sisa != 0) {
            hasil += " " + satuan[sisa];
        }
    } else if (angka == 100) {
        hasil = "Seratus";
    }
    return hasil;
}

int main() {
    int inputAngka;

    cout << "Masukkan angka (0-100): ";
    cin >> inputAngka;

    if (inputAngka < 0 || inputAngka > 100) {
        cout << "Output: Angka di luar batas 0-100." << endl;
    } else {
        cout << "Output: " << inputAngka << " : " << sebutAngka(inputAngka) << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](output/Ungaided2yagesya.png)

penjelasan singkat : 
Program ini menggunakan Fungsi [sebutAngka] untuk memproses konversi angka. Di dalam fungsi tersebut, digunakan struktur if-else if bertingkat untuk menangani berbagai rentang angka diantaranya: satuan yaitu 0-10, belasan yaitu 11-19, puluhan yaitu 20-99, dan seratus (100). Teknik modulo (%) dan pembagian integer (/) digunakan untuk memecah bilangan puluhan menjadi bagian puluhan dan satuan, memungkinkan program menggabungkan kata-kata seperti "Tujuh Puluh" dan "Sembilan".

### Soal 3

Buatlah program yang dapat memberikan input dan output (seperti pada gambar yang ada di soal)
 
 > ![Screenshot bagian x](output/SoalNomer3.png)

```go
#include <iostream>
using namespace std;

int main() {
    int n;

    cout << "Masukkan angka: ";
    cin >> n;

    int a = n;

    while (a >= 1) {

        int b = 1;
      
        while (b <= n - a) {
            cout << "  ";
            b++;
        }
        
        int c = a;
        while (c >= 1) {
            cout << c << " ";
            c--;
        }

        cout << "* ";

        int d = 1;
        while (d <= a) {
            cout << d << " ";
            d++;
        }

        cout << endl;
        a--;
    }

    int e = 1;
    while (e <= n) {
        cout << "  ";
        e++;
    }
    
    cout << "*" << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](output/Ungaided3yagesya.png)

penjelasan singkat : 
Kode ini bertujuan untuk menghasilkan sebuah pola simetris di konsol. Program ini menggunakan perulangan while dengan tujuan untuk menciptakan pola dua bagian yaitu sebuah segitiga terbalik di bagian atas dan sebuah titik bintang di bagian bawah. Pola ini dimulai dengan perulangan while terluar (while (a >= 1)) yang mengendalikan setiap baris dari atas ke bawah. Di setiap baris, perulangan while pertama (while (b <= n - a)) mencetak spasi di awal untuk menciptakan efek rata kanan. Selanjutnya, perulangan while berikutnya mencetak angka: dari c ke 1 (sisi kiri pola) dan dari 1 ke d (sisi kanan pola). Tanda bintang (*) ditambahkan di tengah untuk memisahkan kedua sisi. Bagian terakhir dari kode, di luar perulangan utama, mencetak baris terpisah di bagian bawah yang terdiri dari sejumlah spasi dan sebuah bintang tunggal.


## Referensi

Lippman, S. B., Lajoie, J., & Moo, B. E. (2012). C++ Primer (5th ed.). Addison-Wesley Professional.

Microsoft. (n.d.). struct (C++). Microsoft Learn. Retrieved September 26, 2025, from https://learn.microsoft.com/en-us/cpp/cpp/struct-cpp

Stroustrup, B. (1994). The Design and Evolution of C++. Addison-Wesley Publishing Company.

Stroustrup, B. (2013). The C++ Programming Language (4th ed.). Addison-Wesley Professional.

The C++ Resources Network. (n.d.). C++ Tutorials. Retrieved September 26, 2025, from https://www.cplusplus.com/doc/tutorial/

The C++ Standard Library. (n.d.). C++ reference. Retrieved September 26, 2025, from https://en.cppreference.com/w/cpp/

