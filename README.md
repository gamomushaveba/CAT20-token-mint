<h2 align=center>Mint first CAT20 token CAT on Fractal Mainnet</h2>

# CAT-20

- Install Docker
```bash
sudo apt update && sudo apt install -y curl && curl -fsSL https://get.docker.com -o get-docker.sh && sudo sh get-docker.sh
```
- Install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
- Make this executable
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
- Install `npm`
```bash
sudo apt-get install npm -y
```
- Install `n` pacakges globally
```bash
sudo npm i n -g
```
- Switch to stable node version
```bash
sudo n stable
```
- Install `yarn` package globally
```bash
sudo npm i -g yarn
```
- Clone `Cat Protocol` repo
```bash
git clone https://github.com/CATProtocol/cat-token-box && cd cat-token-box
```
- Install and build this project
```bash
sudo yarn install && yarn build
```
- Change directory to `tracker`
```bash
cd packages/tracker
```
- Run `Fractal Bitcoin` node
```bash
sudo chmod 777 docker/data && sudo chmod 777 docker/pgdata && docker compose up -d
```
- Build docker image under the project root directory
```bash
cd ../../ && docker build -t tracker:latest .
```
- Run the container
```bash
docker run -d \
    --name tracker \
    --add-host="host.docker.internal:host-gateway" \
    -e DATABASE_HOST="host.docker.internal" \
    -e RPC_HOST="host.docker.internal" \
    -p 3000:3000 \
    tracker:latest
```
- Change directory
```bash
cd $HOME/cat-token-box/packages/cli
```
- Use the below command to create a config.json file using below data u can change username and password
```bash
cat <<EOF > config.json
{
  "network": "fractal-mainnet",
  "tracker": "http://127.0.0.1:3000",
  "dataDir": ".",
  "maxFeeRate": 30,
  "rpc": {
      "url": "http://127.0.0.1:8332",
      "username": "ZunXBT",
      "password": "ZunXBT"
  }
}
EOF
```
- Use below command to create a wallet address
```bash
sudo yarn cli wallet create
```
- You can see your wallet address using this command
```bash
yarn cli wallet address
```
- Now u need to have $FB in order to mint CAT token, so to get $FB , first import these seed phrase in [Unisat Wallet](https://chrome.google.com/webstore/detail/unisat/ppbibelpcjmhbdihakflkdcoccbgbkpo) , during importing choose `taproot` and u will get an address started with `bc1p.......`
- Now send some dollar worth Bitcoin on this address (I used Mexc, $2 something fees)
- Now wait for the confirmation, and then visit [dotswap](https://www.dotswap.app/v1/swap#F_BTC_FB) and deposit BTC to this platform and then swap from BTC to FB using this platform, after swapping withdraw FB from this platfotm to your wallet address
- Now mint using below command
```bash
sudo yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate 120
```
** You should change the fee-rate according to the current market fee
- You can check balance using this command
```bash
sudo yarn cli wallet balances
```
- Done ✅