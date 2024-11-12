


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
#### 4.1.2 React Reasoning + Reflection
### 4.2 短期记忆处理，关键记忆处理
**短期记忆（工作记忆）**：完成某个特定任务并不需要记住所有历史**操作**和**状态**， 类比人类的记忆系统，只需要ynwy
### 4.3 长期记忆处理：
#### 4.3.1 外部输入的知识库
#### 4.3.2 ***强化学习得到的RL模型***
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwMTcxMTc4NSwxNzM0MzI2ODQ2LC0xNT
EyOTkxNzYzXX0=
-->