#### Pengendalian Ralat

Anda mewakilkan ralat dengan jenis yang mematuhi protokol `ErrorType`.

```swift
enum RalatMesinPencetak: ErrorType {
    case KehabisanHelaiKertas
    case KetiadaanToner
    case Bakaran
}
```

Gunakan `throw` untuk pembuangan ralat dan `throws` untuk menandakan sebuah fungsi yang boleh membuang sebuah ralat. Kalau anda membuangkan sebuah ralat dalam sebuah fungsi, fungsi tersebut akan pulang segera dan kod yang memanggil fungsi tersebut akan mengendalikan ralat tersebut.

```swift
func beriKepadaMesinPencetak(nameMesinPencetak: String) throws -> String {
    if namaMesinPencetak == "SentiasaKetiadaanToner" {
        throw RalatMesinPencetak.KetiadaanToner
    }
    return "Kerja diberikan"
}
```

Terdapat pelbagai cara untuk pengendalian ralat. Satu cara ialah pengunaan `do-catch`. Dalam sebuah blok `do`, anda tandakan kod yang boleh membuang sebuah ralat dengan penulisan `try` di hadapannya. Dalam blok `catch`, ralat tersebut diberikan nama `error` dengan secara automatik tetapi anda boleh memberikan ia nama berlainan.

```swift
do {
    let tindakBalasMesinPencetak = try beriKepadaMesinPencetak("Bi Sheng")
    print(tindakBalasMesinPencetak)
} catch {
    print(error)
}
```

> Eksperimen: Tukarkan nama mesin pencetak kepada "SentiasaKetiadaanToner" supaya fungsi `beriKepadaMesinPencetak(_:)` membuangkan sebuah ralat.

Anda boleh memberikan pelbagai blok `catch` yang mengendalikan ralat tertentu. Anda menuliskan sebuah corak selepas `catch` sama seperti selepas `case` dalam *switch*.

```swift
do {
    let tindakBalasMesinPencetak = try beriKepadaMesinPencetak("Gutenberg")
    print(tindakBalasMesinPencetak)
} catch RalatMesinPencetak.Bakaran {
    print("Saya akan meletakannya di sana dengan bakaran di situ.")
} catche let ralatMesinPencetak as RalatMesinPencetak {
    print("Ralat mesin pencetak: \(ralatMesinPencetak)")
} catch {
    print(error)
}
```

> Eksperimen: Tambahkan kod untuk membuangkan sebuah ralat dalam blok `do` tersebut. Apakah jenis ralat yang anda perlu membuangkan supaya ralat tersebut dikendalikan oleh `catch` blok pertama? Bagaimana pula dengan blok kedua dan blok ketiga?

Satu cara lagi untuk mengendali ralat adalah pengunaan `try?` untuk menukarkan keputusan kepada sebuah *optional*. Kalau fungsi tersebut membuangkan ralat, ralat tertentu tersebut dibuang dan nilai keputusan tersebut adalah `nil`. Jika tidak, keputusan tersebut ialah sebuah *optional* yang mengandungi nilai yang fungsi tersebut memulangkan.

```swift
let kejayaanMesinPencetak = try? beriKepadaMesinPencetak("Mergenthaler")
let kegagalanMesinPencetak = try? beriKepadaMesinPencetak("SentiasaKetiadaanToner")
```

Gunakan `defer` untuk penulisan sebuah blok kod yang akan dilaksanakan selepas keseluruhan kod lain dalam fungsi tersebut dan sebelum pemulangan fungsi tersebut. Kod ini akan dilaksanakan tidak kira sama ada fungsi tersebut membuangkan sebuah ralat. Anda boleh gunakan `defer` untuk penulisan kod persediaan dan kod pembersihan bersebelahan walaupun mereka perlu dilaksanakan pada masa berlainan.

```swift
var petiSejukTerbuka = false
var kandunganPetiSejuk = ["susu", "telur", "lebihan"]

func petiSejukMengandungi(namaItem: String) -> Bool {
    petiSejukTerbuka = true
    defer {
        petiSejukTerbuka = false
    }

    let keputusan = kandunganPetiSejuk.contains(namaItem)
    return keputusan
}
petiSejukMengandungi("banana")
print(petiSejukTerbuka)
```
