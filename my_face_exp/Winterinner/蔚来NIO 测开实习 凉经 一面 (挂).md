​`KeyWords`​ 蔚来 - NIO - 测试开发 - 合肥 - Java - BXXS - 25届 - 科班 - 日常实习 - 凉凉

​`Collection`​ Tragedy Op.X No.X

​`Locate`​ 合肥

​`Platform`​ 波斯直ping

‍`Status`​ Failed (11.18)

‍

‍

## 时间线

* 11.08 发起沟通, 秒接简历
* 11.12 视频一面 - 技术面(测试)
* 11.18 感谢信.

‍

‍

## 流程

‍

‍

### 一面(测试面)

70min (55min面试, 余下手撕)

‍

1. 主要的东西都是开发, 你对测试是啥看法
2. 讲讲实习项目功能这样的
3. 测试用例设计方法
4. 提交一个bug(单), 需要包含哪些内容
5. bug有争议, 有些人觉得是bug(或者, 开发说是特性), 这种咋办
6. 针对抢红包场景设计测试用例
7. 接口测试经验? Postman是吧, 好, 你编写Postman的要点在哪里, 比如对一个登陆接口进行编写?
8. 接口自动化有经验吗, 我没在简历里面看到?
9. 那代码框架处理自动化经验呢?
10. 还了解其他什么测试框架?
11. 简历里面的Postman流水线到底是啥啊我很感兴趣, 是用接口串联起来一次执行多个吗? (项目)
12. Postman断言一定是有用到的, 说一下?
13. Pytest框架实现原理?
14. Jmeter当时压测的场景? QPS目标是谁给的? (项目)
15. 这个错误率是咋算的?  (项目)
16. (致命一击) 这些请求访问接口都是用一个token吗?
17. 每次请求的请求数据都是一样的吗?
18. 好, 那么如果你需要批量生成虚拟用户去请求访问后端接口, 你要咋办?
19. Jmeter咋做参数化请求?
20. 压测服务端要关注哪些指标?
21. 接口压测返回结果的判断, 对还是错?
22. JAVA + Python 的深拷贝浅拷贝
23. JAVA反射机制, 举一个例子
24. 写SQL, 查手机号136开头数据
25. 手撕超简单题: 字符串转拼音
26. 反问

‍

‍

‍

**个人**

‍

1. 开头就问这个问题, 看来是不好办了. 仍然是自己提前准备好的从测试对人与人对测试的双向选择进行说明, 并说自己在开发的经历能够更好的帮助进行测试内容, 同时要说明确实是有测试的经历, 但是没写出来 (其实是太少了没法写...话说为什么不专门改点东西投测开呢? 因为觉得没啥必要, 毕竟没有去纯测的话应该匹配度还行, 除非对面测试含量太高了) -> 很不幸, 这次看来就是对面测试含量太高了
2. 叽里呱啦, 她的评价不好. 说面试的岗位是"测试", 没有太多相关的. 我就觉得很怪, 不是测开吗? 然后就说:"我们来讲些基础问题吧"
3. 八股, 分几个方面就好; 例如从测试的类型去分......然后我尽量往自己的项目去靠吧, 和面开发那个思路一样
4. 八股, 我实习时候是做过这个东西的, 因此手到擒来, 直接在脑海里回忆一下那个内部QA界面即可, 应该是很全了
5. 八股, 实习时候也遇到这个情况, 但是我是开发, 说这不是bug, 对面是测试(当时真小丑了, 是我的错). 就尽量复现了一下场景和双方的解决方案吧, 最后都要到开会谈这样.
6. 八股, 我还想了些其他场景, 还想了黑客攻击场景(例如绕过前端), 还有高并发的解释, 抢红包的幂等, 多端兼容性等等, 也算是推陈出新了吧; 她说还不够, 那好, 我继续说(虽然感觉还不算太全? 八股没咋背这个)
7. 确实用Postman多, 编写要点? 我平常只是写一个脚本自动获取token保存这样, 其他都是基础的发请求看结果, 哪里知道什么要点? 只能按照基础的来了.

    先讲环境起手, 把Postman的Environment内容进行自动化的注入, 而后在发起请求时候自动携带这个auth请求头 (真是我自己按照官网一点点配出来的, 我没开玩笑, 但是这在测试眼里真算是很简单的内容了吧(关公门前舞大刀属于是)), 剩下的请求头我在后端微服务里面动态处理, 但是考虑到和测试关系不大没说. 说的有些多了, 测试的环境都是开发组提供的, 不需要考虑这么多吧, 从我观察的我们组的测试的生存状态来说, 关键是设计用例测试的流程吧. 

    于是这里把开发的洋洋得意展现的一览无余了? 难怪 (为什么这么说, 请往下看)

    之后就是将最基础的发送一个JSON作为请求体的请求的操作步骤作了说明 (oh, 我大概只会这个了), 后端文档请求类型这谁都会, 感觉我就好像在教人怎么写一个Hello World, 一边讲的眉飞色舞, 复盘的时候我都在祈祷: 憋说了, 憋说了.

    东拉西扯啊, 最后才飙出一大堆的什么 "异常值, 攻击值", 自己的认知里面算是很全了
