# How to launch xDai validator node with Docker Compose and Nethermind

1. Install Docker Engine and Docker Compose following the original instructions https://docs.docker.com/get-docker/ and https://docs.docker.com/compose/install/

2. Clone this repo:

    ```bash
    $ git clone -b nethermind https://github.com/xdaichain/validator-node-dockerized
    $ cd validator-node-dockerized
    ```

3. In order to be a validator, you need to have your mining address private key. You will keep it in a `.env` file.

4. Copy `.env.example` to `.env` and config the `.env` file. There are a few settings you need to define:

    ```
    ETHSTATS_ID=[validator_name]
    ETHSTATS_CONTACT=[contact_email]
    ETHSTATS_SECRET=[netstat_secret_key]
    KEY=[your_private_key_for_mining_address]
    ```

    - `ETHSTATS_ID` - The displayed name of your validator in [Netstats](https://dai-netstat.poa.network/).
    - `ETHSTATS_CONTACT` - Validator's contact (e.g., e-mail).
    - `ETHSTATS_SECRET` - Secret key to connect to Netstat.
    - `KEY` - Your mining address private key (should be 64 characters long without leading `0x`).

5. Start your node.

    ```bash
    $ docker-compose up -d
    ```

After docker containers are created, the node will sync with the chain (may take a while).

To restart you need to use `docker-compose stop` and `docker-compose start` being in the `validator-node-dockerized` directory.
