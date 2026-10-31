# character-scene-asset-prompts

**人物场景资产提示词**：把角色和场景的文字设想、或客户给的概念图，编译成可直接投喂图像模型的中文提示词。目标是"像真人实拍的影视资产"——脸不塑料，衣服有经历，场景有空气，多视图不换脸。

采用 [Agent Skills](https://agentskills.io) 开放格式：Claude Code、Codex 等支持该格式的 agent 可以直接安装；不支持技能的平台也能当系统提示词使用。

## 能做什么

| 任务 | 交付 |
| --- | --- |
| 角色概念设计 | 骨相、五官、妆发、服装逐层材质叙事的角色提示词，可切换结构化 JSON |
| 四栏角色设定卡（古装 / 现代） | 面部大特写 + 正面全身（去头）+ 侧面全身（去头）+ 背面全身，一张直出；脸只出现一次，从构图上防换脸、防全身照小脸出油；八至九头身 |
| 表情板 | 同一张脸的 6–8 格表情网格 |
| 道具设定卡 | 左侧大主图 + 右侧 2–3 格局部微距特写，写清部件和使用痕迹 |
| 场景概念图、空场景氛围图 | 前中后景分层、空气透视、环境侵蚀、光照时段 |
| 概念图写实化 | 先诊断参考图的 CG 感来源，再写"保留什么、改变什么"的编辑式提示词 |

只做静帧图像提示词，不做视频提示词、分镜、剧情或动作序列。本仓库只提供方法和提示词，不调用任何生成服务。

## 安装

仓库根目录就是技能目录（`SKILL.md` + `references/` + `templates/`）。克隆到所用 agent 的技能目录，文件夹名保持 `character-scene-asset-prompts`。

| Agent | 技能目录 |
| --- | --- |
| Claude Code | `~/.claude/skills/`（只给当前项目用：项目内 `.claude/skills/`） |
| Codex | `$CODEX_HOME/skills/`，默认 `~/.codex/skills/` |
| 其他支持 Agent Skills 的工具 | 各工具的 skills 目录，以其文档为准 |

Windows PowerShell（以 Claude Code 为例；Codex 把 `.claude` 换成 `.codex`）：

```powershell
git clone https://github.com/pencil102411-cell/character-scene-asset-prompts.git "$HOME\.claude\skills\character-scene-asset-prompts"
```

macOS / Linux：

```bash
git clone https://github.com/pencil102411-cell/character-scene-asset-prompts.git ~/.claude/skills/character-scene-asset-prompts
```

安装后新开一个会话生效。以后更新：进入该目录执行 `git pull`。

**不支持技能的平台**（ChatGPT 自定义 GPT、扣子 Coze、Dify 等）：把 `SKILL.md` 里第二个 `---` 之后的正文粘贴为系统提示词，`references/` 和 `templates/` 下的文件上传为知识库。

## 使用示例

直接描述需求即可自动触发。也可以显式调用：Claude Code 输入 `/character-scene-asset-prompts`，Codex 输入 `$character-scene-asset-prompts`。

```text
给古装剧女主沈知微做一张四栏定妆设定卡：22 岁，太傅嫡女，外表温婉、内里清醒，服装以月白和黛青为主，要古偶剧质感。
```

```text
做一个都市短剧男主的定妆设定卡：29 岁，集团继承人，冷淡克制，深色西装。
```

```text
给女侠做一张佩剑的道具设定卡：用了十年的旧剑，剑柄缠绳磨亮，剑鞘有磕痕。
```

```text
做一个蓝调晨雾山谷里的废弃山门空场景，仙侠风，2.39:1 宽银幕。
```

```text
（附图）客户给的这张海岛学堂 CG 游戏感太重，帮我写实化成真实航拍质感，构图和建筑布局不能动。
```

同一项目要连续出多个角色、场景时，可以让它在你的项目目录建一份 `资产项目看板.md`，记录已确认的风格锚点、面部参数和光照锚点，保证跨资产一致。

## 文件说明

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | 入口：适用范围、任务路由、核心原则、输出规则、自检 |
| [agents/openai.yaml](agents/openai.yaml) | Codex 显示名称与默认调用提示 |
| [references/角色设计.md](references/角色设计.md) | 面部参数库、服装材质叙事、面部与服装痕迹匹配 |
| [references/场景构建.md](references/场景构建.md) | 空间分层、空气透视、光照时空锚点、环境侵蚀 |
| [references/资产标准化.md](references/资产标准化.md) | 四栏设定卡规范、头身比、去头与跨栏一致性、分栏光照、古装与现代妆发服装参数、表情板、负面词清单 |
| [references/概念图写实化.md](references/概念图写实化.md) | 参考图诊断、光源是否重做、转换规则与案例 |
| [references/写实质感控制.md](references/写实质感控制.md) | 皮肤真实感组合、去油、光学瑕疵、真实与脏的分寸 |
| [references/材质叙事词典.md](references/材质叙事词典.md) | 时间、温度、湿度、使用痕迹与工艺词 |
| [references/风格美学锚点库.md](references/风格美学锚点库.md) | 实拍档 / 写真档、五个风格锚点与光影冷暖分离 |
| [references/结构化提示词框架.md](references/结构化提示词框架.md) | 结构化 JSON、四段镜头覆盖、双重构图、冷暖分离（写真档） |
| [templates/角色设定卡模板.md](templates/角色设定卡模板.md) | 古装女性 / 男性四栏设定卡（模板 A / B） |
| [templates/现代角色设定卡模板.md](templates/现代角色设定卡模板.md) | 现代女性 / 男性四栏设定卡（模板 C / D） |
| [templates/道具设定卡模板.md](templates/道具设定卡模板.md) | 道具设定卡（模板 E）：左主图 + 右侧特写 |
| [templates/写实转化提示词模板.md](templates/写实转化提示词模板.md) | 现状诊断 + 编辑式转化提示词 |
| [templates/项目看板模板.md](templates/项目看板模板.md) | 项目级视觉决策与实战观察记录 |

## 验证边界

提示词效果取决于具体模型和版本。规则里标注"实测"的内容，来自作者在 GPT-image 系模型上的出图验证；换用其他模型时先小批量测试。现代设定卡（模板 C / D）沿用古装模板测试过的排版、去头和身材写法；道具设定卡（模板 E）改版后还没有再次出图验证。本仓库不包含客户素材和出图结果。
