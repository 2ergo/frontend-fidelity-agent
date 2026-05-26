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

1. 确认目标端：Web、小程序或桌面应用。
2. 确认技术栈：沿用现有项目，或选择 React、Vue、Next.js、Vite、微信小程序、Taro、uni-app、Electron、Tauri。
3. 分析参考材料：网址、截图、设计稿、PRD、草图、竞品页面或现有仓库。
4. 判断业务功能边界：登录、注册、权限、页面范围、数据来源、表单、状态和异常。
5. 分析页面结构：路由、模块、布局、响应式、交互、点击事件和滚动范围。
6. 只追问无法从材料中可靠判断、且会影响实现的关键信息。
7. 生成 `layout-confirmation.html` 低保真布局交互确认稿。
8. 等用户确认页面、跳转、点击事件和滚动范围。
9. 开始高保真实现。
10. 运行项目，截图检查，验证交互和滚动，继续修正。

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
- 通过浏览器截图或人工验收反复修正。
