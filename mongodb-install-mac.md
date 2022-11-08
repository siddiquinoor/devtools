# Install MongoDB on Mac (Monterey)

Ref: https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/

## Install Xcode Command-Line Tools

    $ xcode-select --install

## Install Homebrew (if not already installed)

https://brew.sh/#install

## Installing MongoDB 6.0 Community Edition

    $ brew tap mongodb/brew

## Update Homebrew

    $ brew update

## Install MongoDB

    $ brew install mongodb-community@6.0

## The installation includes the following binaries:

- The `mongod` server
- The `mongos` sharded cluster query router
- The MongoDB Shell, `mongosh`

## In addition, the installation creates the following files and directories at the location specified below, depending on your Apple hardware:

                        Intel Processor                 Apple M1 Processor

configuration file /usr/local/etc/mongod.conf /opt/homebrew/etc/mongod.conf
log directory /usr/local/var/log/mongodb /opt/homebrew/var/log/mongodb
data directory /usr/local/var/mongodb /opt/homebrew/var/mongodb

## Run MongoDB Community Edition

### To run MongoDB (i.e. the mongod process) as a macOS service, run:

    $ brew services start mongodb-community@6.0

### To stop a `mongod` running as a macOS service, use the following command as needed:

    $ brew services stop mongodb-community@6.0
