#### Aliran Kawalan

Gunakan `if`(*kalau*) dan `switch`(*tukar*) untuk pembinaan keadaan dan gunakan `for-in`(*untuk-dalam*), `for`(*untuk*), `while`(*sehingga*) dan `repeat-while`(*ulang-sehingga*) untuk membina *loops*. Kurungan sekitar pemboleh ubah boleh digunakan. Pendakap sekitar badan diperlukan.

```swift
let markahIndividu = [75, 43, 103, 87, 12]
var markahPasukan = 0
for markah in markahIndividu {
    if markah > 50 {
        markahPasukan += 3
    } else {
        markahPasukan += 1
    }
}
print(markahPasukan)
```

Dalam sebuah keadaan `if`, keadaan tesebut mesti merupakan ungkapan *Boolean* - ini bermakna kod seperti `if markah { ... }` adalah ralat dan tidak merupakan perbandingan tersirat kepada nilai kosong.

Anda boleh menggunakan `if` dan `let` bersama untuk nilai-nilai yang mungkin hilang. Nilai-nilai tersebut diwakili sebagai *optionals*. Nilai *optionals* sama ada mengandungi sesuatu nilai atau mengandungi `nil` yang mewakili nilai hilang. Tuliskan tanda tanya (`?`) selepas jenis nilai untuk mewakilkan nilai tersebut sebagai nilai *optional*.

```swift
var perkataanOptional: String? = "Hello"
print(perkataanOptional == nil)

var namaOptional: String? = "John Appleseed"
var ucapan = "Hello!"
if let nama = namaOptional {
    ucapan = "Hello, \(nama)"
}
```

> Eksperimen: Tukaran `namaOptional` kepada `nil`. Apakah ucapan yang anda menerima? Tambahkan fasal `else` yang menetapkan ucapan berbeza jika nilai `namaOptional` adalah `nil`.

Kalau nilai *optional* tersebut adalah *nil*, keadaan tersebut adalah `false`(*salah*) dan kod dalam pendakap tersebut dilangkau. Jika tidak, nilai *optional* tersebut akan dibukakan dan diberikan kepada nilai malar selepas `let` yang jadikan kandungan nilai terbuka tersebut tersedia dalam blok kod tersebut.

Satu cara lagi untuk mengendalikan nilai-nilai *optional* adalah untuk memberikan nilai lalai dengan operator `??`. Kalau nilai *optional* tersebut hilang, nilai lalai akan digunakan sebaliknya.

```swift
let namaSamaran: String? = nil
let namaPenuh = String = "John Appleseed"
let ucapanTidakRasmi = "Hi \(namaSamaran ?? namaPenuh)"
```

Keadaaan `switch` menyokong pelbagai jenis data dan pelbagai operasi perbandingan - ia tidak terhad kepada integer dan perbandingan persamaaan.

```swift
let sayur = "lada merah"
switch sayur {
case "saderi":
    print("Tambahkan beberapa kismis dan semut pada kayu pokok.")
case "timun", "selada air":
    print("Itu boleh dijadikan teh sandwic bagus.")
case let x where x.hasPrefix("lada"):
    print("Adakah ia \(x) yang pedas?")
default:
    print("Semuanya rasa bagus dalam sup.")
}
```

> Eksperimen: Cuba keluarkan kes lalai(*default*). Apakah ralat yang anda menerima?

Lihatlah bagaimana `let` boleh digunakan dalam corak untuk menetapkan nilai yang dipadankan corak kepada sebuah nilai malar.

Selepas melaksanakan kod di dalam kes `switch` yang padan, aturcara tersebut akan keluar dari penyata `switch`. Pelaksanaan tidak beterus kepada kes selepasnya, jadi tidak perlulah jelaskan keluaran dari pertukaran pada akhir kod setiap kes.

Anda gunakan `for-in` untuk melelar item dalam sebuah *dictionary*(kamus) dengan memberikan sepasang nama untuk kegunaan setiap pasang *key-value*(kunci bersama nilai). *Dictionaries* merupakan koleksi tidak tertib, jadi kunci dan nilai-nilai mereka dilelar sewenang-wenangnya.

```swift
let nomborMenarik = [
    "Perdana": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Persegi": [1, 4, 9, 16, 25],
]
var terbesar = 0
for (jenisNombor, nomborNombor) in nomborMenarik {
    for nombor in jenisNombor {
        if nombor > terbesar {
            terbesar = nombor
        }
    }
}
print(terbesar)
```

> Eksperimen: Tambahkan pemboleh ubah baru untuk merekodkan jenis nombor terbesar, di samping nombor terbesar.

Gunakan `while` untuk mengulangi sebuah blok kod sehingga keadaan bertukar. Sebaliknya keadaan sebuah *loop* boleh diletakkan pada akhir, memastikan *loop* tersebut dilaksanakan sekurang-kurangnya sekali.

```swift
var n = 2
while n < 100 {
    n = n * 2
}
print(n)

var m = 2
repeat {
    m = m * 2
} while m < 100
print(m)
```

Anda boleh meletakkan sebuah indeks untuk sebuah *loop* dengan menggunakan `..<` untuk membina sejulat indeks.

```swift
var jumlah = 0
for i in 0..<4 {
    jumlah += i
}
print(jumlah)
```

Gunakan `..<` untuk pembinaan julat yang meninggalkan nilai atasnya dan gunakan `...` untuk pembinaaan julat yang termasuk kedua-dua nilai.
