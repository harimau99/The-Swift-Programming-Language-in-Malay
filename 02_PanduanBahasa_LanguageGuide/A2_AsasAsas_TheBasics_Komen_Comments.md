#### Komen

Gunakan komen untuk memasukkan teks dalam kod anda yang tidak akan dilancarkan, sebagai sebuah nota atau sebuah peringatan bagi anda sendiri. Komen diabaikan oleh pengkompil Swift apabila kod anda dikompilkan.

Komen dalam Swift adalah amat sama dengan komen dalam C. Komen sebaris bermula dengan dua garis condong hadapan (`//`).

```swift
// ini merupakan sebuah komen
```

Komen berbilang baris dimulakan dengan sebuah garis condong hadapan disampingkan sebuah asterisk (`/*`) dan berakhir dengan sebuah asterisk disampingkan sebuah garis condong hadapan (`*/`).

```swift
/* ini juga merupakan sebuah komen
 tetapi ia dituliskan secara berbilang baris */
```

Komen berbilang baris dalam Swift tidak sama dengan komen berbilang baris dalam C kerana ia boleh disarangkan di dalam komen berbilang baris lain. Anda tuliskan komen yang disarangkan bermula dengan blok komen berbilang baris dan kemudian memulakan sebuah komen berbilang baris kedua dalam blok pertama. Blok kedua kemudian ditutup disampingkan blok pertama.

```swift
/* di sinilah permulaaan komen berbilang baris pertama
 /* ini merupakan komen berbilang baris kedua yang disarangkan */
 di sinilah akhir komen berbilang baris pertama */
```

Komen berbilang baris membolehkan pembinaan komen blok kod besar dengan cepat dan mudah walaupun kod tersebut mengandungi komen berbilang baris.
