version: "3"

services:
  testnet-validator-node:
    image: $QCLIENT_IMAGE
    entrypoint: ["geth", "--ethstats=bayramov:qstats-testnet@stats.qtestnet.org", "--bootnodes=$BOOTNODE21_ADDR", "--datadir=/data", "--nat=extip:$IP", "--port=$EXT_PORT", "--unlock=$ADDRESS",  "--password=/data/keystore/pwd.txt", "--mine", "--miner.threads=1", "--syncmode=full", "--rpc.allow-unprotected-txs", "--testnet", "--verbosity=3", "--miner.gasprice=1"]
    volumes:
      - ./keystore:/data/keystore
      - ./additional:/data/additional
      - testnet-validator-node-data:/data
    ports:
      - $EXT_PORT:8545/tcp
      - $EXT_PORT:8545/udp
    restart: unless-stopped

volumes:
  testnet-validator-node-data:
