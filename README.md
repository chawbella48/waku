# waku
waku node operate

DONANM
2 CPU 2 RAM - 40 SSD

# Sunucu güncellemesi ve gerekli paketler
sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential git libpq5 jq -y

# kodu girdikten sonra 1 seçelim.
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"

sudo apt install docker.io -y
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Waku kurulumu

# wakuyu klonluyoruz
git clone https://github.com/waku-org/nwaku-compose
cd nwaku-compose
cp .env.example .env

# .env içine giriyoruz bu komutla
nano .env

Değiştireceğimiz kısımlar bunlar aşağıya yazıyorum:

ETH_CLIENT_ADDRESS = Infura'dan Sepolia RPC aldım bedava onu ekledim - https://www.infura.io/
ETH_TESTNET_KEY = Waku için açtığım metamaskın private keyini ekledim - Metamask hesap bilgileri kısmında
RLN_RELAY_CRED_PASSWORD = Bir şifre belirledim
CTRL X Y ENTER ile kaydedip çıkıyoruz.

# ve register edelim.
./register_rln.sh
# register etmeden önce cüzdanda sepolia eth olmalı  

Waku node başlatma

# portları açma

# yes diyelim bu komutu girdikten sonra
sudo ufw enable

# bu port komutlarını toplu girebilirsiniz.
sudo ufw allow 22    
sudo ufw allow 3000   
sudo ufw allow 8545   
sudo ufw allow 8645   
sudo ufw allow 9005   
sudo ufw allow 30304  
sudo ufw allow 8645

# docker up edelim
docker-compose up -d

# bu komutlar ile kontrol edebilirsin logları
docker-compose ps
docker-compose logs nwaku
