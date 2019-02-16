# hyperledger_fabric_sandbox
Sandbox for experiments and code samples pertaining to all things HyperLedger Fabric.

## Environment setup prerequisties
- install homebrew and check version using `brew -v`
- install cURL: `brew install curl` and check version using `curl -V`
- install Docker Community Edition (download from website) and check version using `docker -v` and `docker-compose -v` (Docker Compose comes with Docker)
- install Go: `brew install curl` and check version using `go version` and explicitly set 2 environment variables ($GOPATH and the 'bin' folder of your $GOPATH folder is in included in your $PATH):
    - `export GOPATH=$HOME/go`
    - `export PATH=$PATH:$GOPATH/bin`
    - check correct using `echo $GOPATH` and `echo $PATH`
- install NodeJS: `brew install node` and check version using `node -v` and confirm npm (comes with it) is installed `npm -v`
- install HyperLedger Fabric samples and binaries:
    - `cd ~/Desktop/` 
    - start Docker (in Mac, its simply a case of running the app)
    - `curl -sSL http://bit.ly/2ysbOFE | bash -s 1.4.0` (which will install them onto your desktop in a folder called 'fabric-samples', with the main binaries in your 'bin' folder)
    - as at 12/02/2019, one of the npm dependencies requires CommandLineTools installed on Mac (ref https://github.com/nodejs/node-gyp/issues/569)
        - `xcode-select --install` Install Command Line Tools if you haven't already.
        - `sudo xcode-select --switch /Library/Developer/CommandLineTools` Enable command line tools
- Deploying the network
    - cd `first-network`
    - run `./first-network/byfn.sh -h` script to show options on how to do this
    - run `./byfn.sh generate` to generate certs and the genesis block  in order to set up the network, the channel and the identities on the network where we will be making the transactions
    - run  `./byfn.sh up` will run the HyperLedger network (and set up some sample transactions)
    - note: run `./byfn.sh down` brings down the network and clears up the identities/peers and certificates. It also removes the `crypto-config` directory
- Installing your first App
    - Note: Check docker is running on your machine
    `docker rm -f $(docker ps -aq)` - checks you have no active/stale Docker containers running
    `docker network prune` - clears any cached networks
    `docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba` - clears out old chaincode
    `npm install` (in directory with package.json)
    `./startFabric.sh  javascript/go `- starts our Blockchain network and install and instantiate a NodeJS/GoLang version of the FabCar smart contract which will be used by our application to access the ledger
         `docker logs -f ca.example.com` - this creates a log of our Certificate authority example (logs requests and responses to the cert authority)
         `node enrollAdmin.js` - creates the admin user that can create users that can interact with the ledger. Note: it creates a directory called ‘wallet/admin’ with the user, public & private key. Every time we send a transaction to the ledger, the keys here will be used to sign those transactions to be considered valid on the blockchain. Once signed, the info will be sent to the chaincode, the chaincode will sign it with the correct info and then the Ledger will accept the transaction
         `node registerUser.js` - registers a user (once you have created the admin) who can interact with the ledger. Note: it updates the ‘wallet/admin’  with the new user and public/private keys
- Running your first App
    - `node query.js` - Queries the Ledger which stores data in key/value pairs
    - `node invoke.js` - Changes the ledger
   
