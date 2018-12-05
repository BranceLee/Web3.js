# Web3.js
Blockchain javascript
最近开始试着学习Web3.js 
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
*  inputs:它是一个数组对象，且每一个对象都包含以下几个参数:
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

#### web3 object
   实例化Web3 类，生成对象
```js
var Web3=require('web3') 

var web3 =New Web3( Web3.givenProvider || 'ws://some.local-or-remote.node:8546' )

>web3.eth
>web3.shh
>web3.bzz
>web3.utils
>web3.version
```
<u></u>
### Ethereum for web developers 以太坊对于前端开发的一些相关信息

  如图所示：
  ![48a6ae5235ace9fe0d905105ec7ea7fc.png](https://cdn-images-1.medium.com/max/1760/1*hPV1rCWFXYjeDI6Yd_G-iA.png)
  
 通常网站应用会寄托在一个 hosting provider（托管供应商）例如Awson,or vps 等，所有的这些客户端user都交互这一个中心化的服务，The client can be a browser, 或者一个api，这些请求都会消耗占用你的服务。如图所示，一个user 向服务发起请求，服务does it's magic ，然后告诉数据库或者cache(高速缓存)，提取（读，写，更新） 数据库然后在返回给user 端。
 中心化的网络大多情况work 的都还是很不错的，中心化really helpful if that database was publicy and securely accessible by everyone,并且如果你也不用weapp 的owner 拿你的流量数据怎么分析的化，都还是可以的。
 但是举个栗子，你辛辛苦苦运营的一个公众号，有几十万的粉丝，结果微信说你违规操作，要封你号，或者goverment 一声令下凉凉，所以中心化的一个节点不够稳定，他依赖了企业背书，不是太稳。
 This is how an Ethereum Dapp 的一个框图：
 ![261e32f99902b8c969f8e3a35487866a.png](https://cdn-images-1.medium.com/max/1760/1*y7Cdz1uGBGLxZ3ekIE13RA.png)
 
  有没有发现，每一个client 浏览器对应的通信都有他自己的 instance of the application (instance1 ,instance2).这儿没有中心化的服务器来连接所有的user ，取而代之的是一份整条的blockchain running on their devices.换句话说在你使用该应用时，你不得不下载整条链，然后使用该应用。This might sound ridiculous ，确实挺荒谬的，但是它具有不依靠中心化的服务呀😂。
  In reality, you don’t need to spend lot of your hard disk and RAM downloading the entire blockchain. There are a few workarounds/optimizations to keep the application decentralized yet make the interaction quick and easy.
  待续Loading...
  
