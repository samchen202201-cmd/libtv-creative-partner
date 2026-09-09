# LibTV 创作搭档

**把你的想法、剧本或现有素材，变成清楚、可修改的 LibTV 创作方案。**

LibTV Creative Partner 是一个面向 AI 视频创作者的编剧、导演与制作准备 Skill。它把故事意图整理成剧本、人物与场景资产、分镜、光影、运镜和可复制的生成 Prompt；剧本确定后，再交付一份从剧本到视频的完整 Markdown 制作指南。

版本变化见 [CHANGELOG.md](CHANGELOG.md)。

**剧本确定后，直接给你一份完整的 Markdown 制作指南。** 确认采用完整剧本后说“好，下一步”，即可一次拿到从剧本到视频的完整内容，不必逐项要求分镜、资产和 Prompt。你明确要求 Word／`.docx` 时，再按指定格式导出。

适合会操作 LibTV、希望有人一起想故事、设计镜头和准备提示词的创作者。不必懂齐全的电影术语，也不必每次从头走流程。

## 能帮你做什么

- **没有故事：**提供带题材特色的故事提案；已有剧本直接跳过。
- **需要剧本：**扩写想法、打磨人物与情节，或只改指定段落。
- **建立人物：**从已有剧本提取小传、关系与行为依据，整理能生成的外形、服装和表演特征；已有满意角色图继续沿用，不要求先填人物问卷。
- **准备画面：**设计分镜、表演、构图、光影、运镜和镜间衔接。
- **方便拼接：**将相邻镜头的动作、开场与收尾写进各自 Prompt，需要时补一句切点或声音衔接说明，不要求你填写额外表格，也不把每个镜头都变成花式转场。
- **准备素材：**整理角色、场景、道具与声音，说明已有参考怎么用、缺什么。
- **开始制作或返修：**给出可复制的 Prompt；从最新截图或反馈继续，保留满意部分。

默认质量优先；你提出预算或简化需求时，再讨论低成本做法。模板用于帮助创作，不要求你填表或持续汇报进度。

## 完整指南包含什么

确认版剧本、导演与视听设计、分镜表、全部必要角色／场景／道具／风格资产及生成 Prompt、逐镜关键帧和视频 Prompt、参考连接说明、音色与对白表演、音乐和音效安排，以及从资产准备、视频生成到剪辑混音和导出的制作说明，放进同一份 Markdown 文件。

