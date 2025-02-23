EIP712: 根据合约的作用域domain和需要参与签名的数据以及类型进行链下签名，然后将获取签名结果以及需要参与签名的数据传到线上合约进行签名验证，验证是否是由该address的签名，这样可以节省交易手续费，将授权交易合并到一笔交易当中。 (链下签名可以将交易 gas 成本从用户转移到服务提供商)

域分隔符(domain separator)：主要是防止一个Dapp的签名还能在另外一个Dapp中工作，从而导致签名冲突。

![image](https://user-images.githubusercontent.com/100255425/183845489-08030959-ba39-4c14-ae6b-b95e65daab26.png)
EIP712在可用性和安全性方面有很大的改进。与上面的例子相反，当启用EIP712的DApp请求签名时，用户的钱包会显示哈希之前的原始数据，这样用户更容易验证它。
开发人员应该充分利用 EIP712。它显著提高了可用性，并有助于防止网络钓鱼




# ERC20 Permit

This project is an implementation of an ERC2612 enabled ERC20 token.

It allows to use signatures calculated off-chain to increase allowances using `permit`. The call to `permit` doesn't need to be done by the `holder`, so this contract allows the implementation of "gas-less" tokens, or the replacement of `approve` transactions by methods that call `permit` and `transferFrom` atomically.

Most of the code in this repository was written by Georgios Konstantopoulos.

## How to Use

`ERC20Permit` is an `ERC20` contract. You can just inherit it and you are done from the smart contracts point of view.

```
contract MyContract is ERC20Permit {

    constructor (string memory _name, string memory _symbol) public ERC20Permit(_name, _symbol) {...}

    ...
}
```

The `utils/signatures.ts` file contains useful functions to compute the `DOMAIN_SEPARATOR`, `digest` and `signature` from typescript.

## Further reading

[This article](https://hackernoon.com/how-to-code-gas-less-tokens-on-ethereum-43u3ew4) explains in detail how to use the code in this repository.
