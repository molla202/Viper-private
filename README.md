![image](https://github.com/molla202/Viper-private/assets/91562185/83832c2d-997b-4f4c-992a-6bee394b5891)


 * [Topluluk kanalımız](https://t.me/corenodechat)<br>
 * [Topluluk Twitter](https://twitter.com/corenodeHQ)<br>
 * [Galactica Network Website](https://galactica.com/)<br>
 * [Blockchain Explorer](https://explorer.corenodehq.com/Galactica%20Testnet)<br>
 * [Discord](https://discord.gg/JvynTZAr)<br>
 * [Twitter](https://twitter.com/GalacticaNet)<br>
 * [FAUCET](https://faucet-reticulum.galactica.com/)<br>

## 💻 Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler | 
| ------------ | ------------ |
| CPU |	4|
| RAM	| 8+ GB |
| Storage	| 400 GB SSD |

### 🚧Gereklilikler ve Update
```
sudo apt -q update
sudo apt -qy install curl git jq lz4 build-essential
sudo apt -qy upgrade
```
### 🚧GO
```
ver="1.21.3" &&
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" &&
sudo rm -rf /usr/local/go &&
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" &&
rm "go$ver.linux-amd64.tar.gz" &&
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile &&
source $HOME/.bash_profile &&
go version
```

### Dosyaları çekelim
```
wget -O /usr/local/bin/viper http://37.120.189.81/viper/viper
```
```
chmod +x /usr/local/bin/viper
```
Not: altaki kodu girince cüzdan olusuyor şifre soruyor. yazarken görunmez ama yazar cıkan cıktıyı kaydedin.
```
viper wallet create-account
```
![image](https://github.com/molla202/Viper-private/assets/91562185/b9a96691-6add-4a9a-9436-16c7c49efef2)

Not: Adress yazan yazıyı silip yukarıdaki çıkan cüzdan adresini yazıcaksınız.

viper servicers create-validator address

![image](https://github.com/molla202/Viper-private/assets/91562185/928ca790-8448-434b-8eb5-d04d42d1a275)

- Dicorda gidiyoruz rolunuz varsa #🤑|req-tokens kanalını göruceksınız linki var botun girin açılacak oraya adres yazıp fauceti alın işlemlere devam etmeden once biraz bekleyin.
```
echo $(viper util print-configs) | jq '.tendermint_config.P2P.Seeds = "6304da172fce20a6039a6eb5c9154cb8056c0ed6@testnet-seed1.vipernet.xyz:26656"' | jq . > ~/.viper/config/configuration.json
```
```
viper util gen-chains
```
- soru soracak ilkine 0001 sonrakine http://127.0.0.1:8082/ daha sonrakinede enter ve n deyip bitiriyoruz.

![image](https://github.com/molla202/Viper-private/assets/91562185/24b05386-1e62-477d-92f3-1c65e5d5a78e)
```
viper util gen-geozone
```
- 0001 yazıp enterlıyoruz

![image](https://github.com/molla202/Viper-private/assets/91562185/eb571cf2-c0ea-49e2-9265-6aeec97d00ee)
```
cd ~/.viper/config
```
```
wget https://raw.githubusercontent.com/vipernet-xyz/genesis/main/testnet/genesis.json genesis.json
```
```
ulimit -Sn 16384
```

### Servis olsuturalım
```
sudo tee /etc/systemd/system/viper.service > /dev/null << EOF
[Unit]
Description=viper service
After=network.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
User=root
Group=sudo
ExecStart=/usr/local/bin/viper network start
ExecStop=/usr/local/bin/viper network stop

[Install]
WantedBy=default.target
EOF
```
```
sudo systemctl daemon-reload
sudo systemctl enable viper.service
sudo systemctl restart viper.service
```
### Port ayarları opsiyonel
NOT: baska standart port proje varsa
```
echo "export viper_PORT="12"" >> $HOME/.bash_profile
source $HOME/.bash_profile
```
```
sed -i.bak -e "s%:26658%:${viper_PORT}658%g;
s%:26657%:${viper_PORT}657%g;
s%:26660%:${viper_PORT}060%g;
s%:26656%:${viper_PORT}656%g" $HOME/.viper/config/configuration.json
```















