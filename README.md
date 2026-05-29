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
- PRD 生成前端项目：`JCodesMore/ai-website-cloner-template` + Open Design
- 风格探索：Open Design 设计阶段

## Codex 使用方式

### 安装到 Codex

将本仓库作为 Codex Skill 安装到 Codex skills 目录：

```text
~/.codex/skills/frontend-fidelity-agent
```

Windows 示例：

```text
C:\Users\<your-name>\.codex\skills\frontend-fidelity-agent
```

如果已经把本仓库克隆到本地，可以直接复制整个仓库目录到上面的 skills 目录。Windows 示例：

```powershell
Copy-Item -Path "C:\path\to\frontend-fidelity-agent\*" -Destination "C:\Users\<your-name>\.codex\skills\frontend-fidelity-agent" -Recurse -Force
```

### 在新项目中使用

新建或打开任意前端项目后，在 Codex 中进入该项目目录，然后输入：

```text
/FrontendFidelityAgent
```

也可以用自然语言触发：

```text
使用 FrontendFidelityAgent 帮我复原这个页面
```

Agent 会先按顺序提问：

1. 先确认目标是否是 Web 前端。
2. 再询问参考类型：URL、mockup、Figma 设计、截图，还是 PRD。
3. 根据参考类型自动进入对应模式。

常用示例：

```text
/FrontendFidelityAgent

我要 1:1 复刻这个网站，包括所有页面路由、hover、点击、滚动和动效：
https://example.com
```

```text
/FrontendFidelityAgent

我有一张 mockup，请先问我要用 React 还是 Vue，然后生成前端项目。
```

```text
/FrontendFidelityAgent

这是一个 PRD，请使用 PRD + OpenDesign 模式生成前端项目，并输出 docs/prd-coverage.md。
```

注意：

- 不需要每次新建项目都重新创建 Agent；只要 Codex skills 目录里已安装 `frontend-fidelity-agent`，在任何项目里都可以调用。
- 如果更新了本仓库规则，需要重新复制到 Codex skills 目录，或重新安装该 Skill。
- URL 1:1 复刻会先输出全页侦察结果和 `motion-spec` 动效确认，不会直接开始最终实现。

## Cursor 使用方式

### 安装到 Cursor 项目

把本仓库中的 Cursor 规则文件复制到目标项目：

```text
cursor/.cursor/rules/frontend-fidelity-agent.mdc
```

目标位置：

```text
<your-project>/.cursor/rules/frontend-fidelity-agent.mdc
```

Windows 示例：

```powershell
New-Item -ItemType Directory -Force -Path "C:\path\to\your-project\.cursor\rules"
Copy-Item -Path "C:\path\to\frontend-fidelity-agent\cursor\.cursor\rules\frontend-fidelity-agent.mdc" -Destination "C:\path\to\your-project\.cursor\rules\frontend-fidelity-agent.mdc" -Force
```

### 在 Cursor 中使用

打开目标项目后，在 Cursor Chat / Agent 中直接说明要使用该规则，例如：

```text
请按 FrontendFidelityAgent 规则帮我复原这个页面。
```

或：

```text
使用 FrontendFidelityAgent 流程，先确认平台和参考类型，再根据我的 URL 做 1:1 复刻。
```

Cursor 会根据 `.cursor/rules/frontend-fidelity-agent.mdc` 中的规则约束当前项目。建议每个需要使用该 Agent 的 Cursor 项目都复制一份规则文件。

注意：

- Cursor 中不是通过 `/FrontendFidelityAgent` 命令触发，而是通过项目内 `.cursor/rules` 规则影响 Agent 行为。
- 如果规则更新了，需要把新的 `frontend-fidelity-agent.mdc` 再复制到目标项目。
- URL 1:1 复刻同样需要先做 Full Page Reconnaissance 和 `motion-spec` 动效确认。

## 工作流程

Agent 默认遵循以下流程：

