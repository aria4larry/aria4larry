


> Written with [StackEdit](https://stackedit.io/).

## 任务
> AI Agent 自主通过操作UI 完成用户给定的任务 比如 “使用美团外卖给我订一份奶茶外卖”

## 环境感知
### 任务感知
* LLM NLP/NLU能力，理解用户给的任务
### 手机UI感知
* GPT4o 图像识别、理解能力。

## 工具使用
* LLM调用Tool
* UI Automator 操作手机
* 简化的Action 空间
	* Tap
	* DoubleTap
	* Swipe (direction)
	* Back
	* Home
	* Text
	* Finish

## 学习、泛化
### LLM本身的泛化能力 - 对手机画面、世界的Common理解（黑盒）
### 强化学习（Reinforcement Learning）
> 对于给定任务，利用操作经验达到近似最优解

## 技术重点
### Multi-Agent 架构 发挥LLM的Common能力（Observation - Planning - Reasoning - Action - Reflection）
### 短期记忆处理，关键记忆处理
### 长期记忆处理：
#### 外部输入的知识库
#### 强化学习得到的RL模型
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjAzMTg0NjFdfQ==
-->