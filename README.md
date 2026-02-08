# 🚀 Mikrotik

> *“May your ping be low and your grade be high.”*  
> — (｡•̀ᴗ-)✧ **AzmiiDev** and **Deepsky121**

![MikroTik](https://img.shields.io/badge/MikroTik-RouterOS-blue)
![Networking](https://img.shields.io/badge/Topic-Networking-green)

Panduan singkat & praktis  
Disusun ringkas, dan langsung bisa dieksekusi via **Terminal RouterOS**.

---

## 📝 1. Basic & IP Address

> ⚠️ **Catatan:**  
> Ganti `ether2`, `ether3`, atau `192.168.x.x` sesuai instruksi

```bash
/system identity set name="Peserta-Ujian-Ganteng"

/ip address add address=192.168.10.1/24 interface=ether2
/ip address add address=192.168.20.1/24 interface=ether3
```
Digunakan untuk:
- Identitas router
- IP lokal ke jaringan client

## 2. 🌐 Internet Gateway (NAT & Route)

Biar client di bawah router bisa buka Google.

```bash
/ip route add gateway=192.168.1.1
/ip dns set servers=8.8.8.8,8.8.4.4 allow-remote-requests=yes
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

```

## 3. 🛡️ Web Proxy & Blocking

Ini biasanya bagian yang paling banyak poinnya di ujian.

```bash
# Aktifkan Proxy
/ip proxy set enabled=yes port=8080 cache-administrator=admin@sekolah.sch.id

# Redirect Traffic HTTP (Port 80) ke Proxy (Port 8080)
/ip firewall nat add chain=dstnat protocol=tcp dst-port=80 action=redirect to-ports=8080

# Contoh Blokir Situs (misal: linux.org)
/ip proxy access add dst-host=www.linux.org action=deny

```

## 🛣️ 4. Static Routing (Add Address)

Kalau disuruh routing ke network sebelah:

```bash
/ip route add dst-address=10.10.10.0/24 gateway=192.168.1.2

```

## 🌸 Meme of the Day

> **"Kalo merah berarti salah, kalo biru berarti bener, kalo item... berarti kamu lupa nyalain routernya."**

### 💡 Pro-Tips Terakhir:

1. **Cek Koneksi:** Selalu `ping 8.8.8.8` dari terminal setelah setting NAT.
2. **Tab Key:** Gunakan tombol **Tab** di keyboard buat auto-complete perintah biar nggak typo.
3. **Reset is Life:** Kalau settingan berantakan, ketik: `/system reset-configuration no-defaults=yes`.
**Reset bukan kalah — reset itu strategi.**
