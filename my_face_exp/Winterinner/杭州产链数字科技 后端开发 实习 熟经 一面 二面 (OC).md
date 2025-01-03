​`KeyWords`​ 杭州产链 - 后端 - 杭州 - Java - BXXS - 25届 - 科班 - 日常实习 - OC

​`Collection`​ Tragedy Op.X No.X

​`Locate`​ 杭州西湖

​`Platform`​ 波斯直ping

‍`Status`​ OC - refuse (11.25)

‍

## 时间线

* 11.18 发起沟通, 秒接简历
* 11.19 视频一面 - 技术面
* 11.20 视频二面 - 技术面
* 11.21 OC, 闪电突袭

‍

## 流程

‍

‍

### 一面

20min

‍

1. 常见垃圾回收器
2. MP分页咋实现的
3. 物理/逻辑分页区别
4. 索引覆盖
5. 索引下推
6. ES介绍下用了啥
7. ES的 match 和 term 查询的区别
8. MQ消息可靠性 + 死信队列
9. Linux日志查找
10. 导入功能咋做的(实习)
11. arthas哪些命令?
12. 导入是单线程多线程? 同步怎么办(业务)? 事务处理?
13. JWT 组成
14. 超时删除实现(项目)
15. 反问

‍

‍

**个人**

起手我一看, 对面头像是猪猪侠, 直接开口: "你好, G-G-Bong!" 给他笑啦了.

发现他声音老像我初中同学了, 顿感亲切

1. 是八股, 但是我选择了 G1 -> ZGC -> Parallel -> Serial的路线来讲, 同时给出具体常用版本(JDK17, JDK9, JDK8这样), 以及切换的方法(JVM参数), 还要提一句他们是混合的还是新生代老年代的, 基本撸了个遍. 直接拿下首功
2. 这我有些不理解, 询问了一下是问底层还是操作. 只要问操作的话, 就回答最后还是调用物理分页, limit 起始索引, Num 这样
3. 芝士什么? 我没看过这东西, 直接说没get到. 投降了, 原来就是手动封装分页和直接SQL去取的区别, 哎呀. (下回不会错了) T_T, 对方平和的告诉了我答案, 我恍然大悟
4. 先要讲一下底层实现B+, 以及一般的查询流程. 之后讲覆盖流程, 再举一个例子, 查abc三个字段, 有id树+三个辅助索引就能全部找出来了. 最后插一句深分页用这个来提升性能
5. SQL优化器的内容, 快速缩小范围这样
6. 讲项目
7. 我忘记了...match全文搜索, term精确匹配
8. 分三部分说..八股, 再提一句死信这样的
9. / + grep | 等等
10. 讲业务场景, 然后讲亮点
11. 胡言乱语(只是MT叫我这么做的)
12. 多线程, 拆分区块规避线程问题, 一个线程处理一个块的区域. 同时只是写日志, 不会抛出异常. 沟通了5min, 面试官说懂了get到了
13. 先问下是什么token, 哦原来是JWT, 在0.05秒内想到了三个组成部分, 在0.5s内开口, 在2s内念完: 头/负载/盐. (这个盐就是签名的实际意义吧, 我是这么理解的)
14. Redis set key with expire, setex 同时指定过期时间. 再提提缓存管理的思路, 提LRU的清理方案, 最后能够留下主要的键值.
15. 哪个部门缺人去哪里, 教培2G, 国家网络2G, 储能2G, 卖地等等业务线. 说今天反馈, 看部门领导有空就来(意思是通过了)

‍

‍

### 二面

‍

1. 说说实习和项目, general
2. RBAC了解吗
3. 你这个密码存储方式(项目), 可不可逆
4. 慢SQL优化
5. 索引失效场景
6. 设计模式讲讲
7. 单例并发问题有吗?
8. 服务器运维咋搞的
9. 反问

‍

‍

**个人**

1. 叽里呱啦
2. 若依去年10月我扒过源码, 今年10月有进行过移植, 算是在我的好球区.从前到后的SpringSecurity的实现, 落库都说了 用户 - 角色 - 权限
3. 加密存储 (md5), 我还忘记加密是什么协议了, 该打. 不可逆, 但是从数据库拿回到前端能够比对...
4. 八股 + 具体场景
5. 八股 + 具体场景
6. 用到的, 具体项目 + 功能 + 怎么做的
7. 有的, 懒汉里面的, 从初级的一层检测到双重检测再到终极版volatile双重检测都捋了一遍
8. 我先说实习时候公司有中台看界面占用这样的, 然后狠狠炫技端点的阿里k8s + Docker => 大粒度微服务的运维实现, 体现自己的参与度; 再说具体运维措施, arthas一站式解决问题(基本逻辑谈一下, 附加进程检测, 使用jvm命令查看实例状况这样的). 然后说我平常自己怎么去检测Ubantu系统问题(八股), 以及我调教Linux 的经验, 报菜名: Azure, 阿里云, 腾讯云, 华为云, 天翼云......
9. 对我的评价: 挺好的. (双方沉没了5s, 很尴尬). 对方诚恳的比较了我们的技术栈, 说很匹配.

‍

‍

‍

## 结果

(个人)

‍

感谢HR在OC时候的细心沟通, 但是我出于个人打算还是决定放弃这个机会. 我确定不再去一个"端点二号".

面试体验很好, 自己收获颇丰, 祝工作顺利.

杭州西湖200是最不能接受的一点, 毕竟是希望长期实习, cover不太住, 未来还要一边实习一边春招, 大概常驻到明年7月吧. 杭州算是蛮贵的了(虽然普遍都是4k薪资, 有评优这种奖励算是挺实惠的了)

‍

个人还是有些紧张卡壳, 还是需要磨练, 八股很熟, 但是表达能力还是很差.

‍

---

END. 2024-11-21

玄桃K

‍

note, 这是端点文章后的第一篇文章, 优化了写作风格. 最近秋招彻底失败了, 会把这几天拒掉的OC和挂掉的都记录一下. 哦, 那些开不开视频以及自我介绍的就不记录了, 小事

‍
