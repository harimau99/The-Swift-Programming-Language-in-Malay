#### Fungsi-Fungsi dan *Closure*

Gunakan `func` untuk mengisytiharkan sebuah fungsi. Isytiharkan sebuah fungsi dengan namanya disampingkan senarai argumen dalam kurungan. Gunakan `->` untuk mengasingkan nama *parameter* dan jenis-jenisnya dari jenis pulang fungsi.

```swift
func ucap(nama: String, hari: String) -> String {
  return "Hello \(nama), hari ini hari \(hari)."
}
ucap("Bob", hari: "Selasa")
```

> Eksperimen: Keluarkan *parameter* `hari`. Tambahkan *parameter* untuk mangandungi makanan tengah hari istimewa hari ini dalam ucapan.

Gunakan tupel untuk membina nilai kompaun - contohnya untuk memulangkan nilai-nilai dari fungsi. Elemen tupel boleh dirujukkan sama ada secara nama atau secara nombor.

```swift
func kiraanStatistik(markahSemua: [Int]) -> (min: Int, max: Int, jumlah: Int) {
    var min = markahSemua[0]
    var max = markahSemua[0]
    var jumlah = 0

    for markah in markahSemua {
        if markah > max {
            max = markah
        } else if markah < min {
            min = markah
        }
        jumlah += markah
    }

    return (min, max, jumlah)
}
let statistik = kiraanStatistik([5, 3, 100, 3, 9])
print(statistik.jumlah)
print(statistik.2)
```

Fungsi-fungsi juga boleh menerima beberapa pemboleh ubah dan mengumpulkan mereka ke dalam sebuah *array*.

```swift
func jumlah(nombor: Int...) -> Int {
    var jumlah = 0
    for n in nombor {
        jumlah += n
    }
    return jumlah
}
jumlah()
jumlah(42, 597, 12)
```

> Eksperimen: Tuliskan sebuah fungsi yang megirakan nilai purata argumennya

Fungsi-fungsi boleh disarangkan. Fungsi tersarang memiliki akses kepada pemboleh ubah yang telah diisytiharkan pada fungsi luar. Anda boleh gunakan fungsi tersarang untuk menyusun kod dalam fungsi yang panjang atau kompleks.

```swift
func pulangkanLimaBelas() -> Int {
    var y = 10
    func tambah() {
        y += 5
    }
    tambah()
    return y
}
pulangkanLimaBelas()
```

Fungsi-fungsi merupakan jenis kelas utama. Ini bermakna sebuah fungsi boleh memulangkan sebuah fungsi lain sebagai nilainya.

```swift
func binaTambahan() -> ((Int) -> Int) {
    func tambahSatu(nombor: Int) -> Int {
        return 1 + nombor
    }
    return tambahSatu
}
var tambah = binaTambahan()
tambah(7)
```

Sebuah fungsi boleh menerimakan sebuah fungsi lain bagai argumennya.

```swift
func adaPadanan(senarai: [Int], keadaan: (Int) -> Bool) -> Bool {
    for item in senarai {
        if keadaaan(item) {
            return true
        }
    }
    return false
}
func kurangDariSepuluh(nombor: Int) -> Bool {
    return nombor < 10
}
var nombor = [20, 19, 7, 12]
adaPadanan(nombor, keadaan: kurangDariSepuluh)
```

Fungsi-fungsi merupakan jenis kes *closure* khas: blok kod yang boleh dipanggil kemudian. Kod dalam sebuah *closure* memiliki akses kepada pemboleh ubah dan fungsi-fungsi yang siap sedia pada skop *closure* tersebut dibina, walaupun *closure* tersebut berada di dalam skop berlainan apabila ia dilaksanakan - anda dah melihat sebuah contoh ini dengan fungsi-fungsi tersarang. Anda boleh menulis sebuah *closure* tanpa sebuah nama di sekitar kod dengan pendakap (`{}`). Guna `in` untuk mengasingkan argumen dan jenis pulang dari badannya.

```swift
nombor.map({
    (n: Int) -> Int in
    let keputusan = 3 * n
    return keputusan
})
```

> Eksperimen: Tuliskan semula *closure* tersebut untuk memulangkan nilai kosong untuk nombor ganjil

Terdapat beberapa pilihan bagi anda untuk menuliskan *closure* dengan lebih ringkas. Apabila jenis *closure* dah dikenalpasti, seperti panggil balik sebuah perwakilan(*delegate*), anda boleh meninggalkan jenis *parameter*, jenis pulang atau kedua-duanya. *Closure* penyata tunggal memulangkan nilai dalam penyatanya dengan tersirat.

```swift
let nomborDitukarkan = nombor.map({ n in 3 * n })
print(nomborDitukarkan)
```

Anda juga boleh merujukkan kepada *parameter* dengan nombor - cara ini lebih berguna untuk *closure* yang amat pendek. Sebuah *closure* yang diserahkan sebagai argumen terakhir sebuah fungsi boleh muncul serta-merta selepas kurungan. Apabila sebuah *closure* merupakan *argumen* tunggal sebuah fungsi, anda boleh meninggalkan kurungan fungsi tersebut.

```swift
let nomborDisusun = nombor.sort { $0 > $1 }
print(nomborDisusun)
```
