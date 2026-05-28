# FrontendFidelityAgent

高保真 Web 前端复原 Agent，用于在 Codex 或 Cursor 中从网址、截图、设计稿、PRD、草图、竞品页面或现有代码仓库出发，先澄清需求，再选择合适的生成/实现模式，最后实现并验证前端页面。

## 适用场景

- 根据网页、截图、Figma、蓝湖、即时设计、PRD 或草图复原 Web 前端页面。
- 完整克隆一个用户有权复刻的网站。
- 根据截图、mockup 或 Figma 设计生成 React/Vue 页面。
- 模仿参考网站的视觉风格，但不一比一复制。
- 在编码前确认页面结构、跳转关系、点击事件、滚动范围和业务边界。

## 支持范围

平台：

- Web

常规技术栈：

- React
- Vue
- Next.js
- Vite

特殊模式：

- 完整网站克隆：`JCodesMore/ai-website-cloner-template`
- 截图/Mockup/Figma 生成：`abi/screenshot-to-code`
- 风格探索：Open Design 设计阶段

## Codex 使用方式

将本仓库作为 Codex Skill 安装到 Codex skills 目录：

```text
~/.codex/skills/frontend-fidelity-agent
```

Windows 示例：

```text
C:\Users\<your-name>\.codex\skills\frontend-fidelity-agent
```

安装后，可以在 Codex 中这样触发：

```text
/FrontendFidelityAgent
```

或：

```text
使用 FrontendFidelityAgent 帮我复原这个页面
```

## Cursor 使用方式

把 Cursor 规则文件复制到目标项目：

```text
cursor/.cursor/rules/frontend-fidelity-agent.mdc
```

目标位置：

```text
<your-project>/.cursor/rules/frontend-fidelity-agent.mdc
```

然后在 Cursor 中描述任务，例如：

```text
使用 FrontendFidelityAgent，根据这个 PRD 和截图实现页面。先确认技术栈和交互，不要直接写正式页面。
```

## 工作流程

Agent 默认遵循以下流程：

1. 启动阶段一次只问一个问题。
2. 先确认目标是 Web 前端。
3. 第二个问题必须询问参考类型：URL、mockup、Figma 设计、截图，还是 PRD。
4. 如果参考类型是 URL：
   - 用户要完整复刻整个网站时，进入“网站完整克隆模式”，跳过技术栈选择。
   - 非完整克隆的 URL 生成/还原只支持 React。
5. 如果用户给的是截图、mockup、Figma 设计、UI 图片或静态设计导出，进入“截图设计稿生成模式”，要求用户指定 React 还是 Vue。
6. 如果用户给的是 PRD，再单独确认技术栈：沿用现有项目，或选择 React、Vue、Next.js、Vite。
7. 只有用户说没有偏好，或现有仓库已经明确技术栈时，才推荐默认技术栈。
8. 分析参考材料、业务边界、页面结构、路由、交互、状态、响应式和滚动范围。
9. 只追问无法从材料中可靠判断、且会影响实现的关键信息。
10. 当用户需要设计探索、提供 Open Design 资料，或给了参考网站但只是想模仿风格而非一比一复制时，进入 Open Design 设计阶段。
11. 非完整克隆模式下，必要时生成 `layout-confirmation.html` 低保真布局交互确认稿。
12. 等用户确认页面、跳转、点击事件和滚动范围。
13. 开始实现、运行项目、截图检查、验证交互和滚动，并继续修正。
14. 在生成或大幅修改的前端项目 README 中写明安装、启动、构建、预览、测试和环境配置方式。

## 网站完整克隆模式

当用户给出一个或多个 URL，并明确表示要“完整复制 / 完整复刻 / 克隆整个网站 / 复制所有页面路由和点击效果”时，Agent 必须进入网站完整克隆模式。

强制使用：

```text
JCodesMore/ai-website-cloner-template
```

仓库地址：

```text
https://github.com/JCodesMore/ai-website-cloner-template.git
```

强制技术栈：

- Next.js
- React
- TypeScript
- Tailwind
- shadcn/ui

推荐流程：

```text
git clone https://github.com/JCodesMore/ai-website-cloner-template.git <project-name>
cd <project-name>
npm install
/clone-website <target-url>
```

如果当前 Codex 环境不能直接调用 `/clone-website`，Agent 应读取并遵循该模板中的 `AGENTS.md` 和 `.codex/skills/clone-website/SKILL.md`，而不是用普通方式粗略实现。

这个模式只用于完整复刻。  
如果用户只是想“模仿某个网站风格”，不要使用完整克隆模式，应进入 Open Design 设计阶段。

## 截图设计稿生成模式

当用户指定的主要参考是：

- 截图
- mockup
- Figma 设计
- UI 图片
- 静态设计导出

Agent 必须进入截图设计稿生成模式。

强制使用：

```text
abi/screenshot-to-code
```

仓库地址：

```text
https://github.com/abi/screenshot-to-code
```

在开始生成前，Agent 必须先问用户：

```text
你希望使用 React 还是 Vue？
```

然后按用户选择使用：

- React + Tailwind
- Vue + Tailwind

