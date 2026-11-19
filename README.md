# Schedule Dashboard Web Builder

一个用于构建排期、专家拜访、会议管理和运营工作台网页的 Codex skill。

它把信息架构、数据建模、CSS 主题系统、响应式布局、交互设计和浏览器验证串成一套可复用的方法，适合制作信息密集但易于扫描的业务看板。

## 能做什么

- 将排期、场次、专家、机构、业务线和状态整理成数据驱动的界面
- 搭建顶部栏、日期导航、筛选区、统计区、卡片网格、速览表和详情抽屉
- 使用 CSS 变量建立可维护的科技蓝或其他主题系统
- 实现搜索、日期切换、业务线筛选、状态更新、备注持久化和复制动作
- 检查键盘操作、焦点状态、文字对比度、响应式布局和实际浏览器渲染
- 排查静态网页无法打开、`file://` 加载限制、端口未监听和 CDN 资源失败

## 安装

### 安装到 Codex

Codex 会读取个人目录下的 `SKILL.md`。Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills" | Out-Null
git clone https://github.com/kylokuo/schedule-dashboard-web-builder.git `
  "$env:USERPROFILE\.codex\skills\schedule-dashboard-web-builder"
```

macOS/Linux：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/kylokuo/schedule-dashboard-web-builder.git \
  ~/.codex/skills/schedule-dashboard-web-builder
```

重新打开 Codex 或新建会话后，可以显式调用：

```text
$schedule-dashboard-web-builder
```

### 安装到 Claude Code

Claude Code 会读取个人目录下的 `~/.claude/skills/<skill-name>/SKILL.md`。Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
git clone https://github.com/kylokuo/schedule-dashboard-web-builder.git `
  "$env:USERPROFILE\.claude\skills\schedule-dashboard-web-builder"
```

macOS/Linux：

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/kylokuo/schedule-dashboard-web-builder.git \
  ~/.claude/skills/schedule-dashboard-web-builder
```

重新启动 Claude Code 或开启新会话后，可以使用：

```text
/schedule-dashboard-web-builder
```

也可以直接描述要制作的网页，让 Claude Code 根据 skill 自动判断是否使用它。仓库中的 `SKILL.md` 同时适用于 Codex 和 Claude Code；`agents/openai.yaml` 只提供 Codex 的界面元数据，Claude Code 不依赖该文件。

### 更新已安装的 skill

如果目录已经存在，不要再次执行 `git clone`，进入对应目录拉取更新即可：

Windows PowerShell 只运行你实际安装的客户端对应命令：

```powershell
git -C "$env:USERPROFILE\.codex\skills\schedule-dashboard-web-builder" pull
git -C "$env:USERPROFILE\.claude\skills\schedule-dashboard-web-builder" pull
```

macOS/Linux 只运行你实际安装的客户端对应命令：

```bash
git -C ~/.codex/skills/schedule-dashboard-web-builder pull
git -C ~/.claude/skills/schedule-dashboard-web-builder pull
```

skill 本身不包含运行时依赖；它会优先沿用目标项目已有的框架和工具链。

## 使用

显式调用：

```text
$schedule-dashboard-web-builder
```

也可以直接描述需求，例如：

> 制作一个 4 天会议专家拜访排期看板，需要日期切换、业务方向筛选、专家卡片、详情抽屉和移动端布局。

skill 默认允许自动触发，适合以下请求：

- 制作会议排期或活动管理网页
- 制作专家、客户或机构拜访看板
- 制作带筛选、状态和详情流程的运营工作台
- 将一组业务数据整理成可操作的内部 dashboard

营销落地页、纯展示海报、通用博客和复杂后端系统不属于这个 skill 的主要范围。

## 方法概览

1. 读取项目约定，确认入口、数据源、样式入口和运行方式。
2. 先定义日期、场次、实体、状态和分组等数据模型，再写渲染层。
3. 搭建“顶部栏 + 日期/筛选栏 + 主看板”的工作台骨架。
4. 用语义化 CSS 变量统一 shell、board、surface、ink、muted、line、accent 和状态色。
5. 为桌面端和窄屏端分别验证信息密度、文字换行和横向滚动区域。
6. 通过 HTTP 请求和真实浏览器渲染验证页面，而不是只确认开发命令已启动。

默认推荐的科技蓝基础色：

| 用途 | 颜色 |
| --- | --- |
| 深色侧栏 | `#0A1F3D` |
| 深色看板 | `#12345B` |
| 卡片背景 | `#F5F9FF` |
| 卡片文字 | `#102744` |
| 辅助文字 | `#526A84` |
| 边框 | `#C9D9EA` |
| 强调色 | `#1769D1` |

强调色用于选中态、进度、重点和操作反馈；绿色、琥珀色保留给完成和警告等语义状态。普通文字应达到至少 `4.5:1` 的对比度。

## 本地预览

目标项目没有构建脚本时，可以在项目目录运行：

```powershell
npx --yes http-server . -p 4173 -c-1
```

然后打开 <http://127.0.0.1:4173/>。不要直接双击依赖 JSX 子脚本的 `index.html`；`file://` 环境可能阻止脚本加载。

## 文件

```text
SKILL.md              # Codex 执行规则
agents/openai.yaml    # UI 元数据和自动触发配置
LICENSE               # MIT License
```

## 许可证

[MIT License](./LICENSE)