8. 我不懂自动化测试! 我真不懂, 我只能说我在后端有去拟合Postman Token校验的内容 (笑死了, 别人一翻源码就知道了, 我只是写了行if(token.startWith("Postman") token.substring(8, token.length()) 这样的玩意来面向工具编程罢了, 现在想来提这个简直是纯纯小丑 (废话, 没这行是后端开发的问题, 哪里需要测试管这个)
9. 完全没有啊......只能算得上有了解, 只能用自己的Junit5 + Mock进行单测的编写这样子 (草了, 这不是直接把自己的底裤都扒给人家看了吗? 就是个只会写单测的投机后端, 干不下去了来找测试的背叛鼠鼠), 还有, 在这里说Junit5和6 怕不是会被拷打, 比如问一下Junit版本改了什么就被打死了...
10. 看自己, 还是看了些测试框架吧, 但是仅有皮毛, 不敢说多了.
11. 太小丑了, 竟然是个小瘪三! 我这时候已经不敢看她的脸了...
12. 不会, 直接说没有这个情景 (这踩红线了吧, 断言没有这个情景?)
13. 不晓得, Python半年多没咋用了, Pytest连界面都不知道长啥样
14. 结合项目高并发场景: 产品页面, QPS是根据情况进行动态设置的, 看最后哪个效果好就选哪个写简历里面(真大实话, 就是这样办的, 毕竟实际上这个全栈项目都是鼠鼠从零到一自己做的, 其他人只是挂名和提供建议这样), 然后还说这个具体什么数值是自己项目组订的 -- 项目组多少人? 我本来说两个, 又随便抓一个人说三个 (三人行, 必有我师!) ; 

     笑啦了, 当时自己说的什么鬼话, 我是全栈开发, 一个是产品经理兼测试, 一个是前端开发 (好家伙, 那我自己不就说自己不是测试了吗? 看来是已经石乐志了)

     然后最尬住的一点是, 我当时测试时候, 实际上是放开了不同用户的过滤器的, 也就是说, 测试时候每个请求都是用一个虚拟用户进行. 当时图一个省事, 现在看来确实不好说啊: 多用户情况下, 我咋么动态生成不同的用户? 咋么对其进行鉴权? 我只能想个接口"因为用户鉴权解码会有性能损耗与网络延迟, 体现真实性能下还是采用了无状态的情况" --> 真实情况难倒不是虚拟用户吗? 我真的...无语了

     接下来就是简单的Jmeter的使用方法, 自己真正有用过所以能把流程串好, 但是确实太基础了.
15. 错误率就是做接口保护的那个Guava限流东西, 自己定一个参数...当时有些草台了
16. 绝对要回答不是! 如果说是, 或者把我的情况原封不动说出来:

     > 其实没有token, 哈哈! 我把过滤器删了, 哈哈! 
     >

     那就死球了, 绝对是要先顾左右而言他 (指满嘴跑火车10s), 然后想想对策....

     啊? 什么, 我听到了什么, 我真全都说出来了?
17. QPS, query嘛, 就是选商品和商品分类两个页面去拉数据测量的...我当时是这么想, 现在回去看看4月份的文档才发现说错了, 我还有一个测的是下单的高并发接口, 这个不是简单的查询啊! 要查几次数据库! 我真的红温了看来
18. 先说自己有实现过, 然后, 就想不起来了. 实际上端地是没做过.
19. 不会, 只是了解说读取本地csv文件这种可以, 读外部配置这样
20. 八股. 终于透透气了, 分Jmeter的结果树和结果报告 + 实例情况进行说, 同时再扯一下实习时候在阿里基础架构设计那边的观察结果, 还要掰扯细到Jmeter每个结果的标签...
21. Jmeter响应会有结果的, 自己也重写了对应消息, 能看到. 但是最好的回答还是说用 Assert 进行判断
22. 八股, Python我知道API是clone 和 deepclone所以也说了.
23. 八股. 说自己的项目反射的实现, 手动封装了联表分页的工具类 (现在看来这简直就是小玩具, 就是手动做了个业务抽取, 感觉技术力还不如AOP实现日志管理...唉.)
24. 简单: select * from table where number like("136%")
25. 手撕一个侮辱题, 太简单了, 但是自己已经知道面试结果了, 甚至没写好输入导致一直空白输出难绷 (sc.nextLine() 只写了sc.next(), 那个飞书编程太小了看不见)
26. 面试流程不固定(我就知道); 团队做的是JAVA接口优化测试, 其他时候都是功能测试, 少量性能测试;

     "对我有怎样的评价" -- 笑啦了, 问这个问题不是找打吗

     "还好吧, 挺自信的". 当时面的眼冒金星了, 听成"你还挺自信的了", 吓得大气都不敢出, 在座椅上缩成了一团

‍

‍

‍

‍

## 结果

(个人)

‍

真是不好意思, 给您添麻烦了. 听我这哔哔歪歪了一个小时, 看我这条被丢到岸上的泥鳅, 作滑稽可笑的挣扎.

后来反复琢磨着最后一句话, 把自己的QQ名改成了 "普信男". (没有恶意, 只是自嘲)

是啊, 是我太自信了吗? 不, 是我太逊了.

收感谢信时候其实我早明白我已经被推下了桌, 同时到来的是最后一个被自己拒掉的OC(过两天发那个)

‍

第二天普信男就病了, 那天没学满8h.

但是, 现在大抵是要好过来了, 因为刚才左边脑袋撞到了门框, 像个白面口袋似的横在了地上, 把可笑的一切都忘掉了

‍

‍

> 于是, SpadeK算是把最后的能够进大厂实习的机会也丢掉了, 他的秋招也到此结束

---

‍

END. 2024-11-24

普信男玄桃K, 大脑升级中

‍
