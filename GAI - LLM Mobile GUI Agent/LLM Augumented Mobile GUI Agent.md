


> Written with [StackEdit](https://stackedit.io/).

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
强调如何基于环境而行动，以取得最大化的预期利益。其关注点在于寻找探索（对未知领域的）和利用（对已有知识的）的平衡。
![典型框架：智能体在环境中采取一种行为，环境将其转换为一次回报和一种状态表示，随后反馈给智能体。](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Reinforcement_learning_diagram.svg/375px-Reinforcement_learning_diagram.svg.png)

> 典型框架：智能体在环境中采取一种行为，环境将其转换为一次回报和一种状态表示，随后反馈给智能体。

基本的强化学习被建模为马尔可夫决策过程：

1.  环境状态的集合![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2);
2.  动作的集合![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3);
3.  在状态之间转换的规则（转移概率矩阵）![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a)；
4.  规定转换后“即时奖励”的规则（奖励函数）![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33)；
5.  描述主体能够观察到什么的规则。

**Policy Based** : 输入状态和Action空间，输出各个Action的概率。
* -   _Deterministic_: a policy at a given state  **will always return the same action.**
![enter image description here](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Yaw0uCoQf1HFjVhu_ETVsw.jpeg)
* -   _Stochastic_: outputs a  **probability distribution over actions.**
![Policy Based RL](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Y8o17gdqUdpxy0Ko2EJ0ZA.png)


**Value Based**: 
## 5. 参考文献
* [1. Hierarchical Multi-Agent](https://langchain-ai.github.io/langgraph/tutorials/multi_agent/hierarchical_agent_teams/)
* [2. AI Learns to Walk (deep reinforcement learning)](https://www.youtube.com/watch?v=L_4BPjLBF4E)
* [3. Open AI RL learn to play Hide and Seek](https://www.youtube.com/watch?v=Lu56xVlZ40M)
* [4. AppAgent: Multimodal Agents as Smartphone Users Github Project](https://appagent-official.github.io/)
* [5. AppAgent: Multimodal Agents as Smartphone Users Paper](https://arxiv.org/pdf/2312.13771.pdf)
* [6. MobileAgent github project](https://github.com/X-PLUG/MobileAgent)
* [7. Mobile-Agent-v2: Mobile Device Operation Assistant with Effective Navigation via Multi-Agent Collaboration](https://arxiv.org/abs/2406.01014)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2NzI2MzExMiwtMTQwNDQ4ODM1LDE0Nz
YyMDM2MSw5MTkyNzcwOTEsNTY0ODM2MTIwLC0zNzIwMTM5NzQs
LTczODI0MjQ1NCw4OTU4Njc5MTMsMTg0MjM5ODY4OCwxNzM0Mz
I2ODQ2LC0xNTEyOTkxNzYzXX0=
-->