视频默认不生成 BGM 和字幕，同时保留必要对白、环境声与动作音效；配乐独立准备并在后期加入。每镜按所选模型与 LibTV 实际入口交付可复制正文、必要字段和设置说明，按需支持英文，不把某种负向语法套到所有模型。详见 [Prompt 模块](references/prompts-revisions.md#视频声音字幕与模型适配)。

仅选择故事方向时先写剧本；你明确只要局部内容或指定其他格式时，按你的要求交付。默认格式为 Markdown；用户明确要求 Word／`.docx` 时才调用文档生成器。环境确实缺少文件写入条件时，直接在聊天中交付完整正文，并说明实际保存状态。详见 [格式选择](references/complete-word-guide.md#format-selection)。

默认指南采用紧凑开头、分类资产、全片时间轴和逐镜 Prompt 区块；保留确认剧本全文，不套固定镜头数或页数。Markdown 先保证内容完整、可复制和可继续修改；用户明确要求 Word 时，再使用包内模板与生成器排版，详见 [生成说明](references/word-builder.md)。

指南开篇会提示：**可以在支持生图的环境中，用一条指令启动静态视觉资产生成。** 收到指南后，直接说“按指南生成全部视觉资产，包括首帧和需要的尾帧图”，或只指定角色、场景、道具、风格参考或某个镜号；新开任务时附上指南。首帧和目标尾帧分别保存为独立图片，注明镜号／生成片段与参考用途。先复用或准备人物、场景等共用参考，再生成依赖它们的帧图，不需逐张确认。这里的“一键”指一条指令启动，不是立即完成；生图需要等待并消耗当前环境的使用额度，音频与视频另行制作。指南本身照常先交付，不自动启动生成。

首尾帧按实际镜头需要准备，不强制每镜绑定；概念图不自动锁定视频开场。图片职责、复用和参考输入方法统一见 [资产模块](references/assets-sound.md)。

交付指南后，聊天里会附作品与计划时长、镜头／资产概览和下一步可复制指令。只显示文件中真实已有的信息，展示指令本身不自动启动生图。

## 安装与调用

以下命令以 macOS / Linux 终端为例。先取得完整的 `libtv-creative-partner` 文件夹，确认其中有 `SKILL.md` 和配套文件。

| 环境 | 安装位置 | 调用方式 |
|---|---|---|
| Codex | `${CODEX_HOME:-$HOME/.codex}/skills/` | 下一轮对话中使用 `$libtv-creative-partner` |
| Claude Code / Claude Desktop | `~/.claude/skills/` | 描述任务时自动触发，或明确点名 Skill |
| 其他 Agent | 宿主环境的 skills 目录 | 手动加载 `SKILL.md` |

不同宿主对自动触发的实现可能不同；明确点名 Skill 是最稳定的调用方式。

### Codex 安装

在 `libtv-creative-partner` 文件夹的**上一级目录**打开终端，执行：

```sh
src="./libtv-creative-partner"
dest="${CODEX_HOME:-$HOME/.codex}/skills/libtv-creative-partner"

if [ ! -f "$src/SKILL.md" ]; then
  printf '%s\n' '请先进入包含 libtv-creative-partner 文件夹的目录。'
elif [ -e "$dest" ] || [ -L "$dest" ]; then
  printf '%s\n' '目标已存在，本次不覆盖。请先检查已安装版本。'
else
  mkdir -p "$(dirname "$dest")" && cp -R "$src" "$dest"
fi
```

安装位置为 `$CODEX_HOME/skills`，未设置时使用 `~/.codex/skills`。复制后，在 Codex 的下一轮对话中用 `$libtv-creative-partner` 调用。若未识别，先核对目标文件夹里是否直接包含 `SKILL.md`，而不是又套了一层文件夹。

### Claude Code / Claude Desktop 安装

将完整的 `libtv-creative-partner` 文件夹复制到 `~/.claude/skills/`：

```sh
src="./libtv-creative-partner"
dest="$HOME/.claude/skills/libtv-creative-partner"

if [ ! -f "$src/SKILL.md" ]; then
  printf '%s\n' '请先进入包含 libtv-creative-partner 文件夹的目录。'
elif [ -e "$dest" ] || [ -L "$dest" ]; then
  printf '%s\n' '目标已存在，本次不覆盖。请先检查已安装版本。'
else
  mkdir -p "$(dirname "$dest")" && cp -R "$src" "$dest"
fi
```

在 Claude 中可以直接描述需求，也可以明确写出 `libtv-creative-partner`。具体自动触发行为以当前 Claude 宿主版本为准。

## 直接这样开始

按示例附上剧本、图片或原 Prompt 即可：

```text
$libtv-creative-partner 就用这版完整剧本，下一步。请交付从剧本到视频制作的完整 Markdown 指南，所有必要资产和逐镜 Prompt 放在同一个文件里。
```

```text
$libtv-creative-partner 我带来了剧本，请保留剧情，帮我做分镜表和对应的视频 Prompt。
```

```text
$libtv-creative-partner 我没有故事方向，想做一部轻松有趣的短片。请给我三个不同题材的提案，并推荐一个。
```

```text
$libtv-creative-partner 这是我选定的角色图和场景图。请帮我设计一段人物走进房间、发现异常的镜头，并给出可复制的 Prompt。
```

```text
$libtv-creative-partner 这个镜头的人物和光线都满意，只是伸手动作太快。请根据原 Prompt 调整动作节奏，保留其他设计。
```

## 使用边界

本 Skill 提供创作文本、参考准备与制作说明，**不自动生成图片、视频或音频**，也不自动上传素材、改动画布、付费或发布。普通创作不需要先登录 LibTV 或安装 CLI；实际平台操作另行确认，具体设置以当前平台与目标模型为准。

方案和 Prompt 是创作建议，不代表素材已经生成或效果已经验证。你可以直接提出不同意见，我们围绕具体问题继续修改。

## 许可与参考资料

本项目自有文本、脚本与工具代码按 [MIT License](LICENSE) 发布。README 末尾列出的外部参考资料保留原作者与原许可证署名；参考方法经过独立改写，未打包外部项目的代码、私有素材或完整正文。

## 编导与镜间衔接方法参考

本版参考下列公开资料中的通用导演与连续性方法，按本 Skill 的轻量协作方式独立编写说明与示例；没有打包其代码、模型参数表或生成服务，也不要求用户安装这些项目：

- [DirectorSKILL 的 Editing and Assembly](https://github.com/wuwangzhang1216/DirectorSKILL/blob/main/references/editing-and-assembly.md)，作者 wangzhang-wu：前后构图配对、切镜动机与可剪过程。
- [visual-skills 的 Fixes and Skeletons](https://github.com/smixs/visual-skills/blob/main/video/references/fixes-and-skeletons.md)，作者 Serge Shima，原文标注 CC BY 4.0：分段 Prompt 与一句话衔接说明。本文保留来源署名，未照搬其模型专用写法。
- [xyz-video-skill](https://github.com/huangserva/xyz-video-skill/blob/refactor/video-creator/SKILL.md)：区分适合续接的连续片段与应另做首帧的换场、反打、跳时，不采用其中的自动化字段或效果保证。

增量编导方法参考：

- DirectorSKILL 的 [Blocking and Staging](https://github.com/wuwangzhang1216/DirectorSKILL/blob/main/references/blocking-and-staging.md) 与 [Cinematic Language](https://github.com/wuwangzhang1216/DirectorSKILL/blob/main/references/cinematic-language.md)，作者 wangzhang-wu：参考关系调度与观看距离的选择方法，独立改写为现有分镜模块的短说明和同场景取舍示例，不引入其岗位体系或固定覆盖数量。
- NolanX 的 [Director Visual Language](https://github.com/nolanx-ai/nolanx.ai/blob/main/skills/director-visual-language/SKILL.md)：参考把视觉意图落实到构图、受光与运动结果的方法，不引入平台运行栈、固定时长或未经核实的生成参数。

光影方法参考：

- [Hell-Grind-AIGC-Skill 的灯光、色彩、材质与天气](https://github.com/renmu2017/Hell-Grind-AIGC-Skill/blob/main/skill/hell-grind-aigc-skill/references/lighting-color-material.md)，作者 renmu2017，仓库标注 [MIT](https://github.com/renmu2017/Hell-Grind-AIGC-Skill/blob/main/LICENSE)：参考曝光取舍、材质响应与事件互动光的思路，按现有分镜、资产和 Prompt 分工自行编写；未复制其正文、示例、表格或检查清单，不引入五层必填表、色彩比例和质量门。
- [ARRI 的 Native Soft Light](https://www.arri.com/en/lighting/led-panel-lights/skypanel-classic/native-soft-light)：用于核对柔光、阴影边缘与光输出的区别，不将灯具规格或控制功能当成生成模型的参数。

这些是制作方法参考，不构成生成效果保证，也不要求安装外部 Skill 或购置摄影器材。
