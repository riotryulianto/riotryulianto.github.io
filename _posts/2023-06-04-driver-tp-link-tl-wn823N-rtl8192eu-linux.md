---
layout: post
title: "Instalasi Driver TP-Link TL-WN823N (RTL8192EU) di Linux"
date: "2023-06-04"
categories: linux
---
[TP-Link TL-WN823N](https://www.tokopedia.com/pronetindo/tp-link-300mbps-mini-wireless-n-usb-adapter-tl-wn823n?src=topads) ini adalah salah satu dongle Wi-Fi terlaris di berbagai e-commerce. Sayangnya, bagi pengguna Linux, dongle ini adalah mimpi buruk. dari sekian banyaknya update kernel yang dirilis setiap bulan sejak beberapa tahun yang lalu sampai hari ini, driver bawaan kernel masih belum support perangkat satu ini. 

Beruntungnya, komunitas Open Source dipenuhi oleh orang-orang baik hati, sehingga kita tidak perlu meng-compile driver sendiri.

Di [repo Github ini](https://github.com/Mange/rtl8192eu-linux-driver), sudah tersedia driver untuk perangkat TPLINK TL-WN283N yang siap di-install di berbagai macam distro dan architecture. Jika distro yang digunakan merupakan OpenSUSE, maka kita bisa mengunduh package-nya pada [link OpenSUSE Build Service ini](https://software.opensuse.org/download/package?package=rtl8192eu&project=home%3ASauerland%3Ahardware).

- [Mange/rtl8192eu-linux-driver: Drivers for the rtl8192eu chipset for wireless adapters (D-Link DWA-131 rev E1 included!)](https://github.com/Mange/rtl8192eu-linux-driver)
- [Install package home:Sauerland:hardware / rtl8192eu](https://software.opensuse.org/download/package?package=rtl8192eu&project=home%3ASauerland%3Ahardware)