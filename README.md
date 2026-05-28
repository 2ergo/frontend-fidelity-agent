# FrontendFidelityAgent

高保真前端复原 Agent，用于在 Codex 或 Cursor 中从网址、截图、设计稿、PRD、草图、竞品页面或现有代码仓库出发，先澄清需求，再生成真实可滚动的布局交互确认稿，最后实现并验证前端页面。

## 适用场景

- 根据网页、截图、Figma、蓝湖、即时设计、PRD 或草图复原前端页面。
- 构建 Web、小程序或桌面应用前端。
- 在编码前确认页面结构、跳转关系、点击事件、滚动范围和业务边界。
- 避免只还原首屏，却遗漏页面下方内容、局部滚动、弹窗滚动、固定导航等细节。

## 支持范围

平台：

- Web
- 微信小程序 / 跨端小程序
- 桌面应用

技术栈：

- React
- Vue
- Next.js
- Vite
- 微信小程序原生
- Taro
- uni-app
- Electron
- Tauri

参考材料：

- 网址
- UI 截图
- Figma / 蓝湖 / 即时设计
- PRD
- 手绘草图
- 竞品页面
- 现有代码仓库

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

也可以直接描述任务：

```text
使用高保真前端复原 Agent，根据这个截图做一个 React 页面。
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
使用 FrontendFidelityAgent，根据这个 PRD 和截图实现页面。先生成布局交互确认稿，不要直接写正式页面。
```

## 工作流程

Agent 默认遵循以下流程：

1. 启动阶段一次只问一个问题，不把多个问题打包成清单。
2. 先确认目标端：Web、小程序或桌面应用。
3. 再单独确认技术栈：沿用现有项目，或选择 React、Vue、Next.js、Vite、微信小程序、Taro、uni-app、Electron、Tauri。
4. 只有用户说没有偏好，或现有仓库已经明确技术栈时，才推荐默认技术栈。
5. 分析参考材料：网址、截图、设计稿、PRD、草图、竞品页面或现有仓库。
6. 判断业务功能边界：登录、注册、权限、页面范围、数据来源、表单、状态和异常。
7. 分析页面结构：路由、模块、布局、响应式、交互、点击事件和滚动范围。
8. 只追问无法从材料中可靠判断、且会影响实现的关键信息。
9. 当用户需要设计探索、提供 Open Design 资料，或给了参考网站但只是想模仿风格而非一比一复制时，进入 Open Design 设计阶段。
10. 生成 `layout-confirmation.html` 低保真布局交互确认稿。
11. 等用户确认页面、跳转、点击事件和滚动范围。
12. 开始高保真实现。
13. 运行项目，截图检查，验证交互和滚动，继续修正。
14. 在生成或大幅修改的前端项目 README 中写明安装、启动、构建、预览、测试和环境配置方式。

## URL 参考还原规则

当用户提供 URL 作为视觉或交互参考时，Agent 应把它当成一个可交互产品，而不是静态截图。

如果是精确还原，应检查并尽量还原：

- 颜色、字体感觉、间距、圆角、阴影、信息密度和背景处理。
- 首屏、首屏以下内容、固定/吸顶区域、响应式变化和滚动容器。
- hover、active、focus、selected、disabled、loading、empty、error 等状态。
- 点击按钮、卡片、导航、菜单、Tab、筛选、弹窗、抽屉、下拉、分页、表单等交互。
- 动效节奏、hover 动效、展开/关闭动画、页面切换或轮播行为。
- 图片比例、图标风格、徽标、标签、截断和内容密度。

如果无法访问 URL 或无法检查交互状态，Agent 必须说明限制，并向用户索要截图、录屏或交互说明。不能在没有检查 hover/点击效果的情况下声称高保真。

## Open Design 设计阶段

Open Design 可以作为设计阶段工具，而不是替代最终前端实现。

适合使用 Open Design 的情况：

- 用户只有 PRD、想法或草图，还没有明确视觉设计。
- 用户希望先探索多个视觉方向。
- 用户提供了 Open Design 项目、`DESIGN.md`、设计系统或 artifact。
- 用户给了一个参考网站，但当前项目不是要一比一复制该网站，而是要模仿它的视觉风格。

当参考网站只是风格目标时，Agent 应该：

