# **Kriteria Submission-Bookshelf-Api**


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
## Kriteri 3: API dapat menyimpan buku
API yang Anda buat harus dapat menyimpan buku melalui route: <br/>
Method: POST <br/>
URL : /books <br/>
Body Request: <br/>
```javascript
{
    "name": string,
    "year": number,
    "author": string,
    "summary": string,
    "publisher": string,
    "pageCount": number,
    "readPage": number,
    "reading": boolean
}
```
Objek buku yang disimpan pada server harus memiliki struktur seperti contoh di bawah ini: <br/>
```javascript
{
    "id": "Qbax5Oy7L8WKf74l",
    "name": "Buku A",
    "year": 2010,
    "author": "John Doe",
    "summary": "Lorem ipsum dolor sit amet",
    "publisher": "Dicoding Indonesia",
    "pageCount": 100,
    "readPage": 25,
    "finished": false,
    "reading": false,
    "insertedAt": "2021-03-04T09:11:44.598Z",
    "updatedAt": "2021-03-04T09:11:44.598Z"
}
```
- Properti yang ditebalkan diolah dan didapatkan di sisi server. Berikut penjelasannya: <br/>
    - id : nilai id haruslah unik. Untuk membuat nilai unik, Anda bisa memanfaatkan nanoid. <br/>
    - finished : merupakan properti boolean yang menjelaskan apakah buku telah selesai dibaca atau belum. Nilai finished didapatkan dari observasi pageCount === readPage. <br/>
    - insertedAt : merupakan properti yang menampung tanggal dimasukkannya buku. Anda bisa gunakan new Date().toISOString() untuk menghasilkan nilainya. <br/>
    - updatedAt : merupakan properti yang menampung tanggal diperbarui buku. Ketika buku baru dimasukkan, berikan nilai properti ini sama dengan insertedAt. <br/>

- Server harus merespons gagal bila: <br/>
  - Client tidak melampirkan properti namepada request body. Bila hal ini terjadi, maka server akan merespons dengan: <br/>
    - Status Code : 400 <br/>
    - Response Body: <br/>
      ```javascript
      {
        "status": "fail",
        "message": "Gagal menambahkan buku. Mohon isi nama buku"
      }
      ```

- Client melampirkan nilai properti readPage yang lebih besar dari nilai properti pageCount. Bila hal ini terjadi, maka server akan merespons dengan: <br/>
  - Status Code : 400 <br/>
  - Response Body: <br/>
    ```javascript
    {
      "status": "fail",
      "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
    }
    ```

- Bila buku berhasil dimasukkan, server harus mengembalikan respons dengan: <br/>
  - Status Code : 201 <br/>
  - Response Body: <br/>
    ```javascript
    {
      "status": "success",
      "message": "Buku berhasil ditambahkan",
      "data": {
        "bookId": "1L7ZtDUFeGs7VlEt"
      }
    }
    ```

## Kriteria 4: API dapat menampilkan seluruh buku
API yang Anda buat harus dapat menampilkan seluruh buku yang disimpan melalui route:<br/>
  - Method : GET
  - URL: /books

Server harus mengembalikan respons dengan: <br/>
  - Status Code : 200
  - Response Body:
