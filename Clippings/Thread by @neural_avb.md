---
title: "Thread by @neural_avb"
source: "https://x.com/neural_avb/status/1967469439403872342"
author:
  - "[[@neural_avb]]"
published: 2025-09-15
created: 2025-10-01
description:
tags:
  - "clippings"
---
**AVB** @neural\_avb [2025-09-15](https://x.com/neural_avb/status/1967469439403872342)

If you truly want to learn RL, ditch the readymade gym environments.  
如果你真想学习 RL，就不要使用现成的 gym 环境。  
  
Make a custom environment on your own. You’ll understand how to structure rewards, observations, random initialization states, etc. also, how to debug and render. This is the most practical skill you can get in RL. You can literally implement any env you want - a game, a robotic control task, a text thingy, whatever you feel interested in.  
自己创建一个自定义环境。你会理解如何构建奖励、观察值、随机初始化状态等，同时学会调试和渲染。这是你在 RL 中能获得的最有实践意义的技能。你可以真正实现任何你想实现的环境——一个游戏、一个机器人控制任务、一个文本处理任务，无论你对什么感兴趣都可以。  
  
For the training algorithm, start with SB3 modules as you’re building the env. This will teach you the important hyperparameters and save you the headache of debugging your env and your training at the same time (trust me don’t do this).  
在构建环境时，从 SB3 模块开始训练算法。这将教你重要的超参数，并且可以避免同时调试环境和训练时的头痛问题（相信我，不要这样做）。  
  
Then once you can see it train on your custom env, and you are confident there’s no bugs, create your own implementation from scratch.  
然后一旦你能在自定义环境中看到它训练，并且你确信没有 bug，就从头开始自己实现。  
  
This will teach you exploration, memory, and the actual optimization loop.  
这将教会你探索、记忆以及实际的优化循环。  
  
The minimal algorithms you should know are: DQN/DDQN, REINFORCE, A2C, PPO. Implement in that exact order.  
你应该掌握的最小算法有：DQN/DDQN、REINFORCE、A2C、PPO。按照这个顺序实现。  
  
There’s nothing more rewarding than training a custom agent in your custom environment. You get the full tour of RL.  
在你自定义的环境中训练自定义代理是最有成就感的事情。你将全面体验到强化学习的全过程。  
  
If you read this far, you are ready to do all of the steps above. Take your sweet time but just do it.  
如果你读到这里，你已经准备好完成上述所有步骤。慢慢来，但一定要去做。