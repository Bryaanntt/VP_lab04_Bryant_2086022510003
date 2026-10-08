Lab 04 - Fix Log

1. MenuScreen, struktur halaman
Sebelum: Column berisi header, search, chip, promo, lalu Expanded(ListView). Saat keyboard terbuka atau landscape, bagian atas sudah memakan tinggi layar, lalu overflow bawah 148 px.
Aturan yang dilanggar: Column minta tinggi sebesar isinya, padahal parent hanya punya sisa ruang terbatas dan tidak ada yang bisa di-scroll.
Sesudah: seluruh halaman jadi satu CustomScrollView dengan slivers, jadi kelebihan tinggi bisa digulir.

2. MenuScreen, breakpoint tablet
Sebelum: isTablet = MediaQuery.sizeOf(context).width > 600.
Aturan yang dilanggar: membaca ukuran layar, bukan constraint yang diberikan parent. Batasnya juga salah, karena 600 pas tidak dihitung tablet.
Sesudah: LayoutBuilder dengan constraints.maxWidth >= 600. Lebar: grid. Sempit: list.

3. MenuScreen, list dan grid
Sebelum: ListView(children: [for ...]) dan GridView.count(crossAxisCount: 4, children: [for ...]). Semua item dibuat sekaligus, 4 kolom tetap.
Aturan yang dilanggar: list yang panjangnya tidak dikontrol tidak lazy.
Sesudah: SliverList.builder dan SliverGrid.builder. Kolom 3 atau 4 mengikuti lebar (maxWidth >= 900 jadi 4).

4. MenuScreen, promo
Sebelum: PromoStrip(first: promos[0], second: promos[1]).
Aturan yang dilanggar: kode mengira selalu ada dua promo. Kalau data kosong, RangeError dan crash.
Sesudah: PromoStrip(items: promos).

5. PromoStrip
Sebelum: Row berisi dua PromoCard lebar 200 plus jarak 16, total sekitar 416 dp. Di layar 320 dp overflow kanan.
Aturan yang dilanggar: anak minta lebar lebih besar dari yang diberikan parent.
Sesudah: menerima List, kosong jadi SizedBox.shrink(), Row dibungkus SingleChildScrollView horizontal.

6. PromoCard
Sebelum: tiga Text tanpa maxLines.
Sesudah: maxLines 1 atau 2 dan overflow ellipsis. Ukuran 200 x 150 bawaan file, tidak diubah.

7. StoreHeader
Sebelum: Row berisi ikon, Column nama toko, bintang, dan teks ulasan, tanpa Expanded dan tanpa maxLines. Overflow kanan di 320 dp.
Aturan yang dilanggar: Row memberi Text lebar tak terbatas dan tidak ada yang menyuruhnya mengalah.
Sesudah: Column dibungkus Expanded, rating dipindah ke dalam Column, semua Text diberi maxLines dan ellipsis.

8. CategoryBar
Sebelum: Row berisi 6 ChoiceChip langsung di Padding. Total lebar melebihi 320 dp, overflow kanan.
Aturan yang dilanggar: isi minta lebih lebar dari parent dan tidak bisa digulir.
Sesudah: dibungkus SingleChildScrollView horizontal.

9. MenuTile
Sebelum: Column teks langsung di Row dengan Spacer, tanpa maxLines. Nama panjang membuat overflow kanan.
Aturan yang dilanggar: Row memberi Text lebar tak terbatas.
Sesudah: Column dibungkus Expanded, nama maxLines 2 dan ellipsis, harga maxLines 1.

10. MenuCard
Sebelum: Container(height: 110) dan Text tanpa maxLines. Di tablet overflow bawah 62 px.
Aturan yang dilanggar: tinggi tetap tidak mau mengalah, padahal tinggi sel sudah ditentukan grid.
Sesudah: Container diganti Expanded, semua Text diberi maxLines dan ellipsis.

11. CartBar
Sebelum: Container(height: 72), tombol SizedBox(width: 160), Text tanpa Expanded dan tanpa SafeArea. Overflow kanan dan tombol bisa ketutup gesture bar.
Aturan yang dilanggar: tinggi dan lebar dikeraskan, teks tidak dibatasi parent.
Sesudah: height dan width dihapus, Text dibungkus Expanded dengan maxLines 2, seluruhnya dibungkus SafeArea(top: false).

12. EmptyState (widget baru)
Sebelum: data kosong menghasilkan layar blank.
Aturan yang dilanggar: kode mengira data selalu ada.
Sesudah: widget baru berisi ikon, pesan, dan tombol Reset filter, dengan key const Key('empty-state'). Dipasang di 

13. SliverFillRemaining.
Pendukung di _MenuScreenState
Sebelum: SearchBar tanpa controller, jadi tombol Reset tidak bisa mengosongkan kolom pencarian.
Sesudah: ditambah TextEditingController _search, dispose(), dan _reset().