1. 启动阶段一次只问一个问题。
2. 先确认目标是 Web 前端。
3. 第二个问题必须询问参考类型：URL、mockup、Figma 设计、截图，还是 PRD。
4. 如果参考类型是 URL：
   - 用户要完整复刻整个网站时，进入“网站完整克隆模式”，跳过技术栈选择。
   - 非完整克隆的 URL 生成/还原只支持 React。
5. 如果用户给的是截图、mockup、Figma 设计、UI 图片或静态设计导出，进入“截图设计稿生成模式”，要求用户指定 React 还是 Vue。
6. 如果用户给的是 PRD，进入“PRD + OpenDesign 生成模式”，跳过技术栈选择。
7. 只有用户说没有偏好，或现有仓库已经明确技术栈时，才在普通模式中推荐默认技术栈。
8. 分析参考材料、业务边界、页面结构、路由、交互、状态、响应式和滚动范围。
9. 只追问无法从材料中可靠判断、且会影响实现的关键信息。
10. 当用户需要设计探索、提供 Open Design 资料，或给了参考网站但只是想模仿风格而非一比一复制时，进入 Open Design 设计阶段。
11. URL 类输入在实现前必须先做全页交互/动效侦察。
12. 非完整克隆模式下，必要时生成 `layout-confirmation.html` 低保真布局交互确认稿。
13. 等用户确认页面、跳转、点击事件和滚动范围。
14. 开始实现、运行项目、截图检查、验证交互和滚动，并继续修正。
15. 在生成或大幅修改的前端项目 README 中写明安装、启动、构建、预览、测试和环境配置方式。

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

固定技术栈：

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

完整克隆不是只还原静态首屏。Agent 必须先完整浏览目标页面，形成全页交互/动效侦察结果，再实现所有可观察页面、路由、hover、click、focus、scroll、responsive、motion、media、overlay、form 等行为。

这个模式只用于完整复刻。  
如果用户只是想“模仿某个网站风格”，不要使用完整克隆模式，应进入 Open Design 设计阶段。

### 专有素材处理

完整复刻并不代表可以直接搬运源站的专有图片或品牌素材。

Agent 必须遵守：

- 不直接复制源站的专有图片、Logo、品牌素材、付费媒体或强识别度保护插画。
- 如果图片不能复用，必须先让用户选择媒体替代策略。
- 可选策略：
  1. 用户提供可用素材。
  2. 用户授权的素材库。
  3. 使用 image2 / 图像生成模型生成替代图。
  4. 使用同样尺寸、比例和位置的纯色 / 渐变 / 骨架占位块。
- 无论选择哪种策略，都要保留原区域的尺寸、比例、布局节奏、hover、click、motion、transition 和交互目标。
- 如果使用 image2 或图像生成模型，生成图只匹配用途、比例、构图、色彩氛围和视觉密度，不能复制 Logo、商标、专有产品图、强识别品牌资产或受保护插画。
- README 或交付说明中应标明哪些素材使用了用户素材、授权素材库、生成图或占位块。

### 图标来源策略

当项目需要图标，或源站图标、Logo、品牌标识不能复用时，Agent 必须先让用户选择图标来源策略。

可选策略：

1. 用户提供图标素材包，例如 SVG、PNG、zip。
2. 用户提供可访问的阿里 Iconfont 资源。
3. 使用指定公共图标库，例如 lucide、react-icons、Heroicons、Radix icons。
4. 使用 image2 / 图像生成模型生成简单的非品牌图标。
5. 使用纯 CSS、文字或几何占位图标。

Agent 不得直接复用源站专有 Logo、品牌图标、商标或强识别受保护图标。

无论使用哪种策略，都要保留：

- 图标语义。
- 尺寸、位置、颜色、描边/填充风格和视觉重量。
- hover、click、focus、active、selected、disabled 状态。
- 动效、transition 和点击热区。

#### 阿里 Iconfont 访问说明

阿里矢量图标库项目页经常需要登录或项目权限。  
如果用户只给了一个需要登录的 Iconfont 项目页面 URL，Agent 不能假装已经读取。

用户应提供以下任一可访问输入：

