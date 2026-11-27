PAKET CBT WEB APP — 27 NOVEMBER 2026

ISI PAKET
- Code.gs: backend Google Apps Script, versi sumber terbaru yang tersedia pada percakapan.
- index.html: frontend CBT yang dipanggil oleh doGet() melalui HtmlService.

ARSITEKTUR
- GitHub: repositori sumber kode (backup/version control).
- Google Apps Script: runtime Web App operasional.
- Google Sheets: penyimpanan data peserta, jawaban, nilai, dan koreksi uraian.
- File HTML tidak boleh dibuka langsung dari folder Downloads atau GitHub Pages karena menggunakan google.script.run.

LANGKAH AMAN PEMASANGAN
1. Buat salinan/cadangan proyek Apps Script dan spreadsheet CBT yang sedang dipakai. Jangan menghapus sheet atau baris data lama.
2. Di repository GitHub, simpan Code.gs dan index.html sebagai sumber kode. GitHub tidak otomatis memperbarui Apps Script kecuali integrasi clasp memang sudah dikonfigurasi; tanpa clasp, salin perubahan secara manual.
3. Buka proyek Apps Script operasional yang terhubung ke spreadsheet CBT yang benar.
4. Pada file script Code.gs, cadangkan isi lama lalu ganti dengan isi Code.gs dari paket ini.
5. Pada file HTML bernama index (jenis file HTML; nama di editor Apps Script adalah "index"), ganti isinya dengan index.html dari paket ini. Fungsi doGet() memanggil HtmlService.createHtmlOutputFromFile('index').
6. Jangan membuat proyek Apps Script baru dan jangan menjalankan setup() sebelum memastikan spreadsheet aktif dan struktur header benar. Jangan menghapus atau membuat ulang spreadsheet.
7. Periksa Project Settings > Script Properties. Pastikan properti SS_ID, EXAM_TOKEN, dan GURU_KEY tersedia dan mengarah ke spreadsheet/token/kunci yang benar. Jangan mengirim nilai token atau PIN melalui chat.
8. Jalankan diagnostikCBT() dari editor Apps Script. Fungsi ini bersifat read-only; periksa hasil Execution log. Pastikan spreadsheet ditemukan, properti tersedia, dan sheet REKAP_NILAI, JAWABAN_PERBUTIR, serta KOREKSI_URAIAN tersedia.
9. Simpan proyek. Pilih Deploy > Manage deployments > Edit (ikon pensil) > Version: New version > Deploy.
10. Buka URL Web App yang berakhiran /exec. Jangan membuka file lokal dari Downloads. Pastikan URL deployment yang dibuka berasal dari proyek Apps Script yang baru diperbarui.

UJI FUNGSI
A. Halaman login: pilih kelas, masukkan token, tunggu daftar nama muncul, pilih nama, lalu masuk.
B. Pastikan nama peserta hanya muncul setelah token valid.
C. Uji satu akun peserta uji coba yang memang disiapkan sekolah; jangan mengirim ujian sungguhan untuk tes.
D. Panel Guru: masuk dengan kunci guru, periksa rekap dan lakukan refresh manual. Sinkronisasi otomatis dirancang 30 detik.
E. Koreksi uraian: uji hanya pada data uji coba, pastikan nilai akhir dihitung 80% objektif + 20% uraian dan status Tuntas menggunakan KKTP 76.
F. Setelah uji berhasil, periksa Google Sheets apakah data baru masuk pada baris yang benar. Jangan mengubah atau menghapus data lama selama pengujian.

CATATAN PENTING
- Source HTML memuat gambar soal sebagai data URI/base64. Dua logo di header merujuk file logo-jsit.png dan logo-madrasah.png; jika file tersebut tidak tersedia di proyek/lokasi yang dapat diakses, fallback logo akan tampil.
- Paket ini mempertahankan file sumber terbaru yang tersedia. Saya tidak dapat menerbitkan deployment atau mengakses spreadsheet/proyek Apps Script Anda secara langsung dari sini. Pengujian akhir harus dilakukan pada URL /exec milik Anda.
- Jika diagnostikCBT() melaporkan properti atau sheet tidak tersedia, hentikan deployment dan periksa konfigurasi terlebih dahulu. Jangan menjalankan setup() secara coba-coba.
