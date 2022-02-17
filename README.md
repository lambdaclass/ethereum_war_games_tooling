Install dependencies with

```
make init
```

On a separate terminal tab

```
make eth_node
```

Then deploy the test contract with

```
make deploy_test_contract
```

The output should look like this

```
forge create --rpc-url http://127.0.0.1:8545 Storage --root contracts/ --private-key df57089febbacf7ba0bc227dafbffa9fc08a93fdc68e1e42411a14efcf23656e
compiling...
Compiling 1 files with 0.8.10
Compilation finished successfully
Compiler run successful
success.
Deployer: 0x8626f6940e2eb28930efb4cef49b2d1f2c9c1199
Deployed to: 0xb581c9264f59bf0289fa76d61b2d0746dce3c30d
Transaction hash: 0xe2c19a2f0766c0e00c416433a8cf53c9993fc918e2b321f348d8de421c195416
```

Take note of the address you are given after `Deployed to:`, as that is the contract's address in the local chain.
With it, you can now call its test function using `cast` like this:

```
cast call 0xb581c9264f59bf0289fa76d61b2d0746dce3c30d "test_function()(uint256)" --rpc-url http://localhost:8545
```

which should return `1`.


You can also send a transaction to call the `store` function

```
cast send 0xb581c9264f59bf0289fa76d61b2d0746dce3c30d --private-key ac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 "store(uint256)" 5 --rpc-url http://localhost:8545
```

where the first address is the contract's address and the private key needs to have some funds to pay for the transaction. Output should look like this

```
blockHash            "0xd2f9afae4ef28c63ceccd7575c4370c17ead74448567ca651ec82a7051434e01"
blockNumber          "0x5"
contractAddress      null
cumulativeGasUsed    "0x6746"
effectiveGasPrice    "0xd1790ced"
gasUsed              "0x6746"
logs                 []
logsBloom            "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
root                 null
status               "0x1"
transactionHash      "0x0bc2448d1f7ee4be24bae1201e687d937d5f094af5e64f09ca0b279d62bf0b81"
transactionIndex     "0x0"
type                 "0x2"
```

After storing a number, you can retrieve it with

```
cast call 0xb581c9264f59bf0289fa76d61b2d0746dce3c30d "retrieve()(uint256)" --rpc-url http://localhost:8545
```