- 下载后的 SVG 文件或 zip 包。
- 公开可访问的 `iconfont.js` Symbol 链接。
- 公开可访问的 `iconfont.css` Font class 链接。
- 项目导出的本地 `iconfont.js`、`iconfont.css` 和字体文件。
- 图标名称清单 + 截图，用于从公共图标库选择等价图标，或生成简单替代图标。

默认推荐优先级：

1. 本地 SVG/zip，最稳。
2. 本地或可访问的 Symbol `iconfont.js`。
3. 本地或可访问的 Font class `iconfont.css` 和字体文件。
4. 公共图标库。
5. 生成的非品牌简单图标。
6. CSS/文字/几何占位。

项目 README 或交付说明中必须写明图标来源、接入方式、Iconfont 访问假设和替换说明。

## 全页交互/动效侦察

对 URL 普通还原和网站完整克隆，Agent 在实现前必须完成 Full Page Reconnaissance。

不能只看首屏或单张截图。必须检查：

- 页面位置：top、mid-scroll、bottom、关键 section。
- 视口：large-screen、必要时 tablet、mobile。
- 触发方式：hover、click、focus、active、scroll、resize、drag、load、submit、media event。
- 区域：Header、Hero、Nav、产品导航、section nav、Card、List、Form、Menu、Drawer、Modal、Carousel、Video、CTA、Footer。
- 动态 UI：滚动驱动 Header/Nav 变化、sticky section title、CTA 出现/隐藏、section reveal、lazy load、parallax、元素缩放/淡入、页面底部状态变化。
- 复杂组件：carousel、slider、gallery、film strip、横向卡片轨道、媒体查看器、产品选择器、Tabbed content。

实现前需要形成 interaction/motion inventory，可以是 `docs/reconnaissance.md`，也可以是实现计划里的表格。至少记录：

- 页面/路由：URL、页面名、可达入口。
- 区域：Header、Hero、Nav、Section、Card、Footer 等。
- 触发：hover、click、focus、scroll、resize、drag、load、submit。
- 初始状态：位置、尺寸、颜色、内容、可见性。
- 变化后状态：变化的属性和内容。
- 动效：duration、easing 感觉、delay、方向、透明度、位移、缩放。
- 复杂组件行为：controls、pagination、drag/swipe、scroll snap、autoplay/pause、loop/clamp、keyboard/focus、active/disabled、可见卡片数量、露出半张卡片、移动端差异。
- 滚动阈值：top、进入 section、离开 section、接近底部等。
- 响应式差异：large-screen、tablet、mobile。
- 实现状态：implemented / mocked / placeholder / gap。
- 备注：专有素材替换、无法访问、需要用户确认。

例如 Apple 产品页常见的行为：初始 Header 是全局导航；向下滚动到阈值后，变成产品局部导航或吸顶胶囊栏，并出现 Explore、Buy、Watch film 等 CTA。两种状态及其过渡都必须被侦察、记录并实现或列为 gap。

### 轮播图 / Gallery / Slider 规则

Apple 产品页这类页面常见的 Highlights 轮播、横向卡片、影片卡片、产品颜色选择器，都不能被静态截图或普通图片列表替代。

Agent 必须侦察并实现：

- 下一张/上一张按钮、分页点、缩略图、Tab、进度条、播放/暂停等控件。
- 当前项、上一项、下一项、disabled、selected、hover、focus、active 状态。
- 鼠标 hover、点击、拖拽、触摸滑动、键盘焦点/方向键行为。
- slide/fade/scale 动效、duration、easing、惯性、scroll snap、loop 或边界禁用行为。
- 图片/视频 lazy-load、autoplay、pause、caption/CTA 随卡片变化。
- 桌面端多卡片、露出半张卡片、移动端 swipe/scroll-snap 等响应式差异。

如果因为权限、素材或技术限制无法实现某个轮播行为，必须在交付说明中列为 gap，不能默默降级成静态图。

## 动效反向侦察与确认

当用户给 URL 并要求 1:1 还原时，Agent 不能只看首屏或静态截图就开始写代码。它必须先观察页面的时间轴、滚动转场、hover/click 状态和自动播放行为，并输出 `motion-spec` 让用户确认。

