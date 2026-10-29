# CS Rebuttal Skill · 顶会 Rebuttal 助手

[English](README.en.md) · [技能指令](skills/draft-cs-rebuttal/SKILL.md) · [MIT License](LICENSE)

把计算机会议论文的审稿意见转化为**中文回应策略、基于证据的英文 Rebuttal，以及明确的补实验和论文修改建议**。

这个技能将作者总结的 Rebuttal 经验整理为可复用的工作流：先读懂审稿人真正关心的技术问题，再决定用什么证据回答，最后写成专业、直接、不卑不亢的回应。支持单条意见，也支持整套 reviews。

## 快速安装

在支持 Agent Skills 的本地 AI 编程工具中，可通过 [skills CLI](https://github.com/vercel-labs/skills) 安装。使用该命令需要 Node.js 22.20 或更新版本：

```bash
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal
```

按照交互提示选择工具。默认安装到当前项目，增加 `-g` 可安装到个人范围。也可以明确选择：

```bash
# Codex：个人范围
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal -a codex -g

# Claude Code：个人范围
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal -a claude-code -g
```

本项目本身是 Markdown 指令和参考材料，不需要启动服务或配置单独的 API。模型访问、文件读取和联网能力由所使用的 AI 工具提供。

## 它能做什么

| 任务 | 具体处理 |
|---|---|
| 分析审稿意见 | 将复合评论拆成独立问题，区分明确质疑与可能的深层关切 |
| 回应创新性质疑 | 核对指定相关工作，说明具体差异、差异的价值及支持证据 |
| 处理误解 | 用方法解释和核实的位置澄清事实，避免指责审稿人 |
| 回应实验质疑 | 检查参数量、计算预算、数据划分、基线、消融与统计可靠性 |
| 安排补充实验 | 按重要性、成本与截止时间排序，优先做能解除关键疑虑的最小验证 |
| 融入新结果 | 核对结果实际支持什么，更新相关回应，处理负向或混合结果 |
| 修改和压缩回复 | 检查直接回答、语气、术语、数字、修改状态及字数限制 |
| 提交前检查 | 优先找必须修复的实质问题，并给可替换文本 |

覆盖八类常见情形：参数量混淆、事实误解、创新性不足、实验设置与基线、小幅提升的价值、泛化与鲁棒性、范围外要求或真实局限、含糊或前后矛盾的意见。

## 默认输出

1. **中文策略分析**：审稿人明确提出了什么，可能担忧什么，建议采取什么立场，用什么证据回答。
2. **英文回应**：保留评论编号，尽快进入直接回答，用具体证据支撑，并写清已完成或已确认的修改动作。
3. **必要补充与论文修改**：列出尚缺的证据、最值得做的补实验，以及对应论文修改。

材料充分时直接起草；材料不足时先写有依据的部分，把缺口标明为例如 `[matched-parameter results needed]`。不会把建议实验写成已经完成，也不会把未知数据、章节或表号填成看似真实的内容。

可以随时要求“只给英文”“只改这一段”“保持原来的 LaTeX 格式”或“英文正文限制在 300 词以内”。

## 开始使用

### 单条审稿意见

在 Codex 中使用 `$draft-cs-rebuttal`；在 Claude Code 中使用 `/draft-cs-rebuttal`。在提供技能选择器的其他工具中，选择 `draft-cs-rebuttal` 后描述任务。

```text
请使用 $draft-cs-rebuttal，先给中文策略，再写英文回应。

审稿意见：
“It is unclear whether the improvement comes from the proposed module
or the larger model size.”

论文相关内容：
[贴入模块设计、原实验设置和相关段落]

已有证据：
[贴入已完成的参数匹配实验；如果没做，请直接说明没做]

限制：
[字数上限、截止时间、可用计算资源；没有可省略]
```

### 整套 reviews

```text
请使用 $draft-cs-rebuttal 处理下面整套 reviews。
先按核心问题整理中文策略和补实验优先级，
再按 reviewer 编号输出完整英文回应。

摘要与主要贡献：[内容]
审稿意见、分数及量表含义：[内容]
论文及相关补充材料：[附件或内容]
已完成的新实验和设置：[内容]
作者已经决定的论文修改：[内容]
截止时间与长度限制：[内容]
```

只提供一条评论也可以开始，不必填完全部字段。若仅有评论而没有论文或结果，输出会明确哪些内容仍需核实。

### 已有草稿的最终检查

```text
请使用 $draft-cs-rebuttal 检查这份 Rebuttal。
重点检查是否直接回答全部问题、证据是否支持结论、
回应与论文是否一致，以及是否有过度防御或不必要的认错。
指出必须修改的地方并提供替换文本。
英文正文总计不超过 500 词。
```

## 一个简短示例

以下是虚构示例，仅展示工作方式。

**审稿意见**：提升是否只来自更多参数？

**作者提供的已完成结果**：同一划分、骨干和训练设置，两个模型均为 2.0M 参数；三个种子的 NDCG@10 均值±标准差，本文为 0.240±0.003，扩宽基线为 0.230±0.004。作者确认会把结果加入 Table 5，但尚未修改论文。

**中文策略**：关键是提升来源。参数匹配结果支持“在该设置下，提升不只是参数数量增加带来的”，但不能据此声称计算量也完全相同，或内部机制已经被因果证明。

**英文回应示例**：

> Thank you for raising the question of model capacity. With 2.0M parameters each, our model achieves NDCG@10 of 0.240 ± 0.003, compared with 0.230 ± 0.004 for the widened baseline over three seeds. Both use the same data split, backbone, and training settings. This comparison supports a benefit beyond increasing parameter count under this setup. We will add these results to Table 5.

如果没有该实验，技能会建议参数匹配对照并提供待补证据的草稿，不会生成上面的数字。

## 其他安装方式

### 手动安装到 Codex 或 Claude Code

先克隆仓库：

```bash
git clone https://github.com/zhang-haichao/CS-Rebuttal-Skill.git
```

然后选择对应工具。下面命令适用于 macOS/Linux，并假设从仓库所在目录的上一级执行；目标技能目录应尚不存在：

```bash
# Codex：个人范围
mkdir -p ~/.agents/skills
cp -R CS-Rebuttal-Skill/skills/draft-cs-rebuttal ~/.agents/skills/
```

```bash
# Claude Code：个人范围
mkdir -p ~/.claude/skills
cp -R CS-Rebuttal-Skill/skills/draft-cs-rebuttal ~/.claude/skills/
```

仅对一个项目生效时，将技能文件夹复制到该项目的 `.agents/skills/`（Codex）或 `.claude/skills/`（Claude Code）。Windows 用户也可用文件管理器复制完整文件夹。

目录和调用方式依据 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills) 与 [Claude Code 官方技能文档](https://code.claude.com/docs/en/skills)。

### 在支持自定义技能的 ChatGPT 环境中使用

如果你的 ChatGPT 环境提供 `@skill-creator`，可以直接发送：

```text
请用 @skill-creator 安装这个仓库中的 draft-cs-rebuttal 技能：
https://github.com/zhang-haichao/CS-Rebuttal-Skill/tree/main/skills/draft-cs-rebuttal
```

也可以下载仓库，将 `skills/draft-cs-rebuttal` 文件夹作为安装材料交给技能创建工具。可用入口取决于账号及客户端；本地 CLI 安装不会自动安装到 ChatGPT 云端账号。

## 项目文件

| 文件 | 用途 |
|---|---|
| `skills/draft-cs-rebuttal/SKILL.md` | 触发条件、完整工作流、输出和终检规则 |
| `skills/draft-cs-rebuttal/references/response-patterns.md` | 八类常见意见的处理方法与例句 |
| `skills/draft-cs-rebuttal/references/evidence-and-experiments.md` | 证据检查、对照设计、实验优先级和结果更新 |
| `skills/draft-cs-rebuttal/agents/openai.yaml` | 支持该元数据的工具中的名称、介绍与默认提示 |
| `README.en.md` | 英文项目介绍与安装说明 |

## 设计原则

- **礼貌且有立场**：认可值得讨论的问题，允许有证据的不同意见。
- **证据优先**：数字、文献、实验完成状态和论文定位都应有出处。
- **关注决策相关问题**：把主要篇幅留给正确性、实验可信度和关键共同关切。
- **行动具体**：说明实际修改，不用空泛承诺代替当前证据。
- **保持适当结论**：结果有局限就限定范围，不掩盖影响主要结论的负向结果。

技能用于辅助作者分析、写作和检查。作者需核对最终事实及适用的会议要求；它不保证提分或录用。

## 致谢与许可证

工作流主要来自作者总结的计算机会议论文 Rebuttal 经验，并参考了 [TobiasLee/Rebuttal-Skill](https://github.com/TobiasLee/Rebuttal-Skill) 的问题拆分、实验排序和证据核对思路。这里的流程与例句经过独立整理，默认采用“中文策略分析＋英文回应”。

本项目使用 [MIT License](LICENSE)。欢迎提交 Issue 或 Pull Request，分享匿名化的意见类型、改进建议和文档修正。
