UNTUKMU, GURU — FITUR AUDIO SUPERADMIN

PENTING:
- GitHub Pages hanya hosting file statis. Password dan hak edit TIDAK boleh disimpan/diuji hanya dengan JavaScript di browser.
- Paket ini memakai Supabase sebagai backend terpisah untuk login superadmin, database playlist, dan penyimpanan file audio.
- Pengunjung tidak perlu login. Hanya akun yang diberi app_metadata.role = "superadmin" yang bisa menambah, mengedit, menyembunyikan, atau menghapus lagu.
- Jangan pernah memasukkan service_role key ke supabase-config.js atau repository.

SETUP PERTAMA KALI
1. Buat project Supabase.
2. Buka SQL Editor, jalankan seluruh isi supabase-setup.sql.
3. Buka Project Settings > API. Salin Project URL dan anon/public key.
4. Isi dua nilai itu ke supabase-config.js. Jangan gunakan service_role key.
5. Di Supabase Authentication, buat akun untuk superadmin dengan email dan password kuat.
6. Buka Authentication > Users, pilih akun tersebut, lalu atur app_metadata role menjadi:
   {"role":"superadmin"}
   Lakukan melalui pengaturan user metadata/administrative interface yang mendukung app_metadata. Jangan taruh role di user_metadata.
7. Deploy semua file dalam folder ini ke repository GitHub Pages (index.html, supabase-config.js).
8. Buka website. Di footer ada tautan kecil "Superadmin". Login memakai akun superadmin.
9. Dari HP, pilih file audio melalui formulir, isi judul dan penyanyi, lalu Tambah lagu.
10. Untuk mengaktifkan fitur surat, jalankan ulang seluruh isi `supabase-setup.sql` di SQL Editor. Perintahnya aman dijalankan ulang dan akan membuat tabel `teacher_letters` beserta aturan aksesnya.
11. Login Superadmin. Formulir “Kelola surat untuk guru” dapat digunakan untuk menambah, mengedit, dan menghapus surat.

PENGGUNAAN
- Public: semua pengunjung bisa memutar lagu aktif tanpa login.
- Superadmin: login email + password, dapat tambah lagu, edit judul/keterangan, ganti file audio, sembunyikan/tampilkan, dan hapus.
- Lagu otomatis dipotong saat sudah diputar 120 detik; playlist berpindah ke lagu berikutnya.
- Upload dibatasi 20 MB per file.
- Jika mengganti file, file lama akan dihapus dari bucket.
- Lagu yang dihapus dari playlist juga dihapus dari storage.
- Surat ditampilkan otomatis di halaman publik, 10 surat per halaman. Tombol Sebelumnya/Selanjutnya muncul jika jumlah surat lebih dari 10. Surat terbaru tampil lebih dahulu.
- Nomor surat dibuat otomatis berdasarkan urutan tampilan; nama pengirim tidak disimpan atau ditampilkan.

KEAMANAN
- Password tidak pernah ditulis di HTML atau JavaScript.
- RLS database dan Storage membatasi semua perubahan hanya untuk app_metadata.role = superadmin.
- Anon/public key memang boleh berada di frontend; service_role key TIDAK BOLEH.
- Aktifkan konfirmasi email dan gunakan password unik. Jangan bagikan akun superadmin.
- Jika menggunakan repository publik, jangan pernah commit file yang berisi password, service_role key, atau data rahasia.

CATATAN FILE SPREADSHEET
Link Google Sheets yang diberikan belum dapat saya baca dari koneksi ini karena koneksi Google Drive untuk akun ini tidak tersedia. Fitur surat pada versi ini memakai tabel `teacher_letters` di Supabase sebagai sumber data langsung website. Jika surat yang sudah ada di spreadsheet ingin dimasukkan, ekspor spreadsheet sebagai CSV/XLSX lalu impor ke tabel tersebut atau kirim file ekspornya untuk dibantu siapkan proses impor.
