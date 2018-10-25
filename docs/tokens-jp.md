
# トークン実装のベストプラクティス

トークンの実装は他のベストプラクティスにもちろん準ずるべきですが、トークンならではの注意事項もあります。

## 最新の標準に準ずる

一般的に、トークンのスマートコントラクトは採択されて安定した標準に追従すべきと言われています。

現在採択された標準の例は以下の通りです。

* [EIP20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md)
* [EIP721](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) (non-fungible token)

## 今現在存在しているEIP-20の弱点

EIP-20トークンの`approve()`関数は許可を受けた消費者(spender)が意図する量以上のトークンを引き出せる可能性があります。
[front running attack](./known_attacks/#transaction-ordering-dependence-tod-front-running)を利用されると、消費者(spender)は`approve()`が呼ばれる前と後の両方で`transferFrom()`を呼ぶことが可能になります。
詳細は[EIP](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md#approve)と、[this document](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit)でご覧になれます。


## Prevent transferring tokens to the 0x0 address

At the time of writing, the "zero" address ([0x0000000000000000000000000000000000000000](https://etherscan.io/address/0x0000000000000000000000000000000000000000)) holds tokens with a value of more than 80$ million.


## Prevent transferring tokens to the contract address

Consider also preventing the transfer of tokens to the same address of the smart contract. 

An example of the potential for loss by leaving this open is the [EOS token smart contract](https://etherscan.io/address/0x86fa049857e0209aa7d9e616f7eb3b3b78ecfdb0) where more than 90,000 tokens are stuck at the contract address. 

### Example

An example of implementing both the above recommendations would be to create the following modifier; validating that the "to" address is neither 0x0 nor the smart contract's own address:

```sol
    modifier validDestination( address to ) {
        require(to != address(0x0));
        require(to != address(this) );
        _;
    }
```

The modifier should then be applied to the "transfer" and "transferFrom" methods:

```sol 
    function transfer(address _to, uint _value)
        validDestination(_to)
        returns (bool) 
    {
        (... your logic ...)
    }

    function transferFrom(address _from, address _to, uint _value)
        validDestination(_to)
        returns (bool) 
    {
        (... your logic ...)
    }
```
