# M.AFRIZA-MARANTIKA-103112430271Modul6
LAPRAK MODUL 6

# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA) </h1>
<p align="center">M.AFRIZA MARANTIKA - 103112430271</p>

## Dasar Teori

Doubly Linked List merupakan struktur data yang setiap elemennya saling terhubung dua arah melalui pointer next dan prev. Pointer next digunakan untuk menunjuk node berikutnya, sedangkan prev menunjuk node sebelumnya. Struktur ini memiliki dua penunjuk utama, yaitu first yang mengarah ke node pertama dan last yang mengarah ke node terakhir. Dengan adanya dua arah hubungan tersebut, Doubly Linked List memungkinkan proses traversal, penambahan, dan penghapusan data dilakukan dari dua arah dengan lebih fleksibel. Namun, struktur ini memerlukan memori lebih besar karena setiap node menyimpan dua pointer.
## Guided
### soal 1 
```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
       head->prev = newNode;
    else
       tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current ->data != target)
        current = current->next;

    if(current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if  (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;
    
    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}
void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}
void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}

```
Program ini membuat Singly Linked List dengan node berisi data dan pointer. head sebagai awal list. Ada fungsi untuk tambah, sisip, hapus, ubah, dan tampilkan data. Semua operasi dilakukan dengan mengatur pointer antar node. Program pakai menu agar pengguna bisa pilih operasi.


> Output


## Unguided

### Soal 1

```c++
#include <iostream>
#include <string>
using namespace std;

struct Node {
    string nama;
    string order;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

bool kosong() {
    return head == nullptr;
}

void enqueue(const string& nama, const string& order) {
    Node* baru = new Node;
    baru->nama = nama;
    baru->order = order;
    baru->next = nullptr;

    if (kosong()) {
        head = tail = baru;
    } else {
        tail->next = baru;
        tail = baru;
    }
    cout << "Antrian " << nama << " berhasil ditambahkan.\n";
}

void dequeue() {
    if (kosong()) {
        cout << "Antrian kosong, tidak ada yang dilayani.\n";
        return;
    }

    Node* hapus = head;
    cout << "Melayani pembeli: " << hapus->nama << " - " << hapus->order << endl;
    head = head->next;
    if (head == nullptr) tail = nullptr;
    delete hapus;
}

void tampil() {
    if (kosong()) {
        cout << "Tidak ada antrian.\n";
        return;
    }

    cout << "\n=== Daftar Antrian ===\n";
    Node* temp = head;
    int nomor = 1;
    while (temp != nullptr) {
        cout << nomor << ". " << temp->nama << " - " << temp->order << endl;
        temp = temp->next;
        nomor++;
    }
    cout << endl;
}

void cari(const string& namaCari) {
    if (kosong()) {
        cout << "Antrian kosong.\n";
        return;
    }

    Node* temp = head;
    int posisi = 1;
    bool ketemu = false;

    while (temp != nullptr) {
        if (temp->nama == namaCari) {
            cout << "\nPembeli ditemukan!\n";
            cout << "Posisi : " << posisi << endl;
            cout << "Nama   : " << temp->nama << endl;
            cout << "Pesanan: " << temp->order << endl;
            ketemu = true;
            break;
        }
        temp = temp->next;
        posisi++;
    }

    if (!ketemu) {
        cout << "Pembeli \"" << namaCari << "\" tidak ditemukan.\n";
    }
}

int main() {
    int menu;
    string nama, pesanan;

    do {
        cout << "=============================\n";
        cout << "   SISTEM ANTRIAN PEMBELI    \n";
        cout << "=============================\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Cari Pembeli\n";
        cout << "5. Keluar\n";
        cout << "=============================\n";
        cout << "Pilih menu: ";
        cin >> menu;
        cin.ignore();

        switch (menu) {
            case 1:
                cout << "Masukkan Nama   : ";
                getline(cin, nama);
                cout << "Masukkan Pesanan: ";
                getline(cin, pesanan);
                enqueue(nama, pesanan);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                tampil();
                break;
            case 4:
                cout << "Nama pembeli yang dicari: ";
                getline(cin, nama);
                cari(nama);
                break;
            case 5:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }

        cout << endl;
    } while (menu != 5);

    return 0;
}
```
Program ini membuat sistem antrian pembeli menggunakan linked list. Setiap node menyimpan nama dan pesanan. Variabel front dan rear menandai awal dan akhir antrian. Fungsi tambahAntrian menambah pembeli ke antrian, layaniAntrian menghapus pembeli dari depan, tampilAntrian menampilkan semua antrian, dan cariPembeli mencari nama tertentu dalam antrian. Program utama menampilkan menu pilihan dan menjalankan fungsi sesuai input pengguna.
       
> Output
> ![Screenshot bagian x](ssmodul5unguided1.png)



### Soal 2

