# How to launch Gnosis Chain validator node with Docker Compose and Nethermind

1. Install Docker Engine and Docker Compose following the original instructions https://docs.docker.com/get-docker/ and https://docs.docker.com/compose/install/

2. Clone this repo:

    ```bash
    $ git clone -b nethermind https://github.com/gnosischain/validator-node-dockerized
    $ cd validator-node-dockerized
    ```

3. To be a validator, you need to have your mining address private key. You will keep it in a `.env` file.

    If you don't have the private key in a plain format (a hex string, 64 characters long), but have a JSON Keystore file of it (with a password), please go through the following steps to get your plain private key string:

    - Open your MetaMask.
    - Go to `Import Account`.
    - In the `Select Type` drop-down list choose `JSON File`.
    - Point to your JSON Keystore file, enter the password for it, and click `Import` button.
    - Switch to the newly imported account and go to `Account details`. Click `Export private key` button.
    - On the appeared `Show Private Keys` section type your MetaMask password and click `Confirm`.
    - You will see your 64 characters long private key.

4. Copy `.env.example` to `.env` and configure the `.env` file. There are a few settings you need to define:

    ```
    ETHSTATS_ID=[validator_name]
    ETHSTATS_CONTACT=[contact_email]
    ETHSTATS_SECRET=[netstat_secret_key]
    KEY=[your_private_key_for_mining_address]
    SEQAPIKEY=[seq_api_key]
    ```

    - `ETHSTATS_ID` - The displayed name of your validator in [Netstats](https://dai-netstat.poa.network/).
    - `ETHSTATS_CONTACT` - Validator's contact (e.g., e-mail).
    - `ETHSTATS_SECRET` - Secret key to connect to Netstat (should be provided by xDai team, please, request it).
    - `KEY` - Your mining address private key (should be 64 characters long without leading `0x`).
    - `SEQAPIKEY` - An API key for [Seq](https://datalust.co/seq) log collector (should be provided by xDai team, please, request it).

5. Start your node.

    ```bash
    $ docker-compose up -d
    ```

6. (optional) Remove your private key from the `.env` file. After your docker container is created and started, it doesn't need the key anymore, so the key can be removed from `.env` for security reasons. **But note, that if you `down` your container, you will need to specify the key again before you `up` (recreate) the docker container, so wiping your key is not recommended if you down and up your node often.**

After docker containers are created, the node will sync with the chain (may take a while).

To restart you need to use `docker-compose stop` and `docker-compose start` being in the `validator-node-dockerized` directory.
