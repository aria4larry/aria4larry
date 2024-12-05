
## 任务
> AI Agent 自主通过操作UI 完成用户给定的任务 比如 “使用美团外卖给我订一份奶茶外卖”

## 1. 环境感知
### 1.1 任务感知
* LLM NLP/NLU能力，理解用户给的任务
### 1.2 手机UI感知
* GPT4o 图像识别、理解能力。

## 2. 工具使用
### 2.1 LLM调用Tool
### 2.2 UI Automator 操作手机
### 2.3 图像处理，精确的获取画面对应的可操作的Action空间
* 简化的Action 空间
	* Tap
	* DoubleTap
	* Swipe (direction)
	* Back
	* Home
	* Text
	* Finish

## 3. 学习、泛化
### 3.1 LLM本身的泛化能力 - 对手机画面、世界的Common理解（黑盒）
### 3.2 强化学习（Reinforcement Learning）
> 对于给定任务，利用操作经验达到近似最优解
### 3.3 保存知识库
- 人为提供、标注的知识库
- Agent训练或者运行时见过的知识库Summary

## 4. 技术重点
### 4.1 Multi-Agent 架构 发挥LLM的Common能力（Observation - Planning - Reasoning - Action - Reflection）
#### 4.1.1 LangGraph + Hierarchical Multi-Agent
纯API使用，参考LangGraph文档,略
#### 4.1.2 React Reasoning + Reflection
### 4.2 短期记忆处理，关键记忆处理
**短期记忆（工作记忆）**：完成某个特定任务并不需要记住所有历史**操作**和**状态**， 类比人类的记忆系统，只需要记住5-7 个历史 **操作**和**状态**即可。这样可以 **节省Token**, **加快LLM返回速度**。

**关键记忆**： 短期记忆中还需要判断某些**状态、操作** 可能是关键记忆，需要在整个任务过程中保存。比如跨APP操作 “查询成都的天气，并发送给我的微信好友 A”， 操作步骤中间中天气APP得到的天气信息需要作为关键记忆保留到任务完成。
### 4.3 长期记忆处理：
#### 4.3.1 外部输入的知识库
#### 4.3.2 ***强化学习得到的RL模型***
强调如何基于环境而行动，以取得最大化的预期利益。其关注点在于寻找探索（对未知领域的）和利用（对已有知识的）的平衡。***强化学习：适合需要序列决策的动态环境***
![典型框架：智能体在环境中采取一种行为，环境将其转换为一次回报和一种状态表示，随后反馈给智能体。](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Reinforcement_learning_diagram.svg/375px-Reinforcement_learning_diagram.svg.png)

> 典型框架：智能体在环境中采取一种行为，环境将其转换为一次回报和一种状态表示，随后反馈给智能体。

基本的强化学习被建模为马尔可夫决策过程：

1.  环境状态的集合![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2);
2.  动作的集合![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3);
3.  在状态之间转换的规则（转移概率矩阵）![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a)；
4.  规定转换后“即时奖励”的规则（奖励函数）![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33)；
5.  描述主体能够观察到什么的规则。



