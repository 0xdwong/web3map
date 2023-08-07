# 状态通道

## 什么是状态通道？

状态通道是一个以太坊L2扩容方案，其允许参与者安全且免费地进行任意数量的链下交易，并且只需在开启和关闭通道时支付gas费用。因此状态通道可以实现尽可能低的gas费用，支持更大的交易吞吐量。

## 原理

假设一种场景：Bob每天要向他的朋友Alice支付超过10笔价值为0.5美元的ETH，并持续一个月。然而这么做不仅费时间，而且还浪费大量gas费（每次交易都需要支付一定的gas费）。在多数时候，交易所支付的gas费甚至超过了交易金额。

因此他们想到一个办法，可以在一个记账app上分别开设自己的账户，并且Bob必须预先将一些钱存入保险箱，以获得Alice的信任。以后的每一笔交易，他们只需更新自己的账户余额，不需要立即结算。一段时间后，当所有交易都结束时，记账app可以清楚显示Bob欠Alice的金额。这时锁在保险柜里的钱会在他们之间重新分配。其中所有的存储和计算都由智能合约管理。

从技术上讲，要加入一个状态通道，一组参与者需要共同签署一个多签名的智能合约，将他们的资金存入并锁定到其中，形成一个初始的区块链 "状态"。这个锁定的 "状态 "可以是一定数量的ERC-20代币，甚至是NFT、ENS域名等。

然后，同一通道内的参与者可以自由地进行链下交易，而不需要立即将交易返回L1进行结算。每一笔链下交易都需要由所有参与者签名，才能被认定为是有效的 "状态更新"。 

最后，当交易全部完成后，所有参与者应通过签署智能合约向L1提交最终的、所有参与方均认可的状态。智能合约在验证所有链下交易（"状态更新"）均有效后，将最终关闭通道，并为每个参与者结算存款余额。参与者随后便可以取出他们剩余的存款。

## 优点和缺点

优点在于：状态通道善于处理极高的交易吞吐量，同时为用户保持较低的gas费用，适用于长期、重复、小额支付的情形。

缺点在于：只允许同一通道的参与者之间进行交易，不允许通道在过程中增加或删除参与者。因此使用中不太灵活，增加其应用的局限性。

***

参考文章：

https://cn.tokeninsight.com/zh/tokenwiki/all/what-is-state-channel