# Module-09-B-Kelompok

<details>
<Summary><b>1. The current architecture of the group YOMU (A09), the context, container and deployment diagram.</b></Summary>

## Context Diagram

![Context Diagram](Diagrams/Group/Commit%201/Context%20Diagram.drawio.png)

## Container Diagram

![Container Diagram](Diagrams/Group/Commit%201/Container%20Diagram.drawio.png)

## Deployment Diagram

![Deployment Diagram](Diagrams/Group/Commit%201/Deployment%20Diagram.drawio.png)

</details>

<details>
<Summary><b>2. The future architecture of the group YOMU (A09).</b></Summary>

## Risk Storming Diagram
![Risk Storming Diagram](Diagrams/Group/Commit%202/Risk%20Storming%20Diagram.drawio.png)

## Future Architecture Diagram
![Future Architecture Diagram](Diagrams/Group/Commit%202/Arsitektur%20Masa%20Depan.drawio.png)


</details>

<details>
<Summary><b>3. Explanation of risk storming of the group YOMU (A09).</b></Summary>

## Explanation of Risk Storming

Risk Storming adalah teknik utk mengidentifikasi 
dan mengevaluasi risiko arsitektur sistem secara visual. 
Teknik ini diterapkan dengan cara menandai komponen-komponen 
dalam diagram arsitektur berdasarkan tingkat risikonya.

Pada arsitektur Yomu saat ini, ditemukan beberapa risiko utama:

1. **Backend sebagai Single Point of Failure** - Seluruh 
   logika bisnis berada dalam satu aplikasi monolith di Railway. 
   Jika backend down, seluruh sistem tidak dapat diakses.

2. **Database Bottleneck** - Semua modul menggunakan satu 
   database PostgreSQL. Ketika traffic tinggi, database menjadi 
   titik kemacetan yg dapat memperlambat seluruh sistem.

3. **Event-Driven tidak handal** - Spring Events bersifat 
   in-memory sehingga event dapat hilang jika terjadi crash.

4. **Ketergantungan Google SSO** - Jika Google SSO mengalami 
   gangguan, pengguna tidak dapat login ke sistem.

### Solusi Arsitektur Masa Depan

utk mengatasi risiko tersebut, arsitektur masa depan Yomu 
mengusulkan:
- Migrasi ke **Microservices** agar setiap modul dapat 
  di-scale secara independen
- Setiap service memiliki **database sendiri** utk 
  menghindari bottleneck
- Menggunakan **RabbitMQ** sebagai message broker yg 
  handal menggantikan Spring Events
- Menambahkan **API Gateway** sebagai single entry point

</details>

<details>
<Summary><b>4. Individual Work</b></Summary>

<details>
<Summary><b>Auth</b></Summary>


## Auth Component Diagram
![Auth Component Diagram](Diagrams/Individual/Auth/_Component%20Diagram%20-%20Modul%20Auth.drawio.png)

## Code Diagram

### User Class Diagram
![User Class Diagram](Diagrams/Individual/Auth/User%20Class%20Diagram.drawio.png)

### AuthController Class Diagram
![AuthController Class Diagram](Diagrams/Individual/Auth/AuthController%20Class%20Diagram.drawio.png)

### AuthServiceImpl Class Diagram
![AuthServiceImpl Class Diagram](Diagrams/Individual/Auth/AuthServiceImpl%20Class%20Diagram.drawio.png)

### JWTUtil Class Diagram
![JWTUtil Class Diagram](Diagrams/Individual/Auth/JWTUtil%20Class%20Diagram.drawio.png)

</details>

<details>
<Summary><b>Bacaan dan Kuis</b></Summary>
### Ryan Gibran Purwacakra Sihaloho (2406419833)

**1. Component Diagram (Manajemen Teks Bacaan)**
Diagram ini memperlihatkan alur pengelolaan teks bacaan di dalam komponen backend. Permintaan HTTP dari Frontend akan diverifikasi oleh `SecurityInterceptor` sebelum diproses oleh `ReadingController`. Logika bisnis dieksekusi di `ReadingServiceImpl`, yang berinteraksi dengan Neon DB melalui `ReadingRepository`.
![Component Diagram Bacaan](Diagrams/Individual/Bacaan%20dan%20Kuis/Component_Diagram.png)