```c++
#include <iostream>
#include <string>
using namespace std;

struct Buku {
    string isbn;
    string judul;
    string penulis;
    Buku* next;
};

class LinkedList {
private:
    Buku* head;

public:
    LinkedList() : head(nullptr) {}

    bool kosong() {
        return head == nullptr;
    }

    void tambah(string isbn, string judul, string penulis) {
        Buku* baru = new Buku{isbn, judul, penulis, nullptr};
        if (kosong()) {
            head = baru;
        } else {
            Buku* temp = head;
            while (temp->next) temp = temp->next;
            temp->next = baru;
        }
        cout << "✅ Buku berhasil ditambahkan!\n";
    }

    void tampil() {
        if (kosong()) {
            cout << "📭 Tidak ada data buku.\n";
            return;
        }
        cout << "\n📚 Daftar Buku:\n";
        for (Buku* t = head; t; t = t->next) {
            cout << "ISBN    : " << t->isbn << "\n";
            cout << "Judul   : " << t->judul << "\n";
            cout << "Penulis : " << t->penulis << "\n";
            cout << "-------------------------\n";
        }
    }

    void hapus(string isbn) {
        if (kosong()) {
            cout << "⚠️ Daftar buku kosong.\n";
            return;
        }
        Buku* temp = head;
        Buku* prev = nullptr;
        while (temp && temp->isbn != isbn) {
            prev = temp;
            temp = temp->next;
        }
        if (!temp) {
            cout << "❌ Buku tidak ditemukan.\n";
            return;
        }
        if (!prev) head = head->next;
        else prev->next = temp->next;
        delete temp;
        cout << "🗑️ Buku berhasil dihapus!\n";
    }

    void perbarui(string isbn) {
        Buku* temp = head;
        while (temp && temp->isbn != isbn) temp = temp->next;
        if (!temp) {
            cout << "❌ Buku tidak ditemukan.\n";
            return;
        }
        cout << "Masukkan judul baru: ";
        getline(cin, temp->judul);
        cout << "Masukkan penulis baru: ";
        getline(cin, temp->penulis);
        cout << "✅ Data buku diperbarui!\n";
    }

    void cariISBN(string isbn) {
        Buku* t = head;
        while (t && t->isbn != isbn) t = t->next;
        if (!t) {
            cout << "❌ Buku tidak ditemukan.\n";
            return;
        }
        cout << "\n📗 Buku ditemukan:\n";
        cout << "ISBN    : " << t->isbn << "\n";
        cout << "Judul   : " << t->judul << "\n";
        cout << "Penulis : " << t->penulis << "\n";
    }

    void cariJudul(string judul) {
        Buku* t = head;
        bool ada = false;
        while (t) {
            if (t->judul == judul) {
                if (!ada) cout << "\n📕 Buku dengan judul \"" << judul << "\" ditemukan:\n";
                cout << "ISBN    : " << t->isbn << "\n";
                cout << "Penulis : " << t->penulis << "\n";
                cout << "-------------------------\n";
                ada = true;
            }
            t = t->next;
        }
        if (!ada) cout << "❌ Buku tidak ditemukan.\n";
    }

    void cariPenulis(string penulis) {
        Buku* t = head;
        bool ada = false;
        while (t) {
            if (t->penulis == penulis) {
                if (!ada) cout << "\n📘 Buku karya \"" << penulis << "\" ditemukan:\n";
                cout << "ISBN  : " << t->isbn << "\n";
                cout << "Judul : " << t->judul << "\n";
                cout << "-------------------------\n";
                ada = true;
            }
            t = t->next;
        }
        if (!ada) cout << "❌ Buku tidak ditemukan.\n";
    }
};

int main() {
    LinkedList daftar;
    int pilihan;
    string isbn, judul, penulis;

    do {
        cout << "\n=== 📚 MENU DATA BUKU ===\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku\n";
        cout << "3. Perbarui Buku\n";
        cout << "4. Lihat Semua Buku\n";
        cout << "5. Cari ISBN\n";
        cout << "6. Cari Judul\n";
        cout << "7. Cari Penulis\n";
        cout << "8. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                cout << "Masukkan Judul: "; getline(cin, judul);
                cout << "Masukkan Penulis: "; getline(cin, penulis);
                daftar.tambah(isbn, judul, penulis);
                break;
            case 2:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                daftar.hapus(isbn);
                break;
            case 3:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                daftar.perbarui(isbn);
                break;
            case 4:
                daftar.tampil();
                break;
            case 5:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                daftar.cariISBN(isbn);
                break;
            case 6:
                cout << "Masukkan Judul: "; getline(cin, judul);
                daftar.cariJudul(judul);
                break;
            case 7:
                cout << "Masukkan Penulis: "; getline(cin, penulis);
                daftar.cariPenulis(penulis);
                break;
            case 8:
                cout << "👋 Program selesai.\n";
                break;
            default:
                cout << "❌ Pilihan tidak valid!\n";
        }
    } while (pilihan != 8);

    return 0;
}

```
Program ini membuat sistem data buku dengan singly linked list. Setiap node menyimpan ISBN, judul, penulis, dan alamat buku berikutnya. Variabel head menandai awal data. Ada fungsi untuk menambah buku ke akhir list, menampilkan semua buku, menghapus buku berdasarkan ISBN, memperbarui data buku, serta mencari buku berdasarkan ISBN, judul, atau penulis. Program utama menggunakan menu agar pengguna dapat memilih operasi yang diinginkan.


> Output
> ![Screenshot bagian x](ssmodul5unguided2.png)


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