注意：

- 不允许在这个模式下默认 React 或 Vue。
- screenshot-to-code 生成结果只作为第一版实现，不等于最终验收。
- 后续仍然要检查滚动范围、响应式、点击事件、状态、README、mock/API 等。
- 如果截图、mockup 或 Figma 没有体现 hover、点击、active 等状态，Agent 必须向用户确认，或明确写出假设。

## URL 参考还原规则

当用户提供 URL 作为视觉或交互参考时，Agent 应把它当成一个可交互产品，而不是静态截图。

非完整克隆的 URL 生成/还原当前只支持 React。  
如果用户要求完整复制整个网站，则进入“网站完整克隆模式”，使用固定的 Next.js + React + TypeScript + Tailwind + shadcn/ui 模板。

如果是精确还原，应检查并尽量还原：

- 颜色、字体感觉、间距、圆角、阴影、信息密度和背景处理。
- 首屏、首屏以下内容、固定/吸顶区域、响应式变化和滚动容器。
- hover、active、focus、selected、disabled、loading、empty、error 等状态。
- 点击按钮、卡片、导航、菜单、Tab、筛选、弹窗、抽屉、下拉、分页、表单等交互。
- 动效节奏、hover 动效、展开/关闭动画、页面切换或轮播行为。

如果无法访问 URL 或无法检查交互状态，Agent 必须说明限制，并向用户索要截图、录屏或交互说明。

## Open Design 设计阶段

Open Design 作为设计阶段工具，而不是替代最终前端实现。

适合使用 Open Design 的情况：

- 用户只有 PRD、想法或草图，还没有明确视觉设计。
- 用户希望先探索多个视觉方向。
- 用户提供了 Open Design 项目、`DESIGN.md`、设计系统或 artifact。
- 用户给了一个参考网站，但当前项目不是要一比一复制该网站，而是要模仿它的视觉风格。

当参考网站只是风格目标时，Agent 应提取风格特征，并确认哪些内容必须原创或不同，例如品牌、文案、页面结构、业务流程、数据模型和图片资产。

## 布局交互确认稿

在普通高保真实现前，Agent 可以生成：

```text
layout-confirmation.html
```

它不是最终 UI，而是低保真确认稿，用简单方框展示页面布局、跳转、点击事件、弹窗、抽屉、Tab、菜单、固定区域和滚动范围。

关键规则：

```text
所有标记为可滚动的区域，都必须真的可以滚动。
```

## 登录注册与接口规则

如果项目需要登录、注册、权限或受保护操作，Agent 会先确认是否已有真实接口。

如果暂时没有接口，Agent 默认实现前端 mock 流程：

- 先做登录、注册、权限相关页面和交互。
- 留出可替换的接口层，例如 `authService`、`api/auth` 或项目已有 request 封装。
- 提供至少一个 mock 用户名和密码。
- 用户必须点击登录按钮并通过 mock 校验后，才进入登录态。
- 使用 localStorage、sessionStorage、组件状态或项目已有状态管理保存 mock 登录态。
- 在生成项目的 README 中写明 mock 账号、mock 存储方式、接口假设和未来真实接口接入点。

## 项目 README 规则

Agent 创建或大幅修改前端项目时，必须在该项目的 `README.md` 中写明如何运行。

至少包括：

- 项目用途和已实现范围。
- 技术栈。
- 环境要求，例如 Node.js、包管理器等。
- 安装依赖命令。
- 本地开发启动命令。
- 构建命令。
- 预览或生产启动命令。
- 测试、lint、typecheck 命令，如果项目提供。
- 必要的环境变量或配置文件。
- mock 数据、API 假设或暂未实现内容。
- 如果有 mock 登录，必须写明 mock 用户名、密码、登录态存储方式和后续真实接口接入位置。

## 文件结构

```text
frontend-fidelity-agent/
  SKILL.md
  agents/
    openai.yaml
  assets/
    layout-confirmation-template.html
  cursor/
    .cursor/
      rules/
        frontend-fidelity-agent.mdc
  references/
    acceptance-checklist.md
    interaction-checklist.md
    layout-confirmation-spec.md
    requirement-flow.md
    scroll-behavior-checklist.md
```

## 示例任务

完整网站克隆：

```text
/FrontendFidelityAgent

我要完整复刻这个网站，包括所有页面路由、hover、点击效果和滚动效果：
https://example.com
```

截图设计稿生成：

```text
/FrontendFidelityAgent

根据这张 mockup 生成一个页面。请先问我要用 React 还是 Vue。
```

风格借鉴：

```text
/FrontendFidelityAgent

我要做一个后台首页，参考 https://open-design.ai/ 的风格，但不要一比一复制。
```

## 验收标准

最终实现应尽量满足：

- 视觉布局尽量像素级接近。
- 字体、间距、颜色、圆角、阴影、响应式一致。
- 所有可见交互可用。
- hover、active、loading、empty、error、disabled 等状态完整。
- 动效节奏接近参考。
- 滚动范围和 fixed/sticky 行为符合确认稿。
- 项目 README 清楚说明如何安装、启动、构建和预览。