- 把参考网站当作视觉方向，而不是直接复刻对象。
- 提取风格特征，例如气质、信息密度、字体感觉、间距节奏、颜色使用、组件形态、阴影层级、动效、导航方式和内容层级。
- 确认哪些内容必须原创或不同，例如品牌、文案、页面结构、业务流程、数据模型和图片资产。
- 借鉴 Open Design 的设计规范、设计系统或样例生成合适的设计方向。
- 不复制受保护的品牌资产、Logo、专有插画、原文案或具有强识别度的商业外观，除非用户明确拥有权利并要求这样做。
- 仍然必须生成真实可滚动的 `layout-confirmation.html`，确认后再实现。

Open Design 导出的 HTML 不需要特殊对待，它和普通 HTML/网页参考一样处理。真正有额外价值的是 `DESIGN.md`、设计系统、craft rules、skill 样例、项目元数据或 artifact 说明。

## 布局交互确认稿

在正式实现前，Agent 会优先生成：

```text
layout-confirmation.html
```

它不是最终 UI，而是低保真确认稿，用简单方框展示：

- 页面布局
- 页面跳转
- 点击事件
- 弹窗、抽屉、Tab、菜单等状态
- 固定 Header / Sidebar / Tab / Bottom Bar
- 整页滚动、局部滚动、弹窗滚动、横向滚动
- 待确认问题

确认稿的关键规则：

```text
所有标记为可滚动的区域，都必须真的可以滚动。
```

也就是说，Agent 会用空白卡片、列表项、表格行或区块把滚动区域撑开，让用户可以实际验证：

- 鼠标滚动时到底哪个区域在动。
- Header 是否固定。
- Sidebar 是否独立滚动。
- 弹窗打开后背景是否还能滚动。
- 表格或标签栏是否横向滚动。
- 移动端是否符合预期。

## 业务边界确认

Agent 不只确认视觉布局，也会判断功能边界。

当项目涉及私有数据、个人中心、收藏、下单、内容发布、管理后台、审核、支付或个性化信息时，Agent 会确认：

- 是否需要登录。
- 是否需要注册、忘记密码、退出登录。
- 是否支持游客模式。
- 是否有角色权限。
- 未登录点击受保护功能时如何处理。
- 登录后头像、用户菜单、个人中心如何展示。

## 登录注册与接口规则

如果项目需要登录、注册、权限或受保护操作，Agent 会先确认是否已有真实接口。

如果已经有接口，Agent 应按接口文档接入，例如：

```text
POST /api/login
POST /api/register
GET /api/me
POST /api/logout
```

如果暂时没有接口，Agent 默认实现前端 mock 流程：

- 先做登录、注册、权限相关页面和交互。
- 留出可替换的接口层，例如 `authService`、`api/auth` 或项目已有 request 封装。
- 提供至少一个 mock 用户名和密码。
- 用户必须点击登录按钮并通过 mock 校验后，才进入登录态。
- 使用 localStorage、sessionStorage、组件状态或项目已有状态管理保存 mock 登录态。
- 实现退出登录、未登录访问受保护页面、用户菜单等前端行为。
- 在生成项目的 README 中写明 mock 账号、mock 存储方式、接口假设和未来真实接口接入点。

也就是说，Agent 不会假装已经有后端。没有接口时，它会先做可运行的前端 mock 版本，并把真实接口接入位置留好。

## 项目 README 规则

Agent 创建或大幅修改前端项目时，必须在该项目的 `README.md` 中写明如何运行。

至少包括：

- 项目用途和已实现范围。
- 技术栈。
- 环境要求，例如 Node.js、包管理器、小程序开发者工具、Electron/Tauri 依赖等。
- 安装依赖命令。
- 本地开发启动命令。
- 构建命令。
- 预览或生产启动命令。
- 测试、lint、typecheck 命令，如果项目提供。
- 必要的环境变量或配置文件。
- 小程序或桌面应用需要在哪个工具中打开。
- mock 数据、API 假设或暂未实现内容。
- 如果有 mock 登录，必须写明 mock 用户名、密码、登录态存储方式和后续真实接口接入位置。

如果项目已有 README，Agent 应保留有价值的原内容，并补齐缺失的启动说明。

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

```text
/FrontendFidelityAgent

我要根据这个竞品页面做一个后台管理系统首页。
请先分析页面结构、点击事件和滚动范围，生成 layout-confirmation.html 给我确认。
确认后再用 React + Vite 实现。
```

```text
使用 FrontendFidelityAgent，根据这个小程序截图复原页面。
需要确认哪些区域是页面滚动，哪些区域是 scroll-view。
```

```text
使用 FrontendFidelityAgent，把这个 PRD 做成 Electron 桌面应用原型。
先确认登录、设置页、侧边栏、主内容滚动和弹窗行为。
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
- 通过浏览器截图或人工验收反复修正。