**Policy Based** : 输入状态和Action空间，输出Action或者各个Action的概率。即学习Agent在各个状态下应该做什么Action:
![enter image description here](https://miro.medium.com/v2/resize:fit:720/format:webp/1*F1btD4VBjq66HAz_hzngOg.jpeg)

-   _Deterministic_: a policy at a given state  **will always return the same action.**
![enter image description here](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Yaw0uCoQf1HFjVhu_ETVsw.jpeg)
-   _Stochastic_: outputs a  **probability distribution over actions.**
![Policy Based RL](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Y8o17gdqUdpxy0Ko2EJ0ZA.png)

**Value Based**: 学习在某个状态下对应的回报, （默认Policy 最大化整体回报）：
![enter link description here](https://miro.medium.com/v2/resize:fit:720/format:webp/1*wqiFCC7kERiI1W_gm71JMQ.jpeg)


## 强化学习实做
### Task： 根据手机画面实时截图，操作手机（点击、输入），完成用户给定任务，如“在美团上订一份奶茶外卖”
**训练目标**： 完成用户给定的任务。
**Actions Space(动作集合)**: 操作手机上的元素，坐标，输入文本、按键等
	* Tap
	* DoubleTap
	* Swipe (direction)
	* Back
	* Home
	* Text
	* Finish
**方法**： 使用PyTouch训练一个神经网络来做为输入对应输出的 Policy Network.
	Policy Network输入：截图 + ??  （如何转换为向量？）
	Policy Network输出：对应Action的概率分布
	![PolicyNetwork](https://gymnasium.farama.org/_images/reinforce_invpend_gym_v26_fig2.png)

**环境**
* **Observation Space** （模型输入）:  ？？？ 截图对应的embedding?
* **Rewards**: ??? 目标是完成用户给定的任务，
	* 截图变化、Activity变化 +1？


## 5. 参考/文献
1. [Hierarchical Multi-Agent](https://langchain-ai.github.io/langgraph/tutorials/multi_agent/hierarchical_agent_teams/)
2. [AI Learns to Walk (deep reinforcement learning)](https://www.youtube.com/watch?v=L_4BPjLBF4E)
3. [Open AI RL learn to play Hide and Seek](https://www.youtube.com/watch?v=Lu56xVlZ40M)
4. [AppAgent: Multimodal Agents as Smartphone Users Github Project](https://appagent-official.github.io/)
5. [AppAgent: Multimodal Agents as Smartphone Users Paper](https://arxiv.org/pdf/2312.13771.pdf)
6. [MobileAgent github project](https://github.com/X-PLUG/MobileAgent)
7. [Mobile-Agent-v2: Mobile Device Operation Assistant with Effective Navigation via Multi-Agent Collaboration](https://arxiv.org/abs/2406.01014)
8. [Reinforcement Learning 101: Best Introduction for Beginners](https://cyborgcodes.medium.com/reinforcement-learning-101-best-introduction-for-beginners-b08c4b5e6b43)
9. [Gym](https://www.gymlibrary.dev/) Gym OpenAI 开发的用于构建和比较强化学习（Reinforcement Learning, RL）算法的工具包。它提供了一系列标准化的环境，供研究人员和开发者测试和评估他们的强化学习算法。
10. [Gymnasium](https://gymnasium.farama.org/) Gymnasium, This is a fork of OpenAI's [Gym](https://github.com/openai/gym) library by its maintainers (OpenAI handed over maintenance a few years ago to an outside team), and is where future maintenance will occur going forward.    
    ![Lunar lander](https://gymnasium.farama.org/_images/lunar_lander.gif)
11. [arxiv: Gymnasium: A Standard Interface for Reinforcement Learning Environments](https://arxiv.org/abs/2407.17032)


## 机器学习主要范式对比：强化学习、监督学习和非监督学习 
### 对比表格 
| 特征 | 强化学习 | 监督学习 | 非监督学习 |
|------|----------|----------|------------| 
| 学习目标 | 最大化累积奖励 | 预测正确标签 | 发现数据中的模式或结构 | 
| 数据输入 | 环境状态 | 标记数据 | 无标记数据 | 
| 反馈方式 | 延迟的奖励信号 | 即时、直接的正确答案 | 无直接反馈 | 
| 交互性 | 高（与环境持续交互） | 低（静态数据集） | 低（静态数据集） | 
| 决策过程 | 序列决策 | 单次决策 | 通常无决策过程 | 
| 探索与利用 | 需要平衡 | 不适用 | 不适用 | 
| 典型应用 | 游戏AI、机器人控制、推荐系统 | 图像分类、语音识别、垃圾邮件检测 | 聚类分析、异常检测、降维 | 

### 主要特点 
#### 强化学习 
- 智能体通过与环境交互来学习 
- 基于试错学习，通过奖励信号指导行为 
- 需要平衡探索新动作和利用已知好的动作 
- 适合解决序列决策问题 
#### 监督学习 
- 使用已标记的数据集进行训练 
- 目标是学习输入到输出的映射 
- 性能通过预测准确度直接评估 
- 适合有明确标签的问题 
#### 非监督学习 
- 使用无标记数据集 
- 目标是发现数据的内在结构或模式 
- 没有明确的正确答案 
- 适合数据探索和模式识别 
### 关键区别 
1. **反馈机制**：
 - 强化学习：延迟的、稀疏的奖励信号 
 - 监督学习：即时的、明确的正确答案 
 - 非监督学习：通常没有外部反馈 
 2. **学习过程**： 
 - 强化学习：通过与环境交互进行在线学习
 -  监督学习：通过最小化预测误差进行离线学习 
 - 非监督学习：通过发现数据内在结构进行离线学习 
 3. **应用场景**： 
 - 强化学习：适合需要序列决策的动态环境 
 - 监督学习：适合有大量标记数据的预测任务 
 - 非监督学习：适合数据探索和模式发现任务 
 4. **评估方式**： 
 - 强化学习：累积奖励或任务完成度 
 - 监督学习：预测准确率或误差 
 - 非监督学习：聚类质量或重构误差等内部指标
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjAzMzYzMjc4LC0yMTI0NTg3MDcsMTU2OD
E1MDMyOSw3ODg1NzA4NTEsMTU1OTM5OTUxMCw1ODczMTMyOTIs
NDcxNTkxMTM3LDE3MDYwODgzMzEsMTM0NTU2MzE1Myw3MjM4MT
IxODUsMTkzNzYxNzIwNSwxNDA2NjU5NjkxLDEwNjcyNjMxMTIs
LTE0MDQ0ODgzNSwxNDc2MjAzNjEsOTE5Mjc3MDkxLDU2NDgzNj
EyMCwtMzcyMDEzOTc0LC03MzgyNDI0NTQsODk1ODY3OTEzXX0=

-->