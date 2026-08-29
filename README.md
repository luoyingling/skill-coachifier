# Skill Coachifier

把任意既有 AI Skill 改造成**三模式**版本——让一个技能从"只给答案的引擎"变成"边做事边训练判断力的教练"。

当你想在**使用某个技能的过程中同时训练自己的判断力**时，用这个 Skill 给目标技能附加一层"教练协议"。

## 这是什么

Skill Coachifier 本身不产生内容，它是一个**改造器**：输入一个目标技能，输出一份"三模式技能协议"（可直接追加回目标技能的 SKILL.md，或作为独立提示词使用）。

改造前后对比：

| | 改造前 | 改造后 |
|---|---|---|
| 快速模式 | ✅ 原始能力 | ✅ 原始能力，完全保留 |
| light-coach | ❌ | ✅ 边做边练：输出时暴露每个关键判断的 why，需你定夺处提问并给判断依据引导 |
| full-coach | ❌ | ✅ 专项训练：出题 → 作答 → 揭示 → 复盘 → 评分 五步闭环 |

## 三模式说明

- **快速模式**：完全保留目标技能原始行为，用户说"快速"或直接要结果时生效。
- **light-coach（默认）**：高频、低强度。每次任务输出时，在每个关键判断点标注「决定 + why（依据出处）+ 你可复核」；在需要你输入信息才能定夺的地方明确提问，并告诉你"你可以基于 ____ 来判断"。每个任务最多 2–3 个必答问题，不打断工作流。
- **full-coach**：低频、高强度。用户说"训练我 / full"时触发，按"先猜后答"五步闭环做专项训练，评分并记录到 `训练记录.md`。

## 工作流（四步）

1. **第 0 步 完整分析目标技能**（前置门槛）：完整读取目标技能的 SKILL.md / references / scripts / assets，产出「能力边界 + 工作流程 + 隐含判断点清单」，经用户确认后才继续。
2. **第 1 步 挖掘判断关卡地图**：把 AI 替用户做决定的每个环节提取为判断关卡（通常 5–10 个）。
3. **第 2 步 附加 light-coach 协议**：暴露 why + 引导式提问。
4. **第 3 步 附加 full-coach 协议**：五步闭环 + 评分卡。

关键纪律：判断点必须来自目标技能实际内容，**禁止编造目标技能不存在的功能**；保留目标技能全部原有能力，只做附加层。

## 安装

克隆或下载本仓库后，把 `skill-coachifier` 目录放到你所用 AI 的 skills 目录：

- **OpenAI Codex**
  ```bash
  git clone https://github.com/luoyingling/skill-coachifier
  # 将 skill-coachifier 目录复制（或软链）到：
  ~/.agents/skills/skill-coachifier
  ```
- **Claude Code**
  ```bash
  ~/.claude/skills/skill-coachifier
  ```
- **豆包 / 其他支持 skill 的 AI**
  复制到其 skills 目录，或参考对应平台的 skill 安装方式。

## 使用方法

对任意一个你已安装的技能说类似的话：

> 用 skill-coachifier 给「XX技能」加上训练模式，我要 light-coach。

它会把该技能改造成三模式版本。使用改造后的技能时：

- 默认进入 **light-coach**（边做边练）；
- 说 **"训练我 / full"** 进入专项训练模式；
- 说 **"快速"** 恢复原始模式。

## 仓库结构

```
skill-coachifier/
├── SKILL.md                    # 主协议（frontmatter + 工作流）
├── README.md                   # 本文件
├── LICENSE                     # MIT
└── references/
    ├── analysis-method.md      # 第 0 步：技能完整能力与工作流分析
    ├── judgment-map.md         # 第 1 步：判断关卡地图模板
    ├── light-coach-protocol.md # 第 2 步：light-coach 协议
    └── full-coach-protocol.md  # 第 3 步：full-coach 协议
```

## 设计理念

判断力不是"听答案"练出来的，是"先自己判断、再对答案"练出来的。light-coach 让每一次正常使用都变成一次低成本的判断练习（暴露 why + 引导依据），full-coach 让薄弱关卡得到高强度专项训练。二者共同点：**技能包覆盖不到的、必须靠你上下文输入的地方，才是真正需要你判断力的地方。**

## License

[MIT](LICENSE) © 2026 luoyingling

## 维护声明

个人项目，按现状（as-is）提供，不承诺持续维护。欢迎 fork 与改进。
