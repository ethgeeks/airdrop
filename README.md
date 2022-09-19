# About

**AirDrop** is a command line utility used for mass gas, token and message sending.

**Main features**:

 - Sending of ERC20 tokens to multiple accounts.
 - Sending input data messages (IDMs, https://medium.com/etherscan-blog/ethereum-the-messaging-app-51423e16061f) to multiple accounts.
 - Sending gas to multiple accounts.
 - Harvesting addresses with specific gas / token balances.


# Usage

## Create account

The program works on behalf of a created account.  

```bash
$ ./airdrop create
$ Account: 0x43b60fb17d45B2d0e48C46DA1257ce7fd7BFCfFE 
$ Balance: 0 eth
```

The address and its private key are saved in `account.json` file located in the same folder as the binary.

You can edit the file manually and type pre-existing address and its private key.
 
## Send some gas to the account

Send some gas to the account address so that **AirDrop** can perform its functions.

To check the balance of the account:

```bash
$ ./airdrop info
$ Account: 0x43b60fb17d45B2d0e48C46DA1257ce7fd7BFCfFE
$ Balance: 0.001 eth
```

## Mass sending

### Send message to multiple accounts

The command `message` takes two arguments, the path of a text file with the message and the path of a text file with addresses of recipients.

```bash
$ ./airdrop message message.txt targets.txt
```

Example of `message.txt`:

```text
Dear token owners, please check out our new site at https://mytokensite.com
```

Example of `targets.txt`:

```text
0x7c98Aee68b8bdaaA598b2524698a8e9bFf5e1607
0x82Ecf0843E4daE55fDc7748c73913A8F10ABc939
0xDee4520dCdf41023634340C32DD96A506805302E
0xE3C9FE2a48fC6967065a0858823F6D308A2E71A4
```

### Send ERC20 tokens to multiple accounts

The command `erc20` takes three arguments: token address, token amount and the path of a text file with the addresses of recipients.

```bash
$ ./airdrop erc20 tokenAddress tokenAmount targets.txt
```

### Send gas to multiple accounts

The command `gas` takes two arguments: amount of gas and the path of a text file with the addresses of recipients.

```bash
$ ./airdrop gas gasAmount targets.txt
```

## Address harvesting

To harvest addresses there is no need in creation of the account and topping up its balance. The operation is read-only so no gas is used.

To harvest EOAs (non-contract addresses) with minimal ethereum balance of 0.5 ETH

```text
$ ./airdrop harvest --minbalance 0.5  
```

To harvest EOAs with minimal ERC20 token balance of 0.5 Aavegotchi GHST Token:

```text
$ ./airdrop harvest --minbalance 0.5 --token 0x385eeac5cb85a38a9a07a70c73e0a3271cfb54a7 --rpc https://cloudflare-eth.com
```


**Note** 

The addresses are extracted from the transactions being executed. The same address can execute several transactions in row and it will be recorded because it fits balance requirement. It's up to you to remove duplicated addresses. In linux command line to remove duplicates from the text file with harvested addresses:

```bash
$ cat targets.txt | sort  | uniq > targets_uniq.txt
```

---
**END**
