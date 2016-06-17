#### Protokol dan Extension

Gunakan `protocol` untuk pengisytiharan sebuah protokol.

```swift
protocol ContohProtokol {
    var deskripsiMudah: String { get }
    mutating func laraskan()
}
```

Kelas, enumerasi dan struktur boleh menerima pakai protokol.

```swift
class KelasMudah: ContohProtokol {
    var deskripsiMudah: String = "Kelas yang amat mudah."
    var sifatLain: Int = 69105
    func laraskan() {
        deskripsiMudah += " Sekarag dilaraskan 100%."
    }
}
var a = KelasMudah()
a.laraskan()
let deskripsiA = a.deskripsiMudah

struct StrukturMudah: Contoh Protocol {
    var deskripsiMudah: String = "Struktur mudah."
    mutating func laraskan() {
        deskripsiMudah += " (dilaraskan)"
    }
}
var b = StrukturMudah()
b.laraskan()
let deskripsiMudah = b.deskripsiMudah()
```

> Eksperimen: Tuliskan sebuah enumerasi yang mematuhi protokol tersebut.

Lihatlah bagaimana kegunaan kata kunci `mutating` dalam pengisytiharan `StrukturMudah` digunakan untuk memnandakan sebuah kaedah yang mengubahkan struktur tersebut. Pengisytiharan `KelasMudah` tidak memerlukan mana-mana kaedahnya ditanda sebagai pengubah kerana kaedah sebuah kelas bolehlah sentiasa mengubah kelas tersebut.

Gunakan `extension` untuk tambahan kebolehan kepada jenis yang sedia ada, seperti kaedah baru dan sifat dikira. Anda boleh gunakan sebuah *extension* untuk tambahan pematuhan protokol kepada satu jenis yang diisytiharkan pada tempat lain atau juga pada satu jenis yang diimport dari sebuah *library* atau *framework*.

```swift
extension Int: ContohProtokol {
    var deskripsiMudah: String {
        return "Nombor \(self)"
    }
    mutating func laraskan() {
        self += 42
    }
}
print(7.deskripsiMudah)
```

> Eksperimen: Tuliskan sebuah *extension* untuk jenis `Double` yang tambahkan sebuah sifat `nilaiMutlak` (*`absoluteValue`*)

Anda boleh gunakan nama protokol seperti nama jenis-jenis lain - contohnya pembinaan koleksi objek yang memiliki jenis berlainan tetapi semuanya mematuhi sebuah protokol. Apabila anda mengunakan nilai yang jenisnya sebuah protokol, kaedah di luar definisi protokol tidak sedia ada.

```swift
let nilaiProtokol: ProtokolContoh = a
print(nilaiProtokol.deskripsiMudah)
// print(nilaiProtokol.sifatLain) // Keluarkan komen untuk melihat ralat
```

Walaupun pemboleh ubah *nilaiProtokol* memiliki jenis *runtime* `KelasMudah`, pengkompil melayannya sebagai jenis `ContohProtokol`. Ini bermakna bahawa anda tidak boleh mengakses kaedah dan sifat kelas tersebut di samping pematuhan protokolnya dengan sengaja.
