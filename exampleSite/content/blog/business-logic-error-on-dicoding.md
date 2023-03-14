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

Setelah saya lulus dan mendapatkan 1000 point, saya mulai mencari celah keamanan pada platform dicoding. Setelah melakukan beberapa uji coba, saya menemukan kerentanan yang disebabkan oleh race condition pada parameter "point". Kerentanan ini memungkinkan user untuk menggunakan poin tanpa harus membayar biaya apa pun / user dapat menggandakan point.

#### Covid-19 Situation

Nam ut rutrum ex, venenatis sollicitudin urna. Aliquam erat volutpat. Integer eu ipsum sem. Ut bibendum lacus vestibulum maximus suscipit. Quisque vitae nibh iaculis neque blandit euismod.

> Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!

#### Work From Home

Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius! Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!

{{< image src="images/post/post-5.png" caption="Example Caption" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title" webp="false" >}}

Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius! Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!