**2. Code Diagram (Manajemen Teks Bacaan)**
Class diagram ini membedah komponen di atas ke level kode. `ReadingController` menerima representasi data berupa `ReadingTextDto`, memanggil `ReadingServiceImpl` untuk mengeksekusi logika bisnis, mengonversi DTO menjadi wujud entitas `ReadingText`, lalu menggunakan antarmuka `ReadingRepository` untuk operasi database.
![Code Diagram Bacaan](Diagrams/Individual/Bacaan%20dan%20Kuis/Code_Diagram.png)

**3. Component Diagram (Sistem Kuis & Event Broadcasting) - BONUS**
Diagram ini berfokus pada alur pengerjaan kuis dan implementasi *Event-Driven Architecture*. Setelah Pelajar men-submit jawaban, `QuizServiceImpl` akan menghitung skor dan menyimpannya ke database. Yang paling krusial, *Service* kemudian memanggil `QuizEventPublisher` untuk mengirimkan *event* ke RabbitMQ. Sinyal ini nantinya akan ditangkap secara *asynchronous* oleh Modul Achievements dan Modul Liga tanpa adanya *direct coupling*.
![Component Diagram Kuis](Diagrams/Individual/Bacaan%20dan%20Kuis/Component_Diagram_Kuis.png)

**4. Code Diagram (Sistem Kuis & Event Broadcasting) - BONUS**
Class diagram ini mengilustrasikan injeksi dependensi dalam fitur kuis. `QuizServiceImpl` tidak hanya bergantung pada `QuizRepository`, tetapi juga pada `QuizEventPublisher`. Saat kuis selesai diproses, sistem membentuk objek `QuizFinishedEventMessage` yang berisi *userId*, *score*, dan *accuracy*, lalu dipublikasikan melalui antarmuka *message broker*.
![Code Diagram Kuis](Diagrams/Individual/Bacaan%20dan%20Kuis/Code_Diagram_Kuis.png)


</details>

<details>
<Summary><b>Achievement</b></Summary>



</details>

<details>
<Summary><b>Liga</b></Summary>

# Code diagram
![alt text](Diagrams/Individual/Liga/code_diagram.png)

# Component diagram
![alt text](Diagrams/Individual/Liga/component_diagram.png)

</details>

<details>
<Summary><b>Diskusi</b></Summary>

**Izzudin Abdul Rasyid (2406495786)**

**1. Component Diagram (Discussion Module)**
Diagram ini memvisualisasikan interaksi antara *container* frontend (React) dan backend (Spring Boot) khusus untuk fitur forum diskusi. Komponen UI pada frontend memicu pemanggilan REST API yang ditangani oleh `DiscussionController` di backend, yang kemudian menjalankan logika bisnis melalui service untuk mengelola data komentar dan reaksi pada database Neon PostgreSQL.
![Component Diagram Diskusi](Diagrams/Individual/Discussion/component-diagram.png)

**2. Code Diagram (Backend Discussion Service)**
Class diagram ini membedah struktur kode pada paket `discussion` di backend Yomu. Menunjukkan bagaimana `DiscussionController` bergantung pada abstraksi `DiscussionService`, serta implementasi `DiscussionServiceImpl` yang mengelola siklus hidup entitas `Comment` dan `CommentReaction` menggunakan repositori JPA.
![Code Diagram Backend Diskusi](Diagrams/Individual/Discussion/code-diagram-be.png)

**3. Code Diagram (Frontend Discussion Component) - BONUS**
Sebagai bagian dari pengembangan frontend, diagram ini merepresentasikan arsitektur komponen React untuk modul diskusi. Komponen `DiscussionSection` mengatur *state* internal untuk daftar komentar dan input pengguna, serta berinteraksi dengan `DiscussionAPI` untuk sinkronisasi data asinkron ke server.
![Code Diagram Frontend Diskusi](Diagrams/Individual/Discussion/code-diagram-fe.png)

</details>


</details>


