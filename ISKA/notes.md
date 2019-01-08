# ISKA Notes

## General config

Rpc: `http://ethvtnlhf-dns-reg1.westeurope.cloudapp.azure.com:8540/`\
Private key: `39e5f75128e664ee13836b85f24f30c0c9983b0a9e6584895a7eb6fcc5f832b3`

## Web3

### Dependency

```groovy
implementation ('org.web3j:core:4.0.0')
```

### Config

```kotlin
object Web3Config {
    private const val privateKey = "39e5f75128e664ee13836b85f24f30c0c9983b0a9e6584895a7eb6fcc5f832b3"
    private const val rpcEndpoint = "http://ethvtnlhf-dns-reg1.westeurope.cloudapp.azure.com:8540/"


    private val gasPrice = BigInteger.ZERO
    private val gasLimit = BigInteger("6721975")

    val gasProvider = StaticGasProvider(gasPrice, gasLimit)


    val web3 =  Web3j.build(HttpService(rpcEndpoint))
    val credentials = Credentials.create(privateKey)

    val contract by lazy {
        IskaContract.load("0xd6f6a3bddf5c2b444f7156a98085ceddfb0df261", web3, credentials, gasProvider)
    }
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
