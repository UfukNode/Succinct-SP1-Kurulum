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

> Bu kurulumu boşta duran ya da hâlihazırda çalışan sunucularınız üzerine de yapabilirsiniz.

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

### Kurulumu Doğrula:

```bash
cargo prove --version
cargo +succinct --version
```

---

## 4. SP1 Projesi Oluştur (Fibonacci)

```bash
cargo prove new --bare fibonacci
cd fibonacci
```

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

```
Address:      0xYourAddress
Private Key:  0xYourPrivateKey
```

Private key'inizi kimseyle paylaşmayın.

---

## 7. Programı Test Et

```bash
cd ../script
RUST_LOG=info cargo run --release -- --execute
```
Başarılıysa aşağıda bulunan görseldeki satırları görmelisiniz:

Çıktı:

```
Program executed successfully.
a: 6765
b: 10946
```

---

## 8. Proof Üretimi (Keypair ile)

```bash
SP1_PRIVATE_KEY=0xyourprivatekey RUST_LOG=info cargo run --release -- --prove
```

Başarılıysa aşağıda bulunan görseldeki satırları görmelisiniz:

```
Successfully generated proof!
Successfully verified proof!
```
## 9. Opsiyonel: Proof'u Succinct Ağı Üzerinden Üretmek:

Eğer proof'unuzun Succinct ağına gönderilmesini ve on-chain olarak işlenmesini istiyorsanız, aşağıdaki komutla çalıştırabilirsiniz:

```bash
SP1_PROVER=network \
NETWORK_PRIVATE_KEY=0xyourprivatekey \
NETWORK_RPC_URL=https://rpc.production.succinct.xyz \
RUST_LOG=info \
cargo run --release -- --prove
```

---

Artık bu proje ile Succinct Prover Network whitelist [form](https://docs.google.com/forms/d/e/1FAIpQLSd-X9uH7G0bvXH_kjptnQtNil8L4dumrVPpFE4t8Ci1XT1GaQ/viewform)'una başvurabilirsiniz. Herkese başarılar dilerim.

---

X Hesabım: [@UfukDegen](https://x.com/UfukDegen) 
Daha fazla rehber için: https://github.com/UfukNode
