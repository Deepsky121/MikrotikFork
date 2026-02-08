# 🚀 Mikrotik

> *“May your ping be low and your grade be high.”*  
> — (｡•̀ᴗ-)✧ **AzmiiDev** and **Deepsky121**

![MikroTik](https://img.shields.io/badge/MikroTik-RouterOS-blue)
![Networking](https://img.shields.io/badge/Topic-Networking-green)
![Exam Ready](https://img.shields.io/badge/Status-Exam%20Ready-success)

Panduan singkat & praktis untuk **ujian Mikrotik SMK MA’ARIF**.  
Disusun ringkas, fokus poin ujian, dan langsung bisa dieksekusi via **Terminal RouterOS**.

---

## 📚 Daftar Isi
1. [Basic & IP Address](#-1-basic--ip-address)
2. [Internet Gateway (NAT & Route)](#-2-internet-gateway-nat--route)
3. [Web Proxy & Blocking](#-3-web-proxy--blocking)
4. [Static Routing](#-4-static-routing)
5. [Pro Tips](#-pro-tips)
6. [Meme of the Day](#-meme-of-the-day)

---

## 📝 1. Basic & IP Address

> ⚠️ **Catatan:**  
> Ganti `ether2`, `ether3`, atau `192.168.x.x` sesuai instruksi pengawas.

```bash
/system identity set name="Peserta-Ujian-Ganteng"

/ip address add address=192.168.10.1/24 interface=ether2
/ip address add address=192.168.20.1/24 interface=ether3
```
Digunakan untuk:
- Identitas router
- IP lokal ke jaringan client

🌐 2. Internet Gateway (NAT & Route)

Agar client di bawah router bisa akses internet.

```bash
/ip route add gateway=192.168.1.1
/ip dns set servers=8.8.8.8,8.8.4.4 allow-remote-requests=yes
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade
```

Konsep ujian:
- Default route
- DNS
- NAT masquerade

🛡️ 3. Web Proxy & Blocking
  💡 Biasanya bagian poin terbesar di ujian.

Aktifkan Web Proxy
```bash
/ip proxy set enabled=yes port=3128 cache-administrator=admin@sekolah.sch.id
```
Redirect HTTP ke Proxy
```bash
/ip firewall nat add chain=dstnat protocol=tcp dst-port=80 action=redirect to-ports=3128
```
Blokir Website (Contoh)
```bash
/ip proxy access add dst-host=httpforever.com action=deny
```
Catatan penting:
- Proxy hanya bekerja untuk HTTP (port 80)
- HTTPS tidak sepenuhnya bisa diblok tanpa metode tambahan

🛣️ 4. Static Routing
Digunakan jika diminta routing ke network lain.
```bash
/ip route add dst-address=10.10.10.0/24 gateway=192.168.1.2
```
Pastikan:
- Gateway bisa diping
- Tidak ada konflik network

💡 Pro Tips
Cek koneksi setelah NAT:
```bash
ping 8.8.8.8
```
Gunakan tombol Tab untuk auto-complete agar minim typo.
Kalau konfigurasi kacau:
```bash
/system reset-configuration no-defaults=yes
```
Reset bukan kalah — reset itu strategi.

🌸 Meme of the Day

“Kalau merah berarti salah,
kalau biru berarti benar,
kalau item… berarti kamu lupa nyalain routernya.”
