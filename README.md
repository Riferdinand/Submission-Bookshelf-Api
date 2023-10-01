# Submission-Bookshelf-Api
Repository Ini Berisi Pengalaman Belajarku di Dicoding. 

## Kriteria 1: Aplikasi menggunakan port 9000
Aplikasi yang Anda buat harus menggunakan port 9000. Jika komputer yang Anda gunakan untuk membuat submission tidak bisa memakai port 9000,  buatlah submission dengan port lain, lalu ketika submission hendak dikirimkan silakan ganti portnya ke 9000.

## Kriteria 2: Aplikasi dijalankan dengan perintah npm run start
Aplikasi yang Anda buat harus memiliki runner script start. Cara membuatnya, Anda tambahkan properti start ke dalam properti scripts pada package.json seperti berikut:<br/>
```javascript
{
  "name": "submission",
  ...
  "scripts": {
    "start": "node src/server.js",
  }
}
``` 

Pastikan aplikasi tidak dijalankan dengan menggunakan nodemon. Jika Anda ingin menggunakan nodemon dalam proses development, masukkan nodemon kedalam runner script lain, contohnya: <br/>
```javascript
{
  "name": "submission",
  ...
  "scripts": {
    "start": "node src/server.js",
    "start-dev": "nodemon src/server.js",
  }
}
``` 
