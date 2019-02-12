# hyperledger_fabric_sandbox
Sandbox for experiments and code samples pertaining to all things HyperLedger Fabric

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