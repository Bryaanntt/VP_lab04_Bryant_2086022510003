1. A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?

= Yang dilanggar adalah "constraints go down". Row tidak membatasi lebar Text, jadi Text merasa punya ruang tak terbatas dan melebar sampai keluar layar. Ibaratnya Row adalah rak, dan Text barang yang tidak tahu ukuran rak. Solusinya bungkus Text dengan Expanded, supaya Row bilang "kamu cuma boleh pakai sisa tempat ini".

2. Why is adding width: 150 to the text the wrong fix, even if the stripes disappear?

= Karena itu hanya mengubah angka, bukan hubungan antara parent dan child. Lebar 150 mungkin pas di satu ukuran layar, tapi di layar yang lebih sempit, saat font diperbesar, atau saat teksnya lebih panjang, overflow muncul lagi di tempat lain. Fix yang benar membiarkan parent yang menentukan ukuran.

3. You fixed the landscape overflow by wrapping everything in a SingleChildScrollView and setting shrinkWrap: true on the list. Which test fails, and why does it matter once the data comes from an API?

= Karena itu hanya mengubah angka, bukan hubungan antara parent dan child. Lebar 150 mungkin pas di satu ukuran layar, tapi di layar yang lebih sempit, saat font diperbesar, atau saat teksnya lebih panjang, overflow muncul lagi di tempat lain. Fix yang benar membiarkan parent yang menentukan ukuran.

4. Why does the tablet layout use LayoutBuilder rather than MediaQuery.sizeOf(context)?

= MediaQuery memberi ukuran seluruh layar, sedangkan LayoutBuilder memberi constraint yang benar-benar diberikan parent ke widget itu. Kalau widget ditaruh di panel yang lebih sempit dari layar, LayoutBuilder tetap memilih layout yang tepat, sedangkan MediaQuery bisa salah memilih.

5. The empty-data crash was not a layout error. Why does it belong in a layout lab anyway?

= Karena data kosong adalah salah satu kondisi tampilan yang harus dipikirkan, sama seperti ukuran layar dan keyboard. Kode yang menganggap data pasti ada (seperti PromoStrip lama yang butuh first dan second) akan crash atau menghasilkan layar kosong. Layar yang kokoh harus punya bentuk untuk keadaan kosong, yaitu empty state.