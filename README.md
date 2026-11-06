# pkdj_2026_rancang_jaringan_ubbg_antar_dua_gedung
Project rancang bangun jaringan

Latar Belakang

Universitas Bina Bangsa Getsempena (UBBG) terus meningkatkan kualitas pelayanan akademik dan operasional melalui infrastruktur jaringan lokal (LAN) yang andal, cepat, dan aman. Operasional harian UBBG terbagi dalam beberapa gedung perkuliahan, dengan pusat data (server utama) terletak di Gedung A.
Tantangan utamanya adalah menghubungkan gedung perkuliahan pendukung (Gedung B) ke server pusat secara private (internal) tanpa terakses oleh jaringan publik guna meminimalisir risiko cyber security. Perancangan dan simulasi dilakukan menggunakan Cisco Packet Tracer untuk menguji validitas arsitektur jaringan sebelum diimplementasikan secara fisik.

Tujuan Perancangan

•	Mengembangkan arsitektur topologi jaringan terintegrasi antara Gedung A dan Gedung B di UBBG.

•	Memastikan seluruh client di kedua gedung dapat mengakses Server Pusat UBBG secara private dan aman.

•	Menerapkan konfigurasi VLAN, Trunking, dan Inter-VLAN Routing pada perangkat jaringan Cisco guna mengoptimalkan keamanan dan efisiensi lalu lintas data.

Topologi Jaringan

Menggunakan arsitektur Hierarchical Star Topology dengan sambungan inter-switch link (virtual Fiber Optic / GigabitEthernet di Cisco Packet Tracer):
•	Gedung A: Berisi Switch-A (Akses Gedung A), beberapa client (PC/Laptop), dan Server Utama UBBG.
•	Gedung B: Berisi Switch-B (Akses Gedung B) dan beberapa client (PC/Laptop).
•	Perangkat Penghubung Pusat: Menggunakan Router UBBG (Router-on-a-Stick) atau Layer 3 Switch sebagai pusat routing antar-VLAN dan antar-gedung.

Perangkat & Spesifikasi Virtual

•	1 Unit Router (Router-UBBG): Router Cisco (sebagai pusat routing Inter-VLAN & Gateway).
•	2 Unit Switch Managed: Switch-A (Gedung A) & Switch-B (Gedung B).
•	1 Unit Server Pusat: Server-UBBG (menjalankan service HTTP/Web & DNS internal).
•	PC / Laptop Client: Mewakili pengguna/staf di Gedung A dan mahasiswa di Gedung B.
•	Kabel Ethernet / Fiber Optic: Media koneksi antar-switch, router, server, dan client.

Rancangan VLAN dan Pengalamatan IP

Skema pembagian Virtual LAN (VLAN) dan Subnetting IP Address dikelompokkan sebagai berikut:
VLAN ID	Nama VLAN	Alokasi Network / Subnet	Keterangan & Peruntukan
VLAN 10	GEDUNG A	192.168.10.0/24
(GW: 192.168.10.1)	Client / Staf Gedung A
(Contoh IP: 192.168.10.10)
VLAN 20	GEDUNG B	192.168.20.0/24
(GW: 192.168.20.1)	Client / Mahasiswa Gedung B
(Contoh IP: 192.168.20.10)
VLAN 30	SERVER UBBG	192.168.30.0/24
(GW: 192.168.30.1)	Server Utama Data Penting di Gedung A
(IP Server: 192.168.30.10)

Cara Menjalankan & Langkah Konfigurasi

Langkah 1: Penyiapan Perangkat — Buka Cisco Packet Tracer, letakkan 1 Router, 2 Switch, 1 Server, dan PC Client di masing-masing gedung.
Langkah 2: Pengkabelan (Koneksi) — Hubungkan Client & Server ke Switch gedungnya masing-masing. Hubungkan Switch-A dan Switch-B ke Router melalui port GigabitEthernet/Trunk.
Langkah 3: Konfigurasi IP Server — Set IP Server UBBG: 192.168.30.10 | Subnet: 255.255.255.0 | Gateway: 192.168.30.1. Aktifkan layanan HTTP pada tab Services.
Langkah 4: Konfigurasi IP Client — PC Gedung A: IP 192.168.10.10 | Gateway 192.168.10.1.
PC Gedung B: IP 192.168.20.10 | Gateway 192.168.20.1.
Langkah 5: Konfigurasi Switch & VLAN — Switch Gedung A: Buat VLAN 10 & 30, set port Server ke VLAN 30, port ke Router ke mode Trunk.
Switch Gedung B: Buat VLAN 20, set port Client ke VLAN 20, port ke Router ke mode Trunk.
Langkah 6: Konfigurasi Inter-VLAN Router — Aktifkan sub-interface pada Router (misal: Gi0/0.10, Gi0/0.20, Gi0/0.30) dengan 802.1Q encapsulation untuk masing-masing VLAN ID dan tetapkan IP Gateway.

Rencana Pengujian & Indikator Keberhasilan

Metode Pengujian:
•	Uji ICMP (Ping Test) Antar VLAN & Gedung: Jalankan perintah ping 192.168.30.10 dari Client Gedung B untuk menguji konektivitas ke Server UBBG.
•	Pengujian Layanan Web (HTTP): Buka Web Browser pada Client Gedung B dan akses URL http://192.168.30.10 untuk memastikan layanan web internal terbuka.
•	Simulasi Pergerakan Paket (Simulation Mode): Gunakan mode Simulation di Packet Tracer untuk mengamati lalu lintas paket Simple PDU yang melewati jalur Trunk dan Sub-interface Router.
Indikator Keberhasilan:
•	Ping Berhasil (Reply): Tes ping dari Gedung B ke Server UBBG (192.168.30.10) menghasilkan 'Reply from...' (0% packet loss).
•	Layanan Tampil Sempurna: Halaman web server internal UBBG dapat diakses secara private dari browser PC Gedung B.
•	Isolasi Keamanan Terjaga: Lalu lintas data inter-VLAN teratur dan terisolasi dari akses publik.

Batasan Masalah

Batasan Masalah:
•	Cakupan Wilayah: Terbatas pada dua gedung perkuliahan UBBG (Gedung A sebagai pusat server, Gedung B sebagai client).
•	Lingkup Simulasi: Seluruh perancangan, topologi, dan pengujian dilakukan secara virtual menggunakan Cisco Packet Tracer.

Rencana Pengembangan Selanjutnya

•	Implementasi Redundancy: Menambahkan Redundant Link (Spanning Tree Protocol - STP) dan Router Redundancy (HSRP/VRRP) untuk mencegah Single Point of Failure.
•	Pengembangan Keamanan Lanjutan: Menerapkan Access Control List (ACL), Port Security pada switch, dan Firewall dedicated untuk perlindungan server.

