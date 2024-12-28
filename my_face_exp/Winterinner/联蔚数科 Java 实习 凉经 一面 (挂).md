​`KeyWords`​ 联蔚数科 - Java - 南京 - BXXS - 25届 - 科班 - 日常实习

​`Collection`​ Tragedy Op.X No.X

​`Locate`​ 南京秦淮

​`Platform`​ 波斯直ping

‍`Status`​ failed (12.02)

‍

‍

‍

## 时间线

* 11.26 发起沟通, 秒接简历
* 12.02 视频一面 - 技术面

‍

‍

‍

## 流程

‍

‍

### 一面

20min

‍

1. 经典为什么跑路了
2. 介绍实习日常工作与负责模块
3. 你们这个日志模块是怎么实现的
4. 日志存在数据库里面用什么字段存? 最后还是存在数据库吗?
5. 阿里的东西有用到吗? 中台名字是啥? 一大堆阿里内部体系的名词, 听不懂, 你听过吗?
6. 你对K8s的了解, 不太了解啊, 那说你尽可能的了解.
7. 不是, 哥们你这也没介绍K8s的东西啊? 那我问你, k8s和Docker的关系你咋理解的...拷打
8. Docker了解吗? 那好, 那么你需要在服务器上部署你的服务, 什么操作步骤?
9. 那好, Dockerfile打包成镜像啥命令?
10. 这个镜像变成容器, 啥命令?
11. 沉默8s.
12. 那你知道的Docker命令再说说
13. 数组转为List的方法? 不不不不要问你工具类/工具包的偷懒方法, 就问你Array咋办? 那个API是什么?
14. 好嘛, (一看就是没咋写代码的家伙), List里面可以存NULL吗?
15. 那, Map里面可以存NULL吗? 你咋知道的? 你确定? 真的确定?
16. 好 (遗憾), 多线程这边, 线程池参数. 场景 - 用户一直请求, 一般情况下最后会创建多少线程? 

     嗯哼, 那么最后都满了咋办, 会发生什么? 除了传统的这种抛异常还有啥? 拒绝策略, 全部给我说出来.
17. SpringBoot 在每一层Controller, Ser....有哪些注解被用到.? 好, 你Mapper层还有哪些注解?
18. 人在哪? 咋投南京了?
19. 反问

‍

‍

**个人**

‍

1. 经典
2. ...
3. 只是顺嘴提到了, 实际上只是在这里debug了些东西, 说的不行. 用自定义注解进行抽取这样的一般实现 | 答得很烂
4. 用Blob这样的大字段, 临时用varchar等类型 (不确定); 数据库只是中间态. 最后是要进行写日志文件的. | 很不自信
5. SpringCloud, Arthas, EasyExcel这样的开源的, 闭源的只有这个Trantor中台啥的, 没咋用(没资格用, 臭OD); 根本不知道, 只能说自己MQ能够自动选MQ封装这样子的. (它应该是后台自己封了下) | 很low
6. 几乎为0. 老实说了自己不是运维, 只能说能看封装的东西 (下次真的要去掉这个或者努力去进修一下k8s了).  |投降了

    开始扯系统架构, 说更大的微服务概念和巨石概念等, 但是到最后没答到点上 |答非所问, 小丑
7. k8s是架构, Docker是对象实例. (货架-商品)这样. 然后说着说着还忘记k8s还能够管理的另一种Docker的名字了, 拉跨. ..再问就露馅了.... | 拉跨
8. 了解. 有用云服务器的使用. 忘光光了, 只能胡扯. 1, 本地压测调试OK, 2.写.Dockerfile文件(还是啥名字的文件)在每个服务的资源里面, 这个脚本咋写忘记了, 说的稀烂 3.上传到云服务器 4.云服务器Docker执行dockerfile啥的东东(忘光了真的) 5.对其发起请求测试等. | 根本不对
9. 私密马赛, 确实太久远了, 想不起来了. |投降了
10. 脑子呆了, 想不起来了 (run就行啊)  |投降了
11. 对着黑屏幕吞口水.
12. ps, run, start, rm, pull, 还有些参数, 挂载等  |给个台阶下
13. 用工具类, .of/asList或者toList(忘得有些多, 纯猜), 笨蛋了这时候忘记stream方法咋写了. 答案是

     ```java
              String[] array = {"A", "B", "C"};
             List<String> list = Arrays.asList(array);
             System.out.println(list);
     ```
14. 可以. NULL只是指针引用, 在堆里面没有对应的对象罢了.(胡乱解释, 但是答案是对的) 

     ```java
             List<String> list = new ArrayList<>();
             list.add("A");
             list.add(null);
             list.add("B");
     //sout
     [A, null, B]
     ```
15. 不能, 键值对型的关系, 不行. 根据我的写代码经验可得. Sure. 我很确定(点头)

     我不仅疯了, 还傻了. 明显要K,V分开来说.

     ```java
     a Map in Java can store null values for both keys and values
     public class MapWithNullExample {
         public static void main(String[] args) {
             Map<String, String> map = new HashMap<>();
             map.put(null, "value1");
             map.put("key1", null);
             map.put(null, null);

             System.out.println(map);
         }
     }
     {null=null, key1=null}
     ```

     信誓旦旦的: "以我(3年)开发经验, 下判断了"
16. 很高兴, 线程池八股. 一般就是总线程数满了 (解释流程).

     抛异常. 只说出两个, 真菜狗. (支支吾吾到极点了), 自己都绷不住了.
17. 叽里呱啦还行 (什么还行, AOP注解突然想不起来了). 只想起来一个写SQL的名字想不起来了(一万年没写过SQL, 只写Service的MP/MPJ的下场)

     ```java
     @Mapper
     public interface UserMapper {

         @Select("SELECT * FROM users WHERE id = #{id}")
         User findById(int id);

         @Select("SELECT * FROM users")
         List<User> findAll();

         @Insert("INSERT INTO users(name, email) VALUES(#{name}, #{email})")
         @Options(useGeneratedKeys = true, keyProperty = "id")
         void insert(User user);

         @Update("UPDATE users SET name = #{name}, email = #{email} WHERE id = #{id}")
         void update(User user);

         @Delete("DELETE FROM users WHERE id = #{id}")
         void delete(int id);

         @Results({
             @Result(property = "id", column = "id"),
             @Result(property = "name", column = "name"),
             @Result(property = "email", column = "email")
         })
         @Select("SELECT * FROM users WHERE name = #{name}")
         List<User> findByName(String name);
     }
     ```

     没错, 有这么多, 我除了Mapper之外一个都没想起来, 因为我写代码从来不写Mapper层, 哈哈哈! (双手抱头了)

     "是的, 那里可以写SQL...诶, 写什么来着? 写SQL...? " 这简直是rz一般的回复.....已经宕机了
18. 在家, 之前在南京.
19. 今晚状态很烂, 面得不是够好了, 我想不出其他问题了...合十 (不浪费您时间了, 我自己走吧)

‍

‍

‍

## 结果

(个人)

‍

大报恩寺后面的公司, 嗯去过他们前面那条街.

被剃光头了啊, 啊, 这是什么啊?!

虽然最近一次复习已经是15天前了, 可以说是裸考, 但是这么基础的问题答不上来, 啊, 就

无话可说, 今晚睡不着了.

‍

---

END. 2024-12-03

光头玄桃K

‍
