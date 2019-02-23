# 开源机器人学学习指南 <!-- omit in toc -->

# 目录 <!-- omit in toc -->
- [前言](#前言)
- [先修知识](#先修知识)
- [入门](#入门)
- [勇者斗恶龙](#勇者斗恶龙)
- [参考文献](#参考文献)


## 前言

**[RVBUST INC.](http://www.rvbust.com)** 成立半年有余。面试过不少从事机器人研究的小伙伴后，我发现一个问题：**绝大多数大陆的毕业的学生都不像是「科班出身」的**。

当然，如果仅从工作教育经历上看——大部分毕业于机电、计算机专业，甚至是研究机器人的实验室，有过机器人公司的工作经历——这些人应该都算是「专业选手」。

但是，从面试情况上看，绝大多数人都不具备机器人学的完整知识体系：画电路板的小伙伴不知道怎么进行机器人工作空间分析；设计机构的小伙伴不知道怎么把动力学用在控制上；做控制算法的小伙伴不知道什么的构型空间（Configuration Space）；做运动规划的小伙伴不知道什么是Q-learning；做深度强化学习的小伙伴不知道学习到的控制指令要怎么让实际机器人运动起来。

从我这几年的学习经历上看，我是能理解这一现象的。博士刚入学的时候，我接下了师兄的 SmartPal 机器人。靠着师兄的「祖传代码」，也曾狐假虎威地在外宾面前做过一些演示：

<p align="center">
  <img width="500" src="./Pics/SmartPalAndMe.jpg">
</p>

但是，当我后来真正开始看这些「祖传代码」的时候，我发现实际发给机器人的只有几个关节**位置**点而已。

**「PID 在哪里？？？」**

这是我当时产生的最大疑问，这个代码逻辑跟我本科玩得四旋翼、智能车等都完全不一样。

于是，拿着这个疑问，我在实验室问了一圈，没有得到答案。即使后来，我选修了好几门跟机器人相关的研究生课程。经过一年的学习，我还是没有得到答案。

是的，作为国内最早开展机器人研究的院校之一，这里的机器人研究生课程只教我们如何建立 DH 坐标系，动力学只是简单计算了一个平面三连杆。根本没有涉及控制、轨迹规划的内容，甚至连运动学逆解也没有要求大家计算。

据我所知，很多其他研究机构也是如此，机器人学这块还没有形成完整的教学体系。所以，基本上学生都没有接受过完整的机器人学系统教育，只有在做项目的时候通过自学掌握项目所需的内容。这也就造就了一大批没有算过机器人运动学逆解的机器人专业博硕士生。

当然，这一情况在大陆比较普遍，而国外或者港台高校毕业的学生，基本上都没有这个问题。国外或者港台高校在机器人学这块的教学体系相对比较完整，基本上大作业都会覆盖主要的知识点，并且大都要求编程实现。

虽然，大多数小伙伴都是「非科班出身」的，但是，根据我的经验，大陆的学生还是非常聪明的，基本只要得到一些简单的正确引导，就能很快通过自学掌握这些知识。所以，我们不妨来看看「非科班出身」如何学习机器人学吧。

## 先修知识

当然，先修知识会随着研究深度的变换而不同，尤其是数学，数学就像是写轮眼，看同一个石碑，不同层次的「写轮眼」所看到的内容也完全不同。

<p align="center">
  <img width="800" src="./Pics/Sharingan.jpg">
</p>

但是，由于机器人学涉及面广，不同方向所需要的基础知识也完全不同，如果一开始就陷入「先修知识」的泥潭中，可能就得不偿失了。

所以，我认为，可以先列一些真正必须掌握的先修知识，其他的在后续相应部分提及即可：

1. **基本的英文**：在机器人方面，目前基本上没有非常合适的中文教材可以推荐。写得深入浅出的教材都是国外的，大家**必须**学会阅读英文文献。这个过程一开始肯定是痛苦的，但是，基本上坚持一个月就会习惯了。

2. **学会使用 VPN**。原因同上，基本上有用的资料都需要通过 Goolge 或 Youtube 获取。

3. **线性代数**：所有的空间变换、机器人相关计算都依赖于线性代数，甚至需要有一些基本的"线性空间"思维。对于线性代数，我首推 Prof. Gilbert Strang 的《Linear Algebra》，在 [Youtube](https://www.youtube.com/watch?v=hNDFwVVKVk0&list=PL221E2BBF13BECF6C) 和[网易公开课](http://open.163.com/special/opencourse/daishu.html)上可以找到视频。这门课一开始就引导大家从空间的角度看待问题，而不像国内高校，只要强调如何计算。

4. **微积分**：机器人里，所有涉及到导数、积分、优化的地方，都会有微积分的影子。所以，这门数学课也是一开始就绕不开的。我没有太好的视频推荐，不妨也看看 Gilbert Strange 的[微积分重点](http://open.163.com/special/opencourse/weijifen.html)？

5. **理论力学**：机器人学就是每天与力打交道。但是一般机器人教材里都不会仔细推导空间变换、虚功原理、拉格朗日等力学理论，而且这些东西又相对抽象，很多初学者的自学过程就是被截杀在动力学章节的。当然，这部分我也没有太好的推荐资料，学堂在线上有清华高云峰老师的[理论力学](https://www.xuetangx.com/courses/TsinghuaX/20330334X/_/about)公开课，也可以参考一下。（但至少我当年上他的课总是想睡觉）。

## 入门



John Craig <sup>[1]</sup>

## 勇者斗恶龙

🐀🐂🐅🐇🐉🐍🐎🐏🐒🐓🐕🐖


$S = 2\cdot \pi \cdot r^2$

## 参考文献
[1] John J. Craig. Introduction to Robotics: Mechanics and Control[M]. 1986.