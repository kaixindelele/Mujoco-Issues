# Mujoco-Issues
欢迎大家在issues中挂自己mujoco开发过程中遇到的问题，也欢迎大家去帮忙解决其他人的问题，互相学习互相进步。

## 一、前言：
本文档作为一次**中文**mujoco建模社区的一次尝试，由于mujoco官方一直没有提供很好的例程示教，对于新手来说，很多功能开发在文档中都看不明白。全网相关的信息也不够多，很难直接定位到我们个人需要的功能，而直接在官方论坛的提问门槛太高，且不够及时。

因此我特意建了一个mujoco建模群(818977608)，方便大家的讨论和交流，但是群交流的信息是零散的，有些问题是共性的，大家都会提问，这时候就需要有一个可以“长期性”的介质来保存这些信息，以便所有人的参考。
利用GitHub的issues功能，可以将群友们在利用mujoco开发过程中的问题直接贴出来，其他会的群友则可以在闲暇时间，将解决方案填上，互相学习，互相促进。
大多数人都是做强化的，相信“分布式多智能体”的力量，手动滑稽。

讨论的内容主要和强化学习物理环境建模相关，包括不限于mujoco、mujoco-py、robosuite、dm-control。
甚至可以讨论一些pybullet和ros相关的信息，但最好不要讨论强化相关的问题。

我会定期管理这个仓库，也会添加一些共性的问题和有价值的链接。

最后，大家最好直接用中文提问和回答，比较方便~

## 二、mujoco建模教程和优质资源总结：

### mujoco安装教程：
1. Linux系统完善教程，兼容Ubuntu16.04和Ubuntu18.04：
[快速安装最新版mujoco200, mujoco-py2.2.0.7,gym\[all\],robosuite，解决gcc等报错问题](https://blog.csdn.net/hehedadaq/article/details/109012048)

2. Windows安装，没有试过；

3. 云服务器安装，也没有试过，如果能有权限安装的话，和Linux安装应该区别不大。

### 基于mujoco-py的机器人仿真优质代码库推荐：
1. [gym-fetch](https://github.com/openai/gym/tree/master/gym/envs/robotics)：机械臂系列：slide，push，pick and place。
2. [robosuite](https://github.com/ARISE-Initiative/robosuite/)：如果做机械臂相关的必看！斯坦福开源的Surreal机器人项目，基于Mujoco，包含单/双臂与多种手爪组合配置，task包括pick&place、装配协作等。
3. flow-rl：如果做击球相关的，可以参考一下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210503230410787.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlaGVkYWRhcQ==,size_16,color_FFFFFF,t_70)


### 优质博客和博主推荐：
[王聪 水下机器人：MuJoCo的机器人建模](https://zhuanlan.zhihu.com/p/99991106)

[刘浚嘉 ：MuJoCo自定义机器人建模指南](https://zhuanlan.zhihu.com/p/143983506)

[PyBullet笔记（一）pybullet及其依赖项的安装、pybullet初探](https://zhuanlan.zhihu.com/p/347078711)

### mujoco相关链接：
1. 仿真部分的源代码：[https://github.com/deepmind/mujoco/blob/main/sample/simulate.cc](https://github.com/deepmind/mujoco/blob/main/sample/simulate.cc) 
2. 上面源代码主文件和文档的对应关系可以看：[https://mujoco.readthedocs.io/en/latest/programming.html](https://mujoco.readthedocs.io/en/latest/programming.html)
3. 更新版本的文档：[https://mujoco.readthedocs.io/en/latest/overview.html](https://mujoco.readthedocs.io/en/latest/overview.html) 对很多问题有更详细的介绍，适合深入开发的人员观看。
4. 修改日志：[https://mujoco.readthedocs.io/en/latest/changelog.html](https://mujoco.readthedocs.io/en/latest/changelog.html) 好像没什么特别的内容。
5. 老版本的mujoco仍然可以用，可以免费到2031年。
![在这里插入图片描述](https://img-blog.csdnimg.cn/6066bd44064c4efd943c7b58922531e4.jpg)



## 三、mujoco-py的例程
待更新
### 1. 创建系统默认对象
### 2. 渲染场景
### 3. 设定对象常见属性
### 4. 修改对象常见属性
### 5. 驱动对象
### 6. 弹性碰撞
### 7. 获取传感器信息
### 8. 场景设置：空气、灯光、相机
### 9. 其他域随机化操作
1. robosuite最新版有了一些相机、纹理的域随机化操作。
2. 也可以定制化一些灯光的随机化，需要的话可以加群讨论
### 10. 创建复合对象
1. robosuite最新版有例程，我没试过；
### 11. 外部导入机器人模型
1. 在MUJOCO建立机器人模型：[BUILDING MODELS IN MUJOCO](https://studywolf.wordpress.com/2020/03/22/building-models-in-mujoco/)

包括如何从Skechup（草图大师）创建模型，导出stl文件；
到提供xml文件模板，比较齐全

### 12. 模块化搭建机器人模型：robosuite
超详细的文档！[http://robosuite.ai/docs/overview.html](http://robosuite.ai/docs/overview.html)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210503231045747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlaGVkYWRhcQ==,size_16,color_FFFFFF,t_70)


## 联系方式：
ps: 欢迎做强化的同学加群一起学习：

深度强化学习-DRL：799378128

Mujoco建模：818977608

欢迎玩其他物理引擎的同学一起玩耍~

欢迎关注知乎帐号：[未入门的炼丹学徒](https://www.zhihu.com/people/heda-he-28)

CSDN帐号：[https://blog.csdn.net/hehedadaq](https://blog.csdn.net/hehedadaq)

极简spinup+HER+PER代码实现：[https://github.com/kaixindelele/DRLib](https://github.com/kaixindelele/DRLib)
