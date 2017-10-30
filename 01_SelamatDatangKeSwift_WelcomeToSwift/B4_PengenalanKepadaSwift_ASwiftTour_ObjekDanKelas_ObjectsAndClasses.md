#### Objek dan Kelas

Gunakan `class` disampingkan nama kelas untuk pembinaan sebuah kelas. Pengisytiharan sifat(*property*) di dalam kelas ditulis dengan cara biasa, tetapi konteksnya dalam sebuah kelas. Begitu juga bagi pengisytiharan kaedah(*method*) dan pengisytiharan fungsi.

```swift
class Bentuk {
    var nomborSisi = 0
    func deskripsiMudah() -> String {
        return "Bentuk dengan \(nomborSisi) sisi."
    }
}
```

> Eksperimen: Tambahkan nilai malar dengan `let` dan tambahkan kaedah yang menerima sebuah argumen

Binakan sebuah tentuan(*instance*) kelas dengan meletakkan kurungan selepas nama kelas. Gunakan sintaks titik untuk akses sifat and kaedah tentuan tersebut.

```swift
var bentuk = Bentuk()
bentuk.nomborSisi = 7
var deskripisiBentuk = bentuk.deskripsiMudah()
```

Versi kelas `Bentuk` ini kehilangan sesuatu penting: sebuah pengasal(*initializer*) untuk menubuhkan kelas tersebut semasa sebuah tentuan dibina. Gunakan `init` untuk membina satu.

```swift
class BentukDinamakan {
    var nomborSisi: Int = 0
    var nama: String

    init(nama: String) {
        self.nama = nama
    }

    func deskripsiMudah() -> String {
        return "Bentuk dengan \(nomborSisi) sisi."
    }
}
```

Lihatlah bagaimana `self` digunakan untuk membezakan sifat `nama` dari argumen `nama` kepada pengasal. Argumen bagi pengasal adalah dihantarkan seperti panggilan fungsi apabila anda membina sebuah tentuan kelas. Setiap sifat mesti ditetapkan nilai - sama ada dalam pengisytiharan (seperti dengan `nomborSisi`) atau dalam pengasal (seperti dengan `nama`).

Gunakan `deinit` untuk membina sebuah *deinitializer* jika anda perlu melaksanakan kerja pembersihan sebelum objek tersebut dibuang.

Subkelas memasukkan nama kelas yang diwarisi(*superclass*) selepas nama kelas sendiri, dipisahkan dengan kolon. Tidak wujudnya keperluan bagi kelas untuk mewarisi apa-apa kelas akar(*root*) standard, jadi anda boleh memasukkan atau meninggalkan kelas yang diwarisi berdasarkan keperluan.

Kaedah sebuah subkelas yang mengatasi implementasi kelas yang diwarisinya ditanda dengan `override` - jika sebuah kaedah diatasi dengan sengaja, tanpa `override`, ia akan dikesan oleh pengkompil sebagai sebuah ralat. Pengkompil juga mengesan kaedah dengan `override` yang tidak mengatasi apa-apa kaedah dalam kelas yang diwarisinya.

```swift
class Persegi: BentukDinamakan {
    var panjangSisi: Double

    init(panjangSisi: Double, nama: String) {
        self.panjangSisi = panjangSisi
        super.init(nama: nama)
        nomborSisi = 4
    }

    func kawasan() -> Double {
        return panjangSisi * panjangSisi
    }

    override func deskripsiMudah() -> String {
        return "Persegi dengan panjang sisi \(panjangSisi)."
    }
}
let cuba = Persegi(panjangSisi: 5.2, name: "Persegi Cubaan")
cuba.kawasan()
cuba.deskripsiMudah()
```

> Eksperimen: Binakan sebuah subkelas `BentukDinamakan` yang dipanggil `Bulatan` yang mengambilkan sebuah radius dan nama sebagai argumen pengasalnya. Implemen kaedah `kawasan()` dan `deskripsiMudah()` untuk kelas `Bulatan` tersebut.

