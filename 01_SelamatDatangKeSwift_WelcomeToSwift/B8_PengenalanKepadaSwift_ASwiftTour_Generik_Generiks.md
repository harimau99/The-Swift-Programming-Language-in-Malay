#### Generik

Tuliskan sebuah nama dalam kurungan sudut untuk pembinaan fungsi generik atau jenis generik.

```swift
func ulangiItem<Item>(item: Item, nomborKali: Int) -> [Item] {
    var keputusan = [Item]()
    for _ in 0..<nomborKali {
        keputusan.append(item)
    }
    return keputusan
}
ulangiItem("knock", nomborKali: 4)
```

Anda boleh binakan fungsi dan kaedah yang berbentuk generik disertakan dengan kelas, enumerasi dan struktur.

```swift
// Pengimplemen semula jenis *optional* dari Swift *library* standard
enum NilaiOptional<Dibungkus> {
    case None
    case Some(Dibungkus)
}
var kemungkinanSebuahInteger: NilaiOptional<Int> = .None
kemungkinanSebuahInteger = .Some(100)
```

Gunakan `where` selepas jenis nama untuk menentukan senarai keperluan - contohnya untuk memerlukan sebuah jenis mematuhi sebuah protokol, untuk memerlukan jenis bagi dua jenis berlainan agar sama atau memerlukan sebuah kelas untuk memiliki sebuah kelas yang diwarisinya yang tertentu.

```swift
func wujudkahElemenBiasa <T: SequenceType, U: SequenceType where T.Generator.Element: Equatable, T.Generator.Element == U.Generator.Element>(dariKiri: T, _ dariKanan: U) -> Bool {
    for itemDariKiri in dariKiri {
        for itemDariKanan in dariKanan {
            if itemDariKiri == itemDariKanan {
                return true
            }
        }
    }
    return false
}
wujudkahElemenBiasa([1, 2, 3], [3])
```

> Eksperimen: Ubahkan fungsi `wujudkahElemenBiasa(_:_:)` supaya fungsi tersebut memulangkan sebuah *array* yang mengandungi elemen yang sama dimiliki mana-mana dua urutan(*sequences*).

Penulisan `<T: Equatable>` adalah sama dengan penulisan `<T where T: Equatable>`.
