# Mgbchain

# 1. Create a directory:
mkdir -p Node-5/data

#2. Clone Mgbchain git.

 #3. Start the node:
./besu --data-path=data --genesis-file=../genesis.json --bootnodes=<Node-1 Enode URL> --p2p-port=30307 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8549

#4. Copy the address of the node:
Copy the address of the node. You can find the address in the logs when starting the new node

(or)

./besu --data-path=Node-5/data public-key export-address

#5. Add a validator:
Propose adding the new validator from more than half the number of current validators, using ibft_proposeValidatorVote, specifying the address of the proposed validator and true

curl -X POST --data '{"jsonrpc":"2.0","method":"ibft_proposeValidatorVote","params":["<node_address>", true], "id":1}' http://127.0.0.1:8545

#6. Verify the addition of the new validator:
curl -X POST --data '{"jsonrpc":"2.0","method":"ibft_getValidatorsByBlockNumber","params":["latest"], "id":1}' http://127.0.0.1:8545

#5. Remove a validator:
The process for removing a validator is similar to adding a validator starting from step 5, except you specify false as the second parameter of ibft_proposeValidatorVote.

curl -X POST --data '{"jsonrpc":"2.0","method":"ibft_proposeValidatorVote","params":["<node_address>", false], "id":1}' http://127.0.0.1:8545

