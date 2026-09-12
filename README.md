# Agent English Speaking Coach

一套基于 Codex 的英语口语陪练模板：用自己的兴趣和材料开展对话，每次练习后留下复盘，下次接着练。

陪练规则写在 [AGENTS.md](AGENTS.md)，学习者档案、周计划和每日记录保存在本地文件中。Codex 负责对话和执行文件操作；这些文件为它提供规则和学习进度。[OpenAI 官方说明](https://learn.chatgpt.com/docs/agent-configuration/agents-md)介绍了项目指令文件的作用。

本项目目前是初版模板；尚未进行新账号的完整语音试用，也没有标准化学习效果评估。

## 开始使用

需要能打开本地文件夹并读写文件的 Codex 环境。口语练习还需要当前客户端可用的语音功能。本仓库没有独立语音应用，也没有模型或录音服务；无需运行脚本或安装项目依赖。

1. 在[仓库首页](https://github.com/kukuxiaogua/Agent-English-Speaking-Coach)点击 **Code → Download ZIP** 并解压，在 Codex 中把它作为项目打开。选择含有本 README 和 `AGENTS.md` 的这一层目录。
2. 在文字对话中发送下面的首次设置提示。已有答案可以一次说完，不必接受重复访谈。
3. 设置完成后，开启客户端的语音功能，开始一个短话题。

习惯使用 Git 的人也可以克隆：

```sh
git clone https://github.com/kukuxiaogua/Agent-English-Speaking-Coach.git
```

首次设置示例：

> 请读取 AGENTS.md，帮我初始化英语陪练。我希望能用英语聊日常生活，每天计划练习 20 分钟，喜欢做饭和电影，时区是 Europe/London。设置过程用中文，正式练习用英语。先根据这些信息创建档案和本周计划，再开始一个简短话题；不要预设我的英语等级。

时长、兴趣和时区都换成自己的。你也可以只说“请帮我初始化英语陪练”，让助手一次询问一个必要问题。

初始化会根据 `templates/` 创建自己的 `data/learner-profile.md`、本周计划和所需目录，不会复制示例里的身份、表现或历史。

## 日常怎么用

| 场景 | 可以这样说 |
| --- | --- |
| 开始今天的练习 | “Let's continue from my last review.” |
| 提供自己的材料 | “I'd like to talk about this short passage.” 然后提供正文或本项目内的文件 |
| 听不懂问题 | “Could you ask a shorter question?” |
| 想换话题 | “Let's talk about something else.” |
| 暂停并保存 | “Let's pause. Save my progress and the next step.” |
| 结束并复盘 | “Let's finish. Save today's review and update the weekly plan.” |

如果关闭语音后没有看到保存结果，在同一任务的文字对话里补一句：

> 请根据本次可见的对话补存复盘，注明缺失的时间信息，并写清楚下次从哪里继续。

每次优先读最新记录、继续未完成活动。到新的一周，助手在当前对话中生成新计划，不需要预先配置定时任务。只有完成活动或改变安排时才更新周任务状态。

## 陪练方式

- 一次一个短问题；不明白时先简化英语或举例。
- 先交流，话题结束后再选两三处有用的修正；每处最多在新例子里练一次。
- 先确认你想表达什么，再给反馈；追问来源和请求解释也属于交流。
- 使用你提供的材料；没有材料时提供一个简单的备用话题。
- 记录实际表现、所需帮助和下次起点；不凭文字转写判断发音或编造能力等级。

练习与学习记录默认用英语。可以明确要求中文解释，或在档案里修改偏好。安装、文档整理等工作使用你提出请求时的语言。

## 文件清单

| 文件 | 用途 |
| --- | --- |
| [AGENTS.md](AGENTS.md) | 助手执行的陪练流程和证据规则 |
| [.gitignore](.gitignore) | 忽略个人数据、编辑器配置等 |
| [templates/learner-profile.md](templates/learner-profile.md) | 空白学习者档案 |
| [templates/weekly-plan.md](templates/weekly-plan.md) | 空白周计划 |
| [templates/daily-review.md](templates/daily-review.md) | 空白复盘和会话日志 |
| [examples/learner-profile.md](examples/learner-profile.md) | 虚构档案示例 |
| [examples/weekly-plan.md](examples/weekly-plan.md) | 虚构周计划示例 |
| [examples/daily-review.md](examples/daily-review.md) | 虚构每日复盘示例 |
| [docs/design-notes.md](docs/design-notes.md) | 规则的来由及后续观察方法 |

加上本 README，共 10 个公开文件。`examples/` 中的所有人物、表达、时间和结果都是虚构的展示内容，不能作为真实学习证据。

自己的学习文件在使用后生成：

```text
data/
├── learner-profile.md
├── week-plans/
│   └── YYYY-MM-DD.md       # 使用者当地本周周一的日期
├── daily-reviews/
│   └── YYYY-MM-DD.md       # 使用者当地练习日期
└── materials/             # 可选：自己提供的练习材料
```

`data/` 已被 Git 忽略。不要强制添加个人记录；`.gitignore` 不会清除已经提交的文件，也不会阻止你手动上传它们。

## 时间与能力边界

这是依靠明确指令和本地文件接续的陪练流程。具体语音、时间事件和工具能力由运行它的客户端决定。

助手优先使用可用的语音开始和结束事件，其次使用可靠的时钟读数。如果只知道部分时间，就标注部分计时；如果无法分别测量暂停或工具等待，就不推算有效练习时长。一次通话 20 分钟不自动等于有效练习 20 分钟。

客户端未必会在断线或直接关闭语音时触发保存。因此，结束前明确要求复盘最容易检查；恢复对话时可以根据仍可见的历史补记，缺失部分注明未知。只有文字转写可见时，不评价发音、语速或停顿；语音模式也不自动代表具备可靠的发音评测能力。

## 调整与贡献

改交流节奏或纠错方式，编辑 `AGENTS.md`；改自己的目标和兴趣，更新 `data/learner-profile.md`。模板更新不会自动改写已经生成的历史记录。

反馈问题时，提供期望行为、实际行为和去掉个人信息的最小示例。修订规则后，观察它是否解决原问题、是否增加了不必要的步骤，再决定保留。请保持模板、示例和 README 中的路径一致。

当前尚未指定开源许可证，也未附带 `LICENSE`；选定后会在仓库中补充。