Di samping sifat mudah yang disimpan, sifat juga boleh mengandungi sebuah pengambil(*getter*) dan penetap(*setter*).

```swift
class SegiTigaSamaSisi: BentukDinamakan {
    var panjangSisi: Double = 0.0

    init(panjangSisi: Double, nama: String) {
        self.panjangSisi = panjangSisi
        super.init(nama: nama)
        nomborSisi = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * panjangSisi
        }
        set {
            panjangSisi = newValue / 3.0
        }
    }

    override func deskripsiMudah() -> String {
        return "Segi Tiga Sama Sisi dengan panjang sisi \(panjangSisi)."
    }
}
var segiTiga = SegiTigaSamaSisi(panjangSisi: 3.1, nama: "sebuah segi tiga")
print(segiTiga.perimeter)
segiTiga.perimeter = 9.9
print(segiTiga.panjangSisi)
```

Dalam penetap bagi `perimeter`, nilai barunya memiliki nama tersirat `newValue`(*`nilaiBaru`*). Anda boleh memberikan nama jelas dalam kurungan selepas `set`.

Lihatlah bagaimana pengasal `SegiTigaSamaSisi` memiliki tiga langkah berbeza:

1. Penetapan nilai sifat yang diisytiharkan oleh subkelas.
2. Panggilan pengasal kelas yang diwarisinya.
3. Penukaran nilai sifar yang ditakrifkan oleh kelas yang diwarisinya. Apa jua kerja persediaan yang menggunakan kaedah, pengambil atau penetap pun boleh dibuat pada ketika ini.

Kalau anda tidak perlu mengirakan sifat tetapi anda perlu memberikan kod yang dijalankan sebelum dan selepas penetapan nilai baharu, gunakan `willSet`(*`akanMenetap`*) dan `didSet`(*`dahDitetapkan`*). Kod tersebut yang diberi akan dilancarkan ketika perubahan nilai di luar pengasal. Sebagai contoh, kelas berikut memastikan panjang sisi segi tiganya sentiasa sama dengan panjang sisi perseginya.

```swift
class SegiTigaSamaSisi {
    var segiTiga: SegiTigaSamaSisi {
        willSet {
            persegi.panjangSisi = newValue.panjangSisi
        }
    }
    var persegi: Persegi {
        willSet {
            segiTiga.panjangSisi = newValue.panjangSisi
        }
    }
    init(saiz: Double, nama: String) {
        persegi = Persegi(panjangSisi: saiz, nama: nama)
        segiTiga = SegiTigaSamaSisi(panjangSisi: saiz, nama: nama)
    }
}
var segiTigaDanPersegi = SegiTigaSamaSisi(saiz: 10, nama: "satu lagi segi cubaan")
print(segiTigaDanPersegi.persegi.panjangSisi)
print(segiTigaDanPersegi.segiTiga.panjangSisi)
segiTigaDanPersegi.persegi = Persegi(panjangSisi: 50, nama: "persegi lebih besar")
print(segiTigaDanPersegi.segiTiga.panjangSisi)
```

Dengan nilai-nlai *optional*, anda boleh tuliskan `?` sebelum operasi seperti kaedah, sifat dan *subscripting*. Jika nilai sebelum `?` adalah `nil`, kesemuaan selepas `?` diabaikan dan nilai keseluruhan ekspresi adalah `nil`. Jika tidak, nilai *optional* tersebut dibukakan dan kesemuaan selepas `?` bertindak ke atas nilai yang dibukakan. Dalam kedua-dua kes, nilai keseluruhan ekspresi tersebut ialah nilai *optional*.

```swift
let persegiOptional: Persegi? = Persegi(panjangSisi: 2.5, nama "persegi optional")
let panjangSisi = persegiOptional?.panjangSisi
```
