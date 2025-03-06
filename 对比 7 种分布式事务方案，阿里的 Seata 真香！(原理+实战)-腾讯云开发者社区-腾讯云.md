# 对比 7 种分布式事务方案，阿里的 Seata 真香！(原理+实战)-腾讯云开发者社区-腾讯云
[对比 7 种分布式事务方案，阿里的 Seata 真香！(原理+实战)-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1975104) 

 [社区首页](https://cloud.tencent.com/developer) >[专栏](https://cloud.tencent.com/developer/column) >对比 7 种分布式事务方案，阿里的 Seata 真香！(原理+实战)

![](https://ask.qcloudimg.com/avatar/1263954/r1y1ckb9xa.png)

发布于 2022-04-08 12:29:47

发布于 2022-04-08 12:29:47

这篇文章主要介绍一些目前主流的几种分布式解决方案以及阿里开源的一站式分布式解决方案Seata。

**文章有点长，耐心看完，看完你还不懂分布式事务，欢迎来捶我......**

文章目录如下：

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e376136293cfeb86839c93c9c079ca09.png)

### **什么是分布式事务？**

分布式对应的是单体架构，互联网早起单体架构是非常流行的，好像是一个家族企业，大家在一个家里劳作，单体架构如下图：

![](https://ask.qcloudimg.com/http-save/yehe-1263954/ea1ece2ac77e1d5e938a8727255d2457.png)

但是随着业务的复杂度提高，大家族人手不够，此时不得不招人，这样逐渐演变出了分布式服务，互相协作，每个服务负责不同的业务，架构如下图：

![](https://ask.qcloudimg.com/http-save/yehe-1263954/76967186074612eb93bf0fff7d479a49.png)

分布式架构

因此需要服务与服务之间的远程协作才能完成事务，这种分布式系统环境下由不同的服务之间通过网络远程协作完成事务称之为分布式事务，例如用户注册送积分 事务、创建订单减库存事务，银行转账事务等都是分布式事务。

典型的场景就是[微服务架构](https://cloud.tencent.com/product/tse?from_column=20065&from=20065) 微服务之间通过远程调用完成事务操作。比如：**订单微服务**和**库存微服务**，下单的同时订单微服务请求库存微服务减库存。简言之：**跨JVM进程产生分布式事务**。

![](https://ask.qcloudimg.com/http-save/yehe-1263954/5c06ec69918b4b1c5b24935bd5ce4f71.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/906a3c550a20e90638bd5af794197282.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/c89ec442f02d4671eec7b6ebd79dde53.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/9d82242c1f4137c4333f62c8ad947236.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/58effe1e90bbe0e9ff0a9ad4db91b6f0.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/f1ddb46c3b422780d79f027db0f0cf5f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e33a0a6f76a759ddc6acfd7303be0534.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/286f62d0bd8399cdf523e6ca666ae1aa.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e3578a9b9c7549e70ab1aaf8c59842a7.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e53225742d233d5d8873b1592137066b.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/43744f0a0668652c14efc9304024982a.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/526afe3b19ea046733df6f8db77f450f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/26e53c1f9257e63237f5f670068f24fe.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/9d02f0e25bb4239baecdfe11cc9dd685.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/06f79c002f521e4defcb3727ecdda3c7.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/bdb7dad6d6c6f26ce07d4b508827fa70.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/c20556b1b4f19bbe8f25ae22e51225ae.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/0c85e16c711cd6dc235524f3d9fcab9c.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/f891db29148360e0077a4e061e9c619f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/006992520c0e1c5e223cf563c137ef39.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/564e03191f72abfdcf5e022cbea1a387.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/a30f70601c6ad74b505ec0e4e938a344.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/15f3fbfb4fae34b59da0a4a8177d8c15.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/65639f5719aa5b959a2cf2d74e1c2a6b.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/395d8945be9e1b74c11a91a90335356d.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b6b721f4b66d9f21177250a84aca225b.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/115dc4881c2f38ff4dd3cd7c5d3efad8.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/21e813a40fdaa85eaba4cf07bff849a2.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/373dadfe28ebbb223d68df0a9d84e774.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/6a7ef21a27ac068f76b672d9a086335e.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/2614cdaa982622aefb0885fcbf22cae5.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e83e121a57744c003b5abe8caaf09ff4.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/f6320270b05ac95508625d868883fdaf.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/3d3c432e316b9a5945d13de9a005c02b.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/0ade4d6512b5c99de69dbe1d6bdcf06f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/595366b4ffb1318231a29bd35a3a01b5.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/9d64733d40f9b0082a0014ba509b4a3f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/500f1ae7231f25fcc1c31fc7026b0810.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b403990c6e4cc49e5efcbe946a32011f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e6bcbf0c31b10a37e7771043fcf53fb4.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/660ef21f233ab9af1b52ea71191fd03f.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/672af2754069ef4801dd682fce2f63dd.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b74daf5c4b82d57d32bd711e7f24baf1.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/38417a1a0eed1f7d5004c3e73a6d45ff.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/c02f73b7e927108a2c6e80de582ff8a9.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/f9b22d01909de37af9097fb2be90b682.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e041a3631e2d95be7084dde6994e8e88.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/3d7c5cf4ddc1e42fd5b76309d286d3d8.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/8fcff0a21a7d85f230ba0f032c3da393.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/712f8f055069f70df95baccb2f5a0da5.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/cbb13b9578d64bd0c0059bccca393153.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b0791ae9a4f734b00bb1f9eba6c87a27.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/04421fabc76bb0c95014fe7f5a7fff9d.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/712bc3f342f4978d6dd1fc021523ba2d.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b1fab7d411a8e5115a3b8ec1b43c3f54.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b45ab575bade902ddf7ee99a59e56c39.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/fdbd8a2dc40f3f5061f2704a2d8b36f3.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/6a73aab21358a31be96bbad3cbed0715.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e1460eb7440bc6fb19615a933d687397.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/b702543a6c79a90f88dfc71e7760022e.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/6a3640836eb6456128a84e2c5f7c1048.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/88ad85147eb20c2572993957d202642d.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/a09ce10111482e87433507b034dd4844.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/52ee9a6b09f9ba75a872fb31fe5dc787.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/3e84c2d646d85924284ddacf1f6389c0.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/acca767088207ebbe0978433cdeca276.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/17d98bb07bb3660c895f6188eb624f90.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e67a028606c1bc6cbe3b6b5728d18f52.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/a698f52a988eb93214378ed76ca37d5d.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/e5cf3b05baa3ed2bc8023c64341aaaa2.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/4f41cf4da7e93601524662150d0cf154.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/1ab68523d672ac6c5b442cf63d0594e1.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/824759770ea6099b19b101d56ac26d4e.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/5a1262ae5a7d11d16db6b2046b7dd719.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/8c95d1261e58e6ee003c75680f9a52f8.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/f8208fbac5c823d745d028af616c02f3.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/2a4ef405ae0b9cff718afa195d55d8a9.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/3363e6857b7925e3dcfcb0771d3802de.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/8dcd22dc36cfc7603b475a8b29b64e6e.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/1da57963838afdb7a59ea553f4fd4c40.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/9db87667c011ec3695e8c4eb257a46fb.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/45f4f77ca6aaf2938f2278f42da06b5c.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/a925cbba190c500f440d1facfc05ea64.png)

![](https://ask.qcloudimg.com/http-save/yehe-1263954/d8bc6522be919ac33af40c4ef1cf6715.png)

本文参与 [腾讯云自媒体同步曝光计划](https://cloud.tencent.com/developer/support-plan)，分享自微信公众号。

原始发表：2022-04-05，如有侵权请联系 [cloudcommunity@tencent.com](mailto:cloudcommunity@tencent.com) 删除

![](https://cloudcache.tencent-cloud.com/qcloud/ui/static/static_source_business/789ec94e-0358-4d12-a5ca-0c7ec3478c14.png)

微服务引擎 TSE

微服务引擎（Tencent Cloud Service Engine）提供开箱即用的云上全场景微服务解决方案。支持开源增强的云原生注册配置中心（Zookeeper、Nacos 和 Apollo），北极星网格（腾讯自研并开源的 PolarisMesh）、云原生 API 网关（Kong）以及微服务应用托管的弹性微服务平台。微服务引擎完全兼容开源版本的使用方式，在功能、可用性和可运维性等多个方面进行增强。