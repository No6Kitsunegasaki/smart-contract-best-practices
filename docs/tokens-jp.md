
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


## 0x0アドレスへのトークン転送をしないようにすること

これを書いている時点で、"ゼロ"アドレス([0x0000000000000000000000000000000000000000](https://etherscan.io/address/0x0000000000000000000000000000000000000000))は、8000万ドル以上のトークンを保有しています。


## コントラクトアドレスへのトークン転送をしないようにすること

同様に、コントラクトアドレスへのトークン転送にも注意してください。

注意しなかった場合のトークン喪失の可能性の例として、9万トークン以上がコントラクトアドレスに死蔵されているのを[EOS token smart contract](https://etherscan.io/address/0x86fa049857e0209aa7d9e616f7eb3b3b78ecfdb0)で確認できます。


### 例

このようなmodifierを作った方がいいというお勧めの実装例です。"to"アドレスが0x0もスマートコントラクト自身のアドレスでもないことをチェックしています。

```sol
    modifier validDestination( address to ) {
        require(to != address(0x0));
        require(to != address(this) );
        _;
    }
```

このModifierを"transfer"と"transferFrom"メソッドに適用すべきです。

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
