#### Enumerasi dan Struktur

Gunakan `enum` untuk pembinaan enumerasi(*enumeration*). Seperti kelas dan jenis-jenis bernama lain, enumerasi boleh memiliki kaedah yang berkaitan dengan mereka.

```swift
enum Pangkat: Int {
    case Ace = 1
    case Dua, Tiga, Empat, Lima, Enam, Tujuh, Lapan, Sembian, Sepuluh
    case Jack, Queen, King
    func deskripsiMudah() -> String {
        switch self {
        case .Ace:
            return "ace"
        case .Jack:
            return "jack"
        case .Queen:
            return "queen"
        case .King:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.Ace
let nilaiMentahAce = ace.rawValue
```

> Eksperimen: Tuliskan fungsi yang memperbezakan nilai dua `Pangkat` berbeza dengan membandingkan nilai mentah mereka.

Swift menetapkan nilai mentah dari kosong dan menambahkan satu setiap kali secara lalai, tapi anda boleh mengubah kelakuan tersebut dengan menjelaskan nilainya. Dalam contoh yang diberi, `Ace` jelasnya diberi nilai mentah `1` dan nilai-nilai mentah lain ditetapkan secara tertib. Anda juga boleh gunakan perkataaan atau nombor *floating-point* sebagai nilai mentah bagi sebuah enumerasi. Gunakan sifat `rawValue` untuk mendapatkan nilai mentah sebuah kes enumerasi.

Gunakan pengasal `init?(rawValue:)` untuk pembinaan sebuah tentuan bagi sebuah enumerasi dari nilai mentahnya.

```swift
if let rangkaDitukarkan = Rank(rawValue: 3) {
    let deskripsiTiga = rangkaDitukarkan.deskripsiMudah()
}
```

Nilai-nilai kes sebuah enumerasi merupakan nilai sebenarnya dan bukan sahaja cara berlainan untuk penulisan nilai mentahnya. Malahnya, anda tidak perlu memberikannya dalam kes di mana ketiadaan nilai mentah yang bermakna.

```swift
enum Sut {
    case Spades, Hearts, Diamonds, Clubs
    func deskripsiMudah() -> String {
        switch self {
        case .Spades:
            return "spades"
        case .Hearts:
            return "hearts"
        case .Diamonds:
            return "diamonds"
        case .Clubs:
            return "clubs"
        }
    }
}
let hearts = Sut.hearts
let deskripsiHeart = hearts.deskripsiMudah()
```

> Eksperimen: Tambahkan kaedah `warna()` kepada `Sut` yang pulangkan "hitam" untuk *spades* dan *clubs*, dan pulangkan "merah" untuk *hearts* dan *diamonds*.

Lihatlah kedua-dua cara kes `Hearts` enumerasi di atas dirujukkan: Apabila menetapkan sebuah nilai kepada nilai malar `hearts`, kes enumerasi `Sut.Hearts` dirujukkan dengan nama penuh kerana nilai malar tersebut tidak memiliki sebuah jenis jelas yang nyata. Dalam *switch*, kes enumerasi tersebut dirujukkan dengan singkatan `.Hearts` kerana nilai `self` dahlah dikenalpasti sebagai sebuah sut. Anda boleh menggunakan singkatan apabila jenis nilai dah dikenalpasti.

Gunakan `struct` untuk pembinaan struktur. Struktur menyokong pelbagai tingkah laku yang sama dengan kelas, termasuknya kaedah dan pengasal. Perbezaan terpenting antara struktur dan kelas adalah bahawa struktur akan sentiasa disalin apabila mereka diedarkan dalam kod anda tetapi kelas diedarkan secara rujukan.

```swift
struct Kad {
    var pangka: Pangka
    var sut: Sut
    func deskripsiMudah() -> String {
        return "The \(pangka.deskripsiMudah()) of \(sut.deskripsiMudah())"
    }
}
let threeOfSpades = Kad(pangka: .Three, sut: .Spades)
let deskripsiThreeOfSpades = threeOfSpades.deskripsiMudah()
```

> Eksperimen: Tambahkan kaedah kepada `Kad` yang membinakan dek kad penuh, dengan sebuah kad untuk setiap kombinasi rangka dan sut.

Tentuan sebuah kes enumerasi boleh mengandungi nilai yang berkaitan dengan tentuan tersebut. Tentuan kes enumerasi yang sama boleh memiliki nilai-nilai berbeza yang berkaitan dengan mereka. Anda memberikan nilai-nilai berkaitan apabila anda membinakan tentuan tersebut. Nilai-nilai berkaitan dan nilai-nilai mentah berbeza: Nilai mentah sebuah kes enumerasi adalah sama untuk kesemuaan tentuannya, dan anda boleh memberikan nilai mentah apabila anda menentukan enumerasi tersebut.

Sebagai contoh, bayangkan kes meminta masa kenaikan matahari dan masa matahari terbenam dari sebuah pelayan. Pelayan tersebut sama ada maklum balas dengan maklumat berkenaan atau ia maklum balas dengan maklumat ralat.

```swift
enum MaklumBalasPelayan {
    case Keputusan(String, String)
    case Kegagalan(String)
}

let kejayaan = MaklumBalasPelayan.Keputusan("6:00 am", "8:09 pm")
let kegagalan = MaklumBalasPelayan.Kegagalan("Kehabisan keju.")

switch kejayaaan {
case let .Keputusan(kenaikanMatahari, matahariTerbenam):
    print("Masa kenaikan matahari adalah pada \(kenaikanMatahari) dan masa matahari terbenam adalah pada \(matahariTerbenam).")
case let .Kegagalan(mesej):
    print("Kegagalan... \(mesej)")
}
```

> Eksperimen: Tambahkan kes ketiga kepada `MaklumBalasPelayan` dan kepada *switch* tersebut.

Lihatlah bagaimana masa kenaikan matahari dan masa matahari terbenam dikeluarkan dari nilai `MaklumBalasPelayan` sebagai bahagian yang memadankan nilai terhadap kes *switch*.
