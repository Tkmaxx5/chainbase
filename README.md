![image](https://github.com/user-attachments/assets/412a7544-5504-4aeb-8b5a-fa99f73acf6b)

# chainbase
Chainbase is the world’s largest omnichain data network designed to integrate all blockchain data into a unified ecosystem, providing an open and transparent data interoperability layer for the AI era.
It has designed a novel dual-chain technology architecture that bridges the programmability and composability of crypto data, which supports high throughput, low latency, and eventual determinism, as well as higher cybersecurity through a dual staking model.

# Fund your Eigen wallet
You’ll need at least 2 Holesky ETH to cover the gas cost of the operator registration.

## Link faucet Holesky ETH: 
https://cloud.google.com/application/web3/faucet/ethereum/holesky
https://holesky-faucet.pk910.de/

## Run a Chainbase AVS Operator
​
### Overview
This guide will walk you through the process of setting up and running a Chainbase AVS (Actively Validated Service) operator node.

## https://docs.chainbase.com/node/operator

### Requirements
Recommended Hardware Specifications

Class	vCPUs (10th gen+)	Memory	Networking Capacity
General Purpose - large	2	8 GB	5 Mbps
General Purpose - xl	4	16 GB	25 Mbps
General Purpose - 4xl	16	64 GB	5 Gbps
Before you begin, ensure you have the following prerequisites installed:

➕Docker: Docker is a requirement for AVS operator node.

➕Docker Compose: Docker Compose is used alongside Docker for executing operator node.

➕ Linux Environment: Eigenlayer’s CLI only runs in a Linux environment.

➕Go: Two out of three installation routes require the use of Go. It’s safer to go with Go than go without. 😉

### Installation Process
​
Migration From Previous Version
If you’ve previously run a Chainbase AVS operator node:

You can delete old version chainbase-avs-setup directory on your server, but need to back up your encrypted ECDSA and BLS keys.
Skip the EigenLayer Registration step and only start from Chainbase AVS Setup step.
​
EigenLayer Registration
Ensure you’ve registered with EigenLayer before proceeding. For guidance, refer to the EigenLayer Operator Installation Guide.

​### Chainbase AVS Setup
Clone the Chainbase AVS setup repository:
```
git clone https://github.com/chainbase-labs/chainbase-avs-setup
```
run a Chainbase AVS operator node on mainnet (invited and whitelisted):

```
cd chainbase-avs-setup/mainnet
```
OR run a Chainbase AVS operator node on testnet (no restrictions):

```
cd chainbase-avs-setup/holesky
```

Set up the environment file:
```
cp .env.example .env
```
Configure all fields in the .env file with your specific information:

```
NODE_ECDSA_KEY_FILE_PATH=/your/ecdsa/key/path
NODE_BLS_KEY_FILE_PATH=/your/bls/key/path
OPERATOR_ECDSA_KEY_PASSWORD=yourECDSAKeyPassword
OPERATOR_BLS_KEY_PASSWORD=yourBlsKeyPassword
OPERATOR_ADDRESS=yourECDSAKeyAddress
NODE_SOCKET=yourNodeSocket
OPERATOR_NAME=yourOperatorName
```

Use the command eigenlayer operator keys list to retrieve information about your ECDSA and BLS key paths and operator address.
- OPERATOR_ADDRESS: Set to your operator address (must match your ECDSA key address).
- NODE_SOCKET: Set to your server’s public IP address (format: <your_server_public_ip>:8011).

Important:
Ensure your server’s public IP is internet-accessible.
Verify that port 8011 is open and properly configured in your firewall settings.
Set execution permissions for the script:
```
chmod +x ./chainbase-avs.sh
​```
Operating the Chainbase AVS
​
## Register as an Operator
Run the following command to register as an operator:

```
./chainbase-avs.sh register
​```

## Run Node
Run the following command to startup node:

``` ./chainbase-avs.sh run ```

## Test Node
Run the following command to test node:

```
./chainbase-avs.sh test
```

- If you see the output All systems are working for your manuscript node in the command line output, it indicates that your node is running correctly.
- ​Update Node socket: If your server’s public IP address is changed after you register as an operator, you need to update the node socket. Configure NODE_SOCKET in .env file, then run the following command:

``` ./chainbase-avs.sh socket ```
​
## Update Node version
Run the following command to update node version:

```
./chainbase-avs.sh stop
./chainbase-avs.sh update
./chainbase-avs.sh run
​```

## Monitor Logs: View container logs using any of these commands:
```
docker compose logs -f
docker compose logs -f <container_name>
docker logs -f <container_id>
```

## Dashboard
You can visit <your_server_public_ip>:3010 on browser to view the dashboard to confirm the status of your node.If you are unable to access the page in your browser, please verify that port 3010 on your server is open and properly configured in firewall settings.

