Lab 04 - Fix Log

MenuScreen (keyboard/landscape): overflow bawah 148 px. Column meminta tinggi lebih dari sisa layar dan tidak bisa scroll. Diganti CustomScrollView + slivers.

MenuScreen (tablet): layout cuma melebar, tidak berubah. Pakai MediaQuery, bukan constraint dari parent. Diganti LayoutBuilder: maxWidth >= 600 jadi grid, di bawahnya list.

MenuScreen (list): semua item dibuat sekaligus. List panjang tidak lazy. Diganti SliverList.builder dan SliverGrid.builder.

PromoStrip: error parameter dan bisa crash kalau data kosong. Kode menganggap selalu ada 2 promo. Sekarang terima List, kalau kosong jadi SizedBox.shrink, Row dibungkus scroll horizontal.

MenuTile: overflow kanan di 320 dp, nama panjang. Row memberi Text lebar tak terbatas. Column dibungkus Expanded, maxLines 2 + ellipsis.

MenuCard: overflow bawah 62 px di tablet. Tinggi ikon fix 110 dan tidak mau mengalah. Diganti Expanded, semua Text diberi maxLines + ellipsis.

CartBar: overflow kanan dan tombol ketutup gesture bar. Tinggi 72 dan lebar tombol 160 fix, teks tanpa batas. Height/width fix dihapus, teks pakai Expanded, ditambah SafeArea.

EmptyState: data kosong layar jadi blank. Kode menganggap data pasti ada. Widget baru berisi ikon, pesan, tombol Reset, dan key empty-state.