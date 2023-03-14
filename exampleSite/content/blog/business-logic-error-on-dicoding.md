---
title: Business Logic Error on Dicoding
description: meta description
image: images/post/post-4.png
date: 2021-01-24T18:19:25.000+06:00
categories:
- Bug Bounty
- Dicoding
type: featured

---
Hallo semuanya selamat datang pada artikel pertama saya di blog pribadi saya. Pada kesempatan kali ini izinkan saya untuk membagikan sebuah artikel temuan _bug_ pada sebuah platform pembelajaran online tentang teknologi yang populer di Indonesia yaitu dicoding.

Sebelum saya masuk ke pembahasan, saya akan memberikan sedikit cerita sebelum saya mendapatkan bug ini. Jadi, beberapa bulan sebelum saya mendapatkan bug pada dicoding, saya mengikuti program kampus merdeka yaitu MSIB (magang & studi independent bersertifikat) suatu program pemerintah yang bertujuan untuk para mahasiswa belajar / mencari pengalaman di luar kampus dan mendapatkan full konversi SKS (tidak melakukan kuliah tapi mendapatkan nilai). Dan saya diterima mitra dicoding sebagai tempat belajar saya studi independent selama 1 semester. Singkat cerita saya lulus dari program tersebut selama 1 semester lama-nya dan mendapatkan 1000 point dicoding sebagai hadiah kelulusan. Dan kita akan mulai ke pembahasan-nya.

Setelah saya lulus MSIB dan mendapatkan 1000 point dicoding, saya mulai mencari celah keamanan pada platform dicoding. Setelah melakukan beberapa uji coba, saya menemukan kerentanan yang disebabkan oleh race condition pada parameter "point". Kerentanan ini memungkinkan user untuk menggunakan poin tanpa harus membayar biaya apa pun / user dapat menggandakan point.

#### Apa itu Race Conditon?

> Sebuah situasi di mana beberapa proses yang berjalan bersamaan saling berkompetisi untuk mengakses dan memanipulasi data yang sama.

![](https://miro.medium.com/v2/resize:fit:360/0*DVIMwe5k8C4g7dsq.png)

Misalkan, ketika 2 atau lebih user ingin melakukan perubahan data pada record yang sama, maka akan sering terjadi konflik inilah yang biasa disebut dengan _race condition._ Dengan kata lain, pada _concurrent_ proses, salah satu yang selesai duluan maka berhasil menang, dan yang lain akan mendapatkan error.

Bug ini kerap kali disalahgunakan oleh para hacker untuk mengeksploitasi sistem, dimana seharusnya user tersebut dapat melakukan suatu aksi sekali namun user mendapat keuntungan lain setelah melakukan aksi beberapa kali (secara simultan).

#### Proof Of Concept!

Tools:

* Burp Suite
* Turbo Intruder (Burp Suite)

Langkah-langkah:

1. Pertama Login ke akun dicoding melalui link ini [https://www.dicoding.com/login](https://www.dicoding.com/login "https://www.dicoding.com/login").
2. Pergi ke dashboard tukar point ([https://www.dicoding.com/rewards/966](https://www.dicoding.com/rewards/966 "https://www.dicoding.com/rewards/966")).
3. Capture request dengan intercept pada Burp Suite kemudian send to turbo intruder.

   ![](/images/dicoding-poc-1.png)
4. Pilih examples/race.py untuk menggunakan script race condition tersebut.
5. Diatas request parameter berikan payload seperti ini Test: %s

   ![](/images/dicoding-poc-2.png)
6. Klik Attack dan dapat dilihat penyerang dapat melakukan request secara bersamaan yaitu 3 request dalam waktu yang sama, dampak nya yaitu hanya dengan menggunakan 300 point tetapi pesanan yang terkonfirmasi ada 3.
7. ![Point awal](/images/dicoding-poc-3.png "Point awal")