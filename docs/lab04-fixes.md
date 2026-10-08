Lab 04 - Fix Log

1. MenuScreen (struktur halaman) mengalami overflow bawah 148 px saat keyboard terbuka atau layar landscape. Aturan yang dilanggar adalah Column meminta tinggi sebesar isinya, padahal parent hanya punya sisa ruang yang terbatas dan tidak ada yang bisa discroll. Perbaikannya, Column diganti menjadi CustomScrollView dengan slivers sehingga kelebihan tinggi bisa digulir.

2. MenuScreen (breakpoint tablet) membuat tampilan tablet hanya melebar tanpa mengubah layout. Penyebabnya, kode memakai MediaQuery yang membaca ukuran layar, bukan constraint yang diberikan parent, dan syaratnya > 600 padahal seharusnya >= 600. Perbaikannya memakai LayoutBuilder dengan constraints.maxWidth >= 600: lebar menjadi grid, di bawahnya menjadi list.

3. MenuScreen (list dan grid) membuat semua item dibangun sekaligus dengan jumlah kolom tetap 4. Aturan yang dilanggar adalah list yang panjangnya tidak dikontrol harus dibangun secara lazy. Perbaikannya memakai SliverList.builder dan SliverGrid.builder, dengan jumlah kolom 3 atau 4 mengikuti lebar layar.

4. MenuScreen (promo) bisa menyebabkan RangeError dan crash saat data kosong. Penyebabnya, kode mengira selalu ada dua promo lewat promos[0] dan promos[1]. Perbaikannya mengganti pemanggilan menjadi PromoStrip(items: promos).

5. PromoStrip mengalami overflow kanan di layar 320 dp dan bisa crash saat data kosong. Dua kartu lebar 200 dp ditambah jarak totalnya sekitar 416 dp, lebih besar dari lebar yang diberikan parent. Perbaikannya, widget menerima List, kalau kosong menampilkan SizedBox.shrink(), dan Row dibungkus scroll horizontal.

6. PromoCard memiliki teks yang bisa terpotong karena Text tidak punya maxLines dan strategi overflow. Perbaikannya menambahkan maxLines 1 atau 2 beserta ellipsis, sedangkan ukuran 200 x 150 bawaan file tidak diubah.

7. StoreHeader mengalami overflow kanan di 320 dp. Aturan yang dilanggar adalah Row memberi Text lebar tak terbatas dan tidak ada yang menyuruhnya mengalah. Perbaikannya, Column dibungkus Expanded, rating dipindah ke dalam Column, dan semua Text diberi maxLines serta ellipsis.

8. CategoryBar mengalami overflow kanan karena enam chip totalnya lebih lebar dari 320 dp dan tidak bisa digulir. Perbaikannya membungkus Row dengan SingleChildScrollView horizontal.

9. MenuTile mengalami overflow kanan, terutama saat nama menu sangat panjang. Penyebabnya, Row memberi Text lebar tak terbatas. Perbaikannya, Column teks dibungkus Expanded, nama diberi maxLines 2 dengan ellipsis, dan harga diberi maxLines 1.

10. MenuCard mengalami overflow bawah 62 px di tablet. Aturan yang dilanggar adalah tinggi ikon yang dikeraskan 110 tidak mau mengalah, padahal tinggi sel sudah ditentukan oleh grid. Perbaikannya, Container diganti Expanded dan semua Text diberi maxLines serta ellipsis.

11. CartBar mengalami overflow kanan dan tombolnya bisa tertutup gesture bar. Penyebabnya, tinggi 72 dan lebar tombol 160 dikeraskan, teks tidak dibatasi parent, dan tidak ada inset aman. Perbaikannya, height dan width tetap dihapus, teks dibungkus Expanded dengan maxLines 2, dan seluruh bar dibungkus SafeArea(top: false).

12. EmptyState dibuat karena data kosong sebelumnya menghasilkan layar blank. Penyebabnya, kode mengira data selalu ada. Perbaikannya, dibuat widget baru berisi ikon, pesan, dan tombol Reset filter dengan key empty-state, yang dipasang di SliverFillRemaining.

13. _MenuScreenState mendapat tambahan pendukung karena tombol Reset filter tidak bisa mengosongkan kolom pencarian. Penyebabnya, SearchBar tidak punya controller. Perbaikannya menambahkan TextEditingController _search, method dispose(), dan method _reset().