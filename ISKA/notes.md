# ISKA Notes

## General config

Rpc: `HTTP://127.0.0.1:8545`\
Private key: `...` (check ganache)

## Web3

### Dependency

```groovy
implementation ('org.web3j:core:4.0.0')
```

### Config

```kotlin
object Web3Config {

    val privatKey = "..." // Check ganache
    val web3 =  Web3j.build(HttpService("HTTP://127.0.0.1:8545"))
    val credentials = Credentials.create(privateKey)

    val contract = IskaContract.load("0xd6f6a3bddf5c2b444f7156a98085ceddfb0df261", web3, credentials, DefaultGasProvider())
}
```

### Deploy

```kotlin
IskaContract.deploy(Web3Config.web3, Web3Config.credentials, Web3Config.gasProvider)
```

### Call

```kotlin
Web3Config.contract.updateKmStand(kms.toBigInteger()).send()
```

## Contract

### Code

```sol
pragma solidity ^0.5.0;

contract IskaContract {

    mapping(address => uint) kmStanden;


    function updateKmStand(uint n) public {
        address owner = msg.sender;

        require(kmStanden[owner] < n, "Je kan geen lagere km stand invullen dan de laatste nieuwe");

        kmStanden[owner] = n;
    }

    function getKmStand() public view returns(uint) {
        return kmStanden[msg.sender];
    }

}
```

### Compilen

```bash
solc IskaContract.sol --bin --abi --optimize -o . --overwrite
```

```bash
web3j solidity generate -b IskaContract.bin -a IskaContract.abi -p com.infosupport.iskademo -o ../src/main/java
```
