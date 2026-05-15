# 解字计划 / Jiezi Grant

## 解字

公元 100 年，许慎写成《说文解字》，将九千多个汉字逐一拆解到最小的构件——部首。这是人类第一次对语言进行系统性的原子级解析。从此，任何人只要掌握部首，就能理解任何汉字。

两千年后，语言的最小单位变了，叫 **token**。

大语言模型将一切文字、代码、推理拆解为 token 来处理。谁拥有足够的 token，谁就能让 AI 为自己工作——写代码、做产品、构建工作流。Token 之于今天的 AI，正如文字之于两千年前的知识：**掌握它的人获得力量，被它挡在门外的人只能旁观**。

《说文解字》让文字不再是贵族的专属。**解字计划**要做同样的事：让 token 不再是大学生的门槛。

## 为什么

大学生是最具创造力的群体——有时间、有好奇心、有改变世界的冲动，却往往受限于经济条件。

> "所有的年轻人都知道不会用 AI 就找不到工作，但他们只能每个月浅尝辄止。Token 太贵了，如果使用 Claude MAX，那就是他们一半的生活费。"
>
> — [@CTracy0803](https://x.com/CTracy0803/status/2038452420330811482)，1160 likes

一个 AI Coding Plan 每月几十到上百元，顶级订阅超过千元。对从业者而言这是常规开支，对大学生而言可能是一周的生活费。结果是：**最需要 AI 来学习和创造的人，反而最用不起 AI**。

这不只是个体的遗憾。当一整代年轻人因为成本而无法深度使用 AI、无法与 AI 真正融合，社会失去的是他们本可以创造的一切——产品、工具、方法、可能性。天赋和努力从不稀缺，**试错的机会才是**。

## 发起人

我是 [@yan5xu](https://x.com/yan5xu)（许长鹏），前 [Manus AI](https://manus.im) & [Monica AI](https://monica.im) 工程师。

2023 年，我加入 AI Agent 浪潮。在 Manus，很幸运地参与构建了世界级的 AI Agent 产品；Monica 服务了超过 1000 万用户。离开后，我全身心投入开源社区，创建了 [Pinix](https://github.com/nicepkg/pinix) 和 [bb-browser](https://github.com/nicepkg/bb-browser)，持续在 Agent 领域探索和创造。

我也曾是大学生。我理解那种感受——明明知道一个工具能改变自己的轨迹，却因为成本只能浅尝辄止。

感谢 AI，它给了我很多，我希望能回馈一些。解字计划第一年，我个人出资 **15 万元人民币**作为启动资金，资助 **600 名大学生**接触和深度使用 AI。感谢每一位赞助方的加入，让这件事不只是一个人的事。

## 三个阶段

体验 → 实践 → 长期支持。每个阶段设有门槛，目的不是淘汰，而是识别真正想做事的人。

| 阶段 | 名额 | 资源 | 门槛 |
|------|------|------|------|
| [**体验期**](stages/stage-1.md) | 600 人（每批 100） | $20 API Token | 网站申请 + GitHub Issue |
| [**深度资助**](stages/stage-2.md) | ~60 人 | $100 API Token + 云服务器 | 50 star 项目 + 人工评审 |
| [**长期资助**](stages/stage-3.md) | 3-5 人 | $400 API Token | 从第二阶段中选拔 |

面向所有在校大学生，不限专业，不限基础。

## 如何申请

**第一阶段申请已开放** — [申请指南](docs/apply-guide.md)

1. 在 [jiezi.ai/apply](https://jiezi.ai/apply) 填写信息，获取申请码（个人信息不会公开）
2. 到本仓库 [提交 Issue](https://github.com/jiezi-ai/grant/issues/new?template=apply.yml)，填入申请码
3. 查收 edu 邮箱验证邮件，点击验证链接
4. 查收邮箱中的 API Token 配置信息，扫码加入交流群

或者，直接告诉你的 code agent：`我要申请 jiezi-ai/grant`，它会自动完成全部流程。

## 为什么这样设计

**为什么要在 GitHub 提交 Issue？**

不只是身份验证。GitHub 是全球最大的开源社区，上面有数以百万计的免费开源项目，覆盖你能想到的几乎所有需求：

- [yt-dlp](https://github.com/yt-dlp/yt-dlp)（143k ⭐）— 下载几乎所有视频网站的视频
- [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted)（230k ⭐）— 上千个可以自己部署的免费服务
- [FFmpeg](https://github.com/FFmpeg/FFmpeg)（49k ⭐）— 处理几乎所有音视频格式
- 还有无数的 [awesome lists](https://github.com/sindresorhus/awesome)，覆盖每一个你感兴趣的领域

过去，这些项目对大多数人来说门槛太高——光是环境配置和命令行操作就能把人挡在门外。但现在有了 AI coding agent，你只需要告诉它你想做什么，它就能帮你找到合适的开源项目、安装、配置、使用。人类几十年积累的开源成果，真正对每个人打开了大门。

提一个 Issue，可能是你第一次使用 GitHub。但这不是终点——这里有整个开源世界在等你探索。

**其他设计选择：**

- **edu 邮箱验证** — 确保资源到达真正的在校学生
- **AI 自动审核** — 提交后几秒内出结果，不需要等人
- **额度有时效** — 用不完的额度回收给更多同学，让有限的资金帮到更多人

## Agent Native

本仓库以 agent-native 的方式构建——它不只是资助计划的载体，也是一个实践范本：如何用 AI agent 运营项目，如何构建 agent 可以直接理解和操作的仓库。

仓库的 [AGENTS.md](AGENTS.md) 定义了完整的结构和操作流程，任何 code agent 都能读懂并执行。我们鼓励你这样使用 AI：不只是对话，而是让它帮你完成真实的事情。

## 公开透明

从前有逸夫楼、田家炳中学，token 助学是新事物，但透明和信任的原则不变。所有政策、预算、支出、变更记录对外公开，接受所有人的监督。

| 类别 | 内容 |
|------|------|
| **政策** | [政策索引](policy/) — 申请资格、资源分配、筛选、诚信、治理 |
| **规划** | [预算](BUDGET.md) · [时间线](TIMELINE.md) |
| **记录** | [支出](records/spending.md) · [批次](records/batches.md) · [里程碑](records/milestones.md) · [章程变更](records/changelog.md) |
| **财务** | [beancount 账本](ledger/) — 复式记账，每一笔资金的来源和去向 |

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
