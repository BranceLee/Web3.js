# Web3.js
Blockchain javascript
最近开始试着学习Web3.js ，本文主要来自[https://web3js.readthedocs],有翻译不好的地方多多指教。
### Promises Events

   PromiEvents 的运行方式就像一个具有on, once , off 的promise 函数 
```js
web3.eth.sendTransaction(from:’0x123’ , data: ‘0x432..})
    .once(‘transactionHash’, function(hash){…})
    .once(‘receipt’, function(receipt){…})
    .on(‘confirmation’, function(error){…}
    .then(function(receipt){
        //will be fired once the receipt is mined
    }
)
```
    
### Json interface

   json 接口用来描述一个智能合约的二进制文件，通过使用这个json 接口，通过web3.js 能够创建一个js对象（ web.3.eth.Contract object ）来代表这个智能合约，以及调用该合约的方法和事件
```js
    var Web3=require('web3')
    //实例web3 对象
    var web3=New Web3();
    
    // 连接以太坊节点
    web3.setProvider( New Web3.provider.HttpProvider('http://localhost:8545'))
    
    //合约ABI
    var abi=[...];
    
    var address='0xb3...'
    
    var metacoin =web3.rth.contract(abi).at(address);
    
```

 下面我们来看一个Abi 的demo
 ```js
var abi = [
	{
		constant: false,
		inputs: [ { name: 'receiver', type: 'address' }, { name: 'amount', type: 'uint256' } ],
		name: 'sendCoin',
		outputs: [ { name: 'sufficient', type: 'bool' } ],
		payable: false,
		type: 'function'
	},
	{
		constant: false,
		inputs: [ { name: 'addr', type: 'address' } ],
		name: 'getBalance',
		outputs: [ { name: '', type: 'uint256' } ],
		payable: false,
		type: 'function'
	},
	{ inputs: [], payable: false, type: 'constructor' },
	{
		anonymous: false,
		inputs: [
			{ indexed: true, name: '_from', type: 'address' },
			{ indexed: true, name: '_to', type: 'address' },
			{ indexed: false, name: '_value', type: 'uint256' }
		],
		name: 'Transfer',
		type: 'event'
	}
];
```
 官方文档将其分为两种：
 1.Function 函数
 2.Event    事件
 
 咱们先说说事件吧,
 Events:

*  type:通常代指事件类型；
*  name:即事件本身的名字；
*  inputs:它是一个数组对象，且每一个对象都办函一下个参数:
    *  name:参数名
    *  type:参数，数据类型
    *  indexed：true if the field is part of the log’s topics, false if it one of the log’s data segment.（不太知道怎么翻译）
*   anonynous:该事件是否被匿名声明  

接下来咱们来看看Functions:

 *  type:'function','constructor'；
 *  name:函数的名字，只代表函数类型的；
 *  constant:该函数是否会修改区块链的状态；
 *  payable:函数是否能够接收，默认false;
 *  stateMutability: a string with one of the following values: pure (specified to not read blockchain state), view (same as constant above), nonpayable and payable (same as payable above);
*   inputs: an array of objects, each of which contains:
name: the name of the parameter;
*   type: the canonical type of the parameter.
*   outputs: an array of objects same as inputs, can be omitted if no outputs exist.


### Web3
  class 类
  关于Ethereum 主要有一下几个class:
  ```js
var Web3=require('web3')

> Web3.utils
> Web3.version
> Web3.givenProvider
> Web3.providers
> Web3.modules

```

#### Web3.modules
  Web3 类 的属性值：
 Web3.modules 它会返回一个具有所有子模块的对象，这样你就能够手动的实例化想要的东西
 ##### Return
 Object : 所包含的子模块如下：

*     Eth - Function:The Eth modules能够与以太坊网络数据交互.
*     Net - Function:这个Net 模块是为了与网络属性进行交互处理；
*     Personal -Function:The Personal 模块是为交互，以太坊的账号设立的。
*     Shh -Function : 为了（whisper protocol） 我理解为加密处理。
*     Bzz -Function : 为交互 swarm network 。

```js
Web3.modules
> {
    Eth: Eth function(provider),
    Net: Net function(provider),
    Personal: Personal function(provider),
    Shh: Shh function(provider),
    Bzz: Bzz function(provider),
}
```

