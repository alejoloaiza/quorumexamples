# TESTS USING QUORUM AND IBFT

## Pre-Requisites:
Go 1.10 installed with $GOPATH configured.
Istanbul tools installed. 
`go get github.com/getamis/istanbul-tools`
Geth (go-Ethereum)
## Installation: 
`go get github.com/alejoloaiza/quorumexamples`

# Test data:

**Dataset 1:** 
The idea is to test with 7 validator nodes and see when block creation starts.  
`istanbul setup --num 7 --docker-compose --verbose --quorum --save`

This command will create a docker-compose.yml.
Now we will bring up some of the images, not all.

`export COMPOSE_PROJECT_NAME=quorum`
`docker-compose -f docker-compose.yml up -d eth-stats constellation-0 constellation-1 constellation-2 constellation-3 validator-0 validator-1 validator-2 validator-3`

We bring up 4 nodes, to see if blocks are getting generated. Wait a couple of seconds and then run this command.

`geth attach http://localhost:8545`

You will see a console like this:

```Welcome to the Geth JavaScript console!```

```instance: Geth/validator-0/v1.7.2-stable/linux-amd64/go1.9```
```coinbase: 0xa81807268ae6e6f8dddaeac7a75001c764d9d81f```
```at block: 0 (Sun, 12 Aug 2018 22:00:22 -05)```
``` modules: eth:1.0 istanbul:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0```

That means there are no blocks being generated with 4 validators, so lets add one more.

`docker-compose -f docker-compose.yml up -d constellation-4 validator-4`

Now if you have some patience and wait a couple of minutes, you will notice this:

```Welcome to the Geth JavaScript console!```

```instance: Geth/validator-0/v1.7.2-stable/linux-amd64/go1.9```
```coinbase: 0xa81807268ae6e6f8dddaeac7a75001c764d9d81f```
```at block: 9 (Sun, 12 Aug 2018 22:23:48 -05)```
``` modules: eth:1.0 istanbul:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0```