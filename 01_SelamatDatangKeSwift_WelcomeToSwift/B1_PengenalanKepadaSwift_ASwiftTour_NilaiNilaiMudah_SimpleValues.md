#### Nilai-nilai Mudah

Gunakan `let` untuk nilai-nilai malar/tetap dan `var` untuk nilai-nilai pemboleh ubah. Nilai sebuah nilai malar tidak perlu dikenalpasti semasa kompilasi, tetapi nilainya harus ditetapkan sekali. Ini bermakna bahawa anda boleh menggunakan nilai-nilai malar untuk pembinaan sebuah nilai yang anda akan tentukan sekali sahaja tetapi ia boleh digunakan di ramai lokasi.

```swift
var nilaiPembolehUbahKu = 42
nilaiPembolehUbahKu = 50
let nilaiMalarKu = 42
```

Nilai malar atau nilai pemboleh ubah mesti mempunyai jenis yang sama dengan nilai yang anda ingin menetapkan kepadanya. Walau bagaimanapun, anda tidak harus selalu menjelaskan jenis nilai tersebut. Pemberian sebuah nilai apabila anda membina sebuah nilai malar atau nilai pemboleh ubah membolehkan pengkompil merujukkan jenis nilai tersebut. Berdasarkan contoh di atas, pengkompil boleh merujukkan bahawa `nilaiPembolehUbahKu` merupakan sebuah integer kerana nilai asalnya sebuah integer.

Kalau nilai asal tidak memberikan maklumat yang cukup (atau jika ketiadaan nilai asal), jelaskan jenis nilai dengan menuliskan jenis nilai tersebut selepasnya, dipisahkan dengan sebuah kolon.

```swift
let integerTersirat = 70
let doubleTersirat = 70.0
let jelaskanJenisDouble: Double = 70
```

> Eksperimen: Binakan sebuah nilai malar dengan jenis nilai jelas `Float` dengan nilai `4`.

Nilai-nilai tidak akan sekali pun ditukarkan kepada jenis-jenis lain. Kalau anda perlu menukarkan nilai sesuatu kepada jenis lain, binalah sebuah ciptaan(*instance*) jenis tersebut dengan penjelasan.

```swift
let label = "Lebarnya ialah "
let lebar = 94
let labelLebar = label + String(lebar)
```

> Eksperimen: Cuba mengeluarkan pertukaran ke jenis `String` dari ayat terakhir di atas. Apakah ralat yang anda menerima?

Wujudnya cara lebih mudah untuk memasukkan nilai dalam perkataan: Tuliskan nilai tersebut dalam kurungan dan tuliskan sebuah garis sendeng terbalik (`\`) sebelum kurungan. Sebagai contoh:

```swift
let epal = 3
let oren = 5
let ringkasanEpal = "Saya ada \(epal) buah epal."
let ringkasanBuahBuahan = "Saya ada \(epal + oren) keping buah-buahan."
```

> Eksperimen: Gunakan `\()` untuk memasukkan pengiraan *floating-point* dalam satu perkataan dan memasukkan nama seseorang dalam sebuah ucapan.

Binakan *arrays* dan *dictionaries* dengan kurungan persegi (`[]`), dan akses elemen-elemen mereka dengan menuliskan indeks atau *key*(kunci) dalam kurungan persegi. Sebuah komma dibenarkan selepas elemen terakhir.

```swift
var senaraiBeliBelah = ["ikan keli", "air", "tulip", "cat biru"]
senaraiBeliBelah[1] = "botol air"

var perkerjaan = [
    "Malcolm": "Kapten",
    "Kaylee": "Mekanik",
]
perkerjaan["Jayne"] = "Hubungan Awam"
```

Untuk pembinaan *array* atau *dictionary* kosong, gunakan sintaks pengawalan.

```swift
let arrayKosong = [String]()
let dictionaryKosong = [String: Float]()
```

Kalau maklumat jenis boleh disimpulkan, anda boleh tuliskan sebuah *array* kosong sebagai `[]` dan sebuah *dictionary* kosong sebagai `[:]` - contohnya bila anda menetapkan nilai baru untuk nilai pemboleh ubah atau memberikan sebuah *parameter* kepada sebuah fungsi.

```swift
senaraiBeliBelah = []
perkerjaan = [:]
```
