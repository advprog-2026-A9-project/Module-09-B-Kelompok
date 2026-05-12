# Module-09-B-Kelompok

<details>
<Summary><b>The current architecture of the group YOMU (A09), the context, container and deployment diagram.</b></Summary>

## Context Diagram

![Context Diagram](Diagrams/Group/Commit%201/Context%20Diagram.drawio.png)

## Container Diagram

![Container Diagram](Diagrams/Group/Commit%201/Container%20Diagram.drawio.png)

## Deployment Diagram

![Deployment Diagram](Diagrams/Group/Commit%201/Deployment%20Diagram.drawio.png)

</details>

<details>
<Summary><b>The future architecture of the group YOMU (A09).</b></Summary>

## Risk Storming Diagram
![Risk Storming Diagram](Diagrams/Group/Commit%202/Risk%20Storming%20Diagram.drawio.png)

## Future Architecture Diagram
![Future Architecture Diagram](Diagrams/Group/Commit%202/Arsitektur%20Masa%20Depan.drawio.png)


</details>

<details>
<Summary><b>Explanation of risk storming of the group YOMU (A09).</b></Summary>

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