`motion-spec` 至少记录：

- 区域：Hero floating badges、Header、CTA、Section 2 preview 等。
- 元素：圆形图片、Logo、按钮、页面容器、第二屏大图等。
- 触发：page load、idle timer、scroll threshold、hover、click、section enter。
- 初始状态：scale、opacity、blur、transform、position、z-index。
- 动效描述：专业名称 + 自然语言描述。
- 参数估计：duration、delay、easing、loop、direction、transform-origin、filter blur 范围。
- 状态变化：hover 后暂停旋转、flip、blur 变化、auto-scroll 触发。
- 用户确认：confirmed / needs change / missing。
- 实现状态：pending / implemented / approximated / gap。

例如 ardot 类页面，Agent 应该先总结并确认这些动效，而不是直接实现：

- 四周小圆图的 `ambient orbital rotation`，保持匀速环绕/旋转。
- 不同角度出现不同程度的 `angle-dependent blur filter`。
- 鼠标 hover 到圆形元素时触发 `hover-triggered 3D flip`。
- hover 期间 `hover pauses ambient rotation`，离开后恢复。
- 页面刚打开时存在 `initial scale-down entrance animation`。
- 静置一段时间后触发 `timed auto-scroll to next section`。
- 第二屏进入时有 `section scale-in/scale-out transition`。

用户可以补充遗漏的动效。确认前，Agent 不得进入 1:1 最终实现；如果浏览器工具无法观察时间轴，Agent 必须要求用户提供录屏、截图或补充说明。

## PRD + OpenDesign 生成模式

当用户指定的参考文件是 PRD 时，Agent 必须进入 PRD + OpenDesign 生成模式。

工程基础强制使用：

```text
JCodesMore/ai-website-cloner-template
```

固定技术栈：

- Next.js
- React
- TypeScript
- Tailwind
- shadcn/ui

设计风格来源使用：

```text
nexu-io/open-design
```

推荐集成方式：**不要硬合并 Open Design 和 bolt.diy，第一版先用 MCP 打通。**

推荐流程：

```text
PRD
→ Open Design 生成或选择 DESIGN.md / tokens.css / components / prototype
→ bolt.diy 通过 Open Design MCP 读取设计上下文
→ bolt.diy 生成 React 前端项目
→ WebContainer 运行、预览、修复
→ 生成 docs/prd-coverage.md
```

Open Design 中优先读取：

- `DESIGN.md`：给 LLM 的设计规范，作为主要视觉权威。
- `tokens.css`：颜色、字体、间距、圆角、阴影等 CSS 变量来源。
- `components.html`：组件和布局参考。
- artifact / prototype / entry HTML：页面结构和视觉参考。

如果当前环境没有配置 Open Design MCP，Agent 应要求用户提供 `DESIGN.md`、`tokens.css`、`components.html` 或 Open Design artifact 导出，而不是凭空声称使用了 Open Design 风格。

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
- 动效节奏、hover 动效、展开/关闭动画、section reveal、media behavior、页面切换或轮播行为。
- 轮播图、gallery、slider、横向卡片轨道、媒体查看器、产品选择器的控件、分页、hover、click、drag/swipe、scroll snap、autoplay/pause 和响应式行为。
- 滚动阈值变化，例如 Header 从全局导航变成产品导航、CTA 出现/隐藏、section nav 吸顶。

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

PRD 生成前端：

```text
/FrontendFidelityAgent

这是一个 PRD。请使用 PRD + OpenDesign 生成模式，生成前端项目，并输出 docs/prd-coverage.md。
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
- URL 类任务已完成全页交互/动效侦察，发现项已实现或列为 gap。
- 轮播图、gallery、slider、横向卡片轨道等复杂组件的 hover、click、drag/swipe、pagination、active state、motion 和响应式行为已实现或列为 gap。
- hover、active、loading、empty、error、disabled 等状态完整。
- 动效节奏接近参考。
- 滚动范围和 fixed/sticky 行为符合确认稿。
- 项目 README 清楚说明如何安装、启动、构建和预览。
