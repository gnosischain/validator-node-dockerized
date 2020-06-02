# How to launch xDai validator node with Docker Compose

1. Install Docker Engine and Docker Compose following the original instructions https://docs.docker.com/get-docker/ and https://docs.docker.com/compose/install/

2. Clone this repo:

    ```bash
    $ git clone https://github.com/xdaichain/validator-node-dockerized
    $ cd validator-node-dockerized
    ```

3. In order to be a validator, you need to have a mining address and a private key for it. Name your JSON keystore file as `key` and put it to the `validator-node-dockerized` directory. Put keystore's password to `password` file.

4. Config `.env` file. There are a few settings you need to define:

    ```
    ETHSTATS_ID=[validator_name]
    ETHSTATS_CONTACT=[contact_email]
    ETHSTATS_SECRET=[netstat_secret_key]
    EXT_IP=[server_external_ip]
    ACCOUNT=[0x_your_mining_address]
    ```

    - `ETHSTATS_ID` - The displayed name of your validator in [Netstats](https://dai-netstat.poa.network/).
    - `ETHSTATS_CONTACT` - Validator's contact (e.g., e-mail).
    - `ETHSTATS_SECRET` - Secret key to connect to Netstat.
    - `EXT_IP` - External IP of the current server.
    - `ACCOUNT` - Your mining address (beginning from `0x`).

5. Start your node and Netstat service.

    ```bash
    $ docker-compose up -d
    ```

After docker containers are created, the node will sync with the chain (may take a while).

To restart you need to use `docker-compose stop` and `docker-compose start`.
