# Create your own ocean

### DeFiChain Mainnet Node
DeFiChain Masternode/Fullnode Installationscript incl. API and Ocean

#### Requirements

- Debian 10/11 or Ubuntu 20.04/22.04 (KVM virtualization recommended)
- 6-8 Cores
- 16-32 GB Memory
- 480 GB SSD/NVMe
- Registered Domain or Subdomain pointing to the IP address of your server

> :warning: Please note, the Script install Apache and configure it and change your Hostname and disable root-Access. Please use it only on a fresh installed system to avoid problems.  For test purposes only! You can compare your Node with https://explorer.mydefichain.com/blocks to check correkt Chain and Blockheight/Hash.

#### Installation

Login to your Server with SSH (Putty) as a root-User

```wget https://raw.githubusercontent.com/mydefichain/ocean/main/install_ocean.sh```  
```chmod 744 ./install_ocean.sh```  
```./install_ocean.sh USERNAME SERVERNAME DOMAIN VERSION```  

#### Actual Version

Here you will find information about the latest version and what to look out for:

AIN: https://github.com/DeFiCh/ain/releases/latest

Jellyfish: https://github.com/JellyfishSDK/jellyfish/releases/latest

---
#### Example

```./install_ocean.sh defichain myocean freedomain.com 3.2.7```  

The Script creates a user named "defichain" and your Server is reachable at http://myocean.freedomain.com  

---

*You need a public DNS Record that points this Domain to your public IP-Address of your Server.*

After the Script is finished, restart your Server with ```shutdown -r now``` and Login with your newly created user and your new password.

Type ```su USERNAME /home/USERNAME/install_user.sh```

Example: ```su defichain /home/defichain/install_user.sh```

This second Script install the correct AIN-Version and use the latest Snapshot of the Mainnet.

#### Docker Configuration

Edit your Configuration File ~/whale/docker-compose.yml. You can use Midnight Commander for easier handling. Type ```mc```, F4 for edit.

```Line 5: Set actual Version of AIN
Line 9: Change the username to the one you have chosen.
Line 18/19: Insert rpcuser and rpcpassword (freely definable)
Line 35: Set actual Version of Jellyfish
Line 39: Change the username to the one you have chosen.
Line 45: Change th RPC-URL and replace rpcuser and rpcpassword with the data from Line 18 and 19.
```

#### Start Ocean

Change to your Directory with your docker-compose.yml: ```cd ~/whale/```

Create Network: ```sudo docker network create ocean```

Start Ocean: ```sudo docker-compose up -d```

Finished. You can use your Oceannode and can reach your API with http://myocean.freedomain.com/api/. The Ocean URL listen on http://myocean.freedomain.com:3000

Try the Configuration with http://myocean.freedomain.com:3000/v0/mainnet/stats/

To check your log, use ```sudo docker-compose logs -f -t --tail=10```

Questions? Join us on Telegram https://t.me/mydefichain
