# Go-ABI
Go-ABI - is a built ABI package in go language.

Support standards following below.
- ERC20
- ERC721
- ERC1155

### Install package
```
go get github.com/nattaponra/go-abi
```

### Example
```go
package main

import (
	"fmt"

	"github.com/ethereum/go-ethereum/accounts/abi/bind"
	"github.com/ethereum/go-ethereum/common"
	"github.com/ethereum/go-ethereum/ethclient"
	erc721 "github.com/nattaponra/go-abi/erc721/contract"
)

func main() {
	client, err := ethclient.Dial("https://cloudflare-eth.com")
	if err != nil {
		panic(err)
	}
	// holder address
	holderAddress := common.HexToAddress("0xdbfd76af2157dc15ee4e57f3f942bb45ba84af24")
  
	//Bored Ape Yacht Club: BAYC Token
	contractAddress := common.HexToAddress("0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D")
	contract, err := erc721.NewContract(contractAddress, client)
	if err != nil {
		panic(err)
	}

	balance, err := contract.BalanceOf(&bind.CallOpts{}, holderAddress)
	if err != nil {
		panic(err)
	}

	fmt.Println(balance)

}

```
