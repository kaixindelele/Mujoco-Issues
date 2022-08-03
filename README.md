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

[最全的强化相关的开源环境！！！强烈推荐](https://github.com/clvrai/awesome-rl-envs)

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
### 2. 两种不兼容的渲染场景设置：

1. 直接渲染：env.render()
需要确保路径有这个玩意儿：
可以在终端导入：
```
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so
```
也可以在pycharm里面直接添加.

2. 从mujoco中拿到图片：img = env.render('rgb_array', 512, 512)
如果报错：Failed to initialize OpenGL

则参考这个链接：[mujoco获取rgb_array报错Failed to initialize OpenGL](https://blog.csdn.net/hehedadaq/article/details/123012530)
注释掉：
```
# export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so
```
或进入pycharm的envronment virables，找到LD_PRELOAD，删掉上面那个东西就好了。

**这两种渲染是不能兼容的，必须手动配置！**


### 3. 设定对象常见属性
#### 3.1 设定物体的初始速度：

示例提问和回答：

   Q1：请问mujoco仿真可以在哪里设置模型的初始速度吗？不知道是应该在xml文件里设置还是在控制程序里设置？
   
   A1：通过sim.data.set_joint_qvel函数设定，或者sim.data.qvel[i]=5直接赋值。
   
       其中sim.data.qvel[i]是得给定joint的index，set_joint_qvel函数，顾名思义是给定joint的name，才能设定速度值。
       
       示例图片：
       
sim.data.set_joint_qvel得提前知道关节的名称：

![图片描述](https://img-blog.csdnimg.cn/54fcd30a090444a1a972034293491a9a.png)

sim.data.qvel[i]得提前知道关节的索引，索引可以根据函数获取：self.sim.model.get_joint_qvel_addr(joint_name)，本质上还是得用关节名字


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

## robosuite的render和image冲突问题:
相信很多同学在使用robosuite的时候，会被它的`has_render`, `has_offscreen_renderer`, `use_camera_obs`,这三个鬼东西整的不知道该如何搭配。

更诡异的是Ubuntu16.04和Ubuntu18.04及以上的配置还不一样！

### Ubuntu18.04及以上的配置：
1. 无图无渲染，即不需要渲染，也不需要offscreen产生图片信息：

![在这里插入图片描述](https://img-blog.csdnimg.cn/5d7993832ea641c49c57c38d962f9442.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAaGVoZWRhZGFx,size_20,color_FFFFFF,t_70,g_se,x_16)

2. 渲染无图：即渲染了，但是不产生图片信息：
![在这里插入图片描述](https://img-blog.csdnimg.cn/af536fe3f8324765ab680d1653f1351a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAaGVoZWRhZGFx,size_20,color_FFFFFF,t_70,g_se,x_16)

3. 不渲染有图：即不渲染，但是在observation里面能够拿到对应相机视角下图片的数据：
![在这里插入图片描述](https://img-blog.csdnimg.cn/34fce303eaf445569401358be0804a8b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAaGVoZWRhZGFx,size_20,color_FFFFFF,t_70,g_se,x_16)

包括如何从Skechup（草图大师）创建模型，导出stl文件；
到提供xml文件模板，比较齐全

### 12. 模块化搭建机器人模型：robosuite
超详细的文档！[http://robosuite.ai/docs/overview.html](http://robosuite.ai/docs/overview.html)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210503231045747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlaGVkYWRhcQ==,size_16,color_FFFFFF,t_70)

### 13.[mujoco_py的代码示例！！！](https://www.codenong.com/3160b48f32144f352b05/)

### 14. windows10安装教程：
[win10安装mujoco_py最新版本，亲测有效](https://blog.csdn.net/weixin_43263346/article/details/122062297)


## 联系方式：
ps: 欢迎做强化的同学加群一起学习：

深度强化学习-DRL：799378128

Mujoco建模：818977608

欢迎玩其他物理引擎的同学一起玩耍~

欢迎关注知乎帐号：[未入门的炼丹学徒](https://www.zhihu.com/people/heda-he-28)

CSDN帐号：[https://blog.csdn.net/hehedadaq](https://blog.csdn.net/hehedadaq)

极简spinup+HER+PER代码实现：[https://github.com/kaixindelele/DRLib](https://github.com/kaixindelele/DRLib)
