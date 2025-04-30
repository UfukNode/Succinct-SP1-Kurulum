<img width="1290" alt="sp1-95bcd700ff147045135ad0d0e96a2722" src="https://github.com/user-attachments/assets/f94acd10-038f-45dd-9248-f03fa0ab4a43" />

# Succinct SP1 Fibonacci zkVM Programı Kurulum ve Proof Üretim Rehberi

Bu rehberde, SP1 kurulumu yapıp örnek bir zkVM programı derleyerek nasıl proof üreteceğinizi ve ardından whitelist formunu nasıl dolduracağınızı adım adım anlattım.  
Hiçbir hata almadan, birebir uygun şekilde ilerleyebilirsiniz.

---

| Gereksinim              | Detaylar                                 |
|------------------------|------------------------------------------|
| RAM                    | En az 4 GB RAM                          |
| Depolama               | En az 25 GB SSD                         |
| İşletim Sistemi        | Ubuntu 22 veya üzeri                    |
| vCPU                   | En Az 2 vCPU                            |


## Sunucu Önerileri

**Ücretsiz:**

- [https://www.digitalocean.com/](https://www.digitalocean.com/) → Kredi veriyor, kredi ile sunucu kiralayabilirsiniz.

**Ücretli:**

- [https://contabo.com/en/vps/cloud-vps-4c/](https://contabo.com/en/vps/cloud-vps-4c/) → 6$ civarı, en ucuzunu seçebilirsiniz.

> Bu kurulumu boşta duran ya da hâlihazırda çalışan sunucularınız üzerine de yapabilirsiniz. Boşuna para harcamanıza gerek yok.

---

## 1. Gereksinimleri Kur:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential git curl gcc make jq clang protobuf-compiler pkg-config libssl-dev -y
```

---

## 2. Rust Kurulumu:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

---

## 3. SP1 CLI & Toolchain Kurulumu:

```bash
curl -L https://sp1up.succinct.xyz | bash
source ~/.bashrc
sp1up
```

---

## 4. SP1 Projesi Oluştur (Fibonacci)

```bash
cargo prove new --bare fibonacci
cd fibonacci
```
Örnek Çıktı:

![image](https://github.com/user-attachments/assets/b60ba49e-0bd7-4cc3-8a7d-796723a38dc7)

---

## 5. Programı Derle

```bash
cd program
cargo prove build
```

---

## 6. Wallet Oluştur

### A. Foundry Kurulumu

```bash
curl -L https://foundry.paradigm.xyz | bash
source ~/.bashrc
foundryup
```

### B. Cüzdan Kurulumu:

```bash
cast wallet new
```

Örnek çıktı:

![Adsız tasarım (1)](https://github.com/user-attachments/assets/687817c1-7383-470f-895c-97915560e3ff)

⚠️ Private key'inizi kaydedin ve kimseyle paylaşmayın.

---

## 7. Programı Test Et

```bash
cd ../script
RUST_LOG=info cargo run --release -- --execute
```
- Başarılıysa en sonunda aşağıda bulunan görseldeki satırları görmelisiniz:

Örnek Çıktı:

![image](https://github.com/user-attachments/assets/43a4b1c6-9d11-4e6c-b5bc-e0f7f41dcef4)

---

## 8. Proof Üretimi (Keypair ile)

```bash
SP1_PRIVATE_KEY=Private_Keyini_Gir RUST_LOG=info cargo run --release -- --prove
```
- "Private_Keyini_Gir" kısmına, oluşturduğunuz cüzdanın private key'ini girin.

Komut başarılı çalıştıysa, aşağıdaki görselde yer alan satırları görmelisiniz:

![Ekran görüntüsü 2025-04-29 191455](https://github.com/user-attachments/assets/705e900a-97cb-43c1-9d0a-6a290db06e54)

---

Artık bu proje ile Succinct Prover Network whitelist [form](https://docs.google.com/forms/d/e/1FAIpQLSd-X9uH7G0bvXH_kjptnQtNil8L4dumrVPpFE4t8Ci1XT1GaQ/viewform)'una başvurabilirsiniz. Herkese başarılar dilerim.

---

→ Daha fazla rehber için X hesabımı takip edebilirsiniz: [@UfukDegen](https://x.com/UfukDegen) 
