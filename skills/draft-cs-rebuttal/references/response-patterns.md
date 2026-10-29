# 常见意见的回应方法

将以下内容作为选择论证方式的参考。例句中的方括号是待用真实证据填写的位置；例句不代表实验已完成，也不默认作者承诺修改。

## 1. “提升是否只来自参数更多？”

- 将问题定位到提升来源和比较公平性，而非泛泛解释模块结构。
- 优先检查是否已有参数量相近的基线；必要时增加合理的扩宽／加深控制，报告参数、计算量及任务指标。参数匹配不等于计算量、训练预算全部匹配。
- 若对照只控制参数量，就只陈述排除了何种解释；不要据此断言内部机制已被因果证明。
- 没有对照结果时先给实验设计，不能说模块贡献已经被验证。

有已完成结果时可写：
> Thank you for raising the question of model capacity. With [parameter-matching procedure], [control] obtains [metric], compared with [metric] for our model. Both use [verified shared settings]. This comparison supports a benefit beyond increasing parameter count under this setup.

若作者确认补表，再增加相应修改句。

## 2. “没有考虑时间信息”等事实误解

- 查读原文对应机制，确认审稿人究竟指输入、结构还是评估过程；不要因为出现过关键词就认定误解。
- 用简短解释加准确定位纠正事实。原文确实不突出时建议补公式、交叉引用或一句说明；不自动承担并不存在的错误。

> Temporal information enters the model through [verified mechanism], which [brief explanation]. Section [verified location] describes this operation.

若作者已同意重写，再具体说明会在哪里强调其作用。不能只丢出章节号。

## 3. “与 X 类似，创新性不足”

- 找到 X 的原始论文并核对比较对象；链接不可读时请求相关段落或标记未核实。
- 先承认真实存在的共同技术背景，再选最关键的区别，不强行找一长串差异。
- 如有帮助，用紧凑表格梳理：比较维度／X 的做法／本文做法／差异的实际后果。维度可以是任务、约束、信息可用性、机制或保证。
- 解释“换任务”为什么需要技术变化；仅换数据集、改名或把已有模块拼接不能自动证明创新。
- 不主动认领没有依据的新贡献，也不把 reviewer 的 novelty 判断当作已成立结论。

> The connection to [X] is relevant: both methods use [shared element]. Our contribution addresses [specific unresolved requirement] through [mechanism]. Under [verified condition], this enables [supported capability], as shown by [evidence].

只有在证据确实支持时填写 capability；不要补上“首个”“完全不同”等未经检验的词。

## 4. “实验设置不公平／不清楚／缺少基线”

- 先查明究竟是描述缺失，还是实际协议有问题。逐项核对数据划分、预处理、可用信息、调参、训练预算和模型选择。
- 已公平但没写清楚：说明现有设置及出处，建议补细节。
- 确有不公平：承认具体问题，说明影响，使用修正后的对比；不要把错误称为单纯措辞问题。
- 不同实验使用不同 train/validation/test 划分时，不得直接跨表比较性能或用含糊措辞掩盖差异。重跑统一协议，或清楚标明各实验的适用范围。
- 没有代码不是任意排除强基线的理由。核实复现可行性与可比设置，说明真实限制和替代验证。

> The comparison uses [verified split], [selection procedure], and [budget conditions]. [Specific explanation resolving the concern].

若设置已修正，则写具体改变及其结果，不把上句当作未修正设置的辩解。

## 5. “只有约 1% 提升，价值不足”

- 先确认是相对百分比还是百分点，再核对方差、重复次数和评估一致性。
- 分开回答“提升可靠吗”和“提升有什么用途”。不要把任务竞争激烈当作充分证据。
- 用已验证的成本、延迟、内存、数据需求或适用范围解释价值；不能凭模块设计声称更可解释或更鲁棒。
- 若精度与效率之间存在权衡，直接给出两者，不把 trade-off 写成全面优越。

> Accuracy changes from [baseline] to [ours] under [protocol]. The practical benefit is [verified benefit with evidence], while [relevant trade-off].

统计证据不足时在中文分析中指出，必要时明确正文只报告观测结果，不使用 statistically significant。

## 6. “泛化、鲁棒性或可扩展性不足”

- 先分清跨数据集、跨分布、跨规模、扰动或部署延迟等不同问题。
- 让补充实验对应确切外推主张；不要把随机划分多跑几次写成跨域泛化。
- 将当前证据的范围说清楚；新增结果只有部分有效时，限定结论而不挑选有利子集。

> The current evaluation covers [verified conditions]. It supports [bounded conclusion]; performance under [unmeasured condition] has not yet been established.

只有缺口与问题直接相关时才加入限制句，避免在已解决的回答末尾附加无关自我削弱。

## 7. 无法补实验、要求超出范围或存在真实局限

- 说明对方建议与主张的关系，给出已有证据能回答的部分。
- “不适用”必须有技术原因；“没时间”不能证明方法正确。资源、数据或代码限制须由作者提供，不代编借口。
- 对重大正确性质疑，即使实验做不完，也必须指出当前未解决状态；不能包装成普通 future work。
- 对范围外的扩展，不卑不亢地说明设定；不承诺没有条件完成的工作。

> Our claim concerns [defined setting], where [supported explanation]. The requested extension would additionally require [verified requirement]. The present results therefore address [current scope].

## 8. 意见含糊、前后矛盾或语气不当

- 将技术内容与语气分开。给出最合理的解释；影响回应的歧义可用中文向作者说明。
- 评分与文字冲突时优先回应具体问题，不默认审稿流程不公，不催促改分。
- 只在作者要求时起草 AC 说明；以必要原话、具体事实和已核验规则为依据，不揣测身份或动机。

## 参考来源与采用范围

主要依据作者总结的 Rebuttal 经验与回应模板：礼貌沟通、识别疑虑、用证据回应、明确行动、处理创新性与实验质疑。

另参考 [TobiasLee/Rebuttal-Skill](https://github.com/TobiasLee/Rebuttal-Skill)（2026-10-29 阅读）的问题拆分、实验排序和证据核对思路。本文重新编写流程与例句，按作者偏好默认提供中文策略及英文草稿；不把外部模板中的结果、评分判断或通用政策表述作为事实。
