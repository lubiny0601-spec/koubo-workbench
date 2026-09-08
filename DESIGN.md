# DESIGN.md — 口播工作台 Design System

## 产品坐标

单一用户，零代码，学AI，练表达。本地网页工具，桌面优先，偶尔移动端。安静、聚焦、工具感。内容是主角，界面是配角。

## 颜色角色

| Token | 值 | 用途 |
---|---|---|
| `--bg` | `#F7F7F5` | 页面背景（暖白，非纯灰） |
| `--surface` | `#FFFFFF` | 卡片、输入区、输出区 |
| `--surface-muted` | `#F4F4F1` | 次要表面、segmented track、输入区背景 |
| `--ink` | `#1A1A17` | 主文字（暖黑，非纯黑） |
| `--ink-secondary` | `#5C5C56` | 次要文字、标签 |
| `--ink-tertiary` | `#9A9A92` | 占位符、提示 |
| `--border` | `#E8E6E0` | 结构边框、分割线 |
| `--border-strong` | `#D5D3CC` | 输入框边框、hover 边框 |
| `--primary` | `#0F766E` | 品牌色——选中态、激活态、链接 |
| `--primary-surface` | `#F0FDFA` | 品牌色 Surface——选中态背景、nav active bg |
| `--cta` | `#C2410C` | 主操作按钮（生成、解释）唯一出现位置 |
| `--cta-hover` | `#9A3412` | CTA hover |
| `--danger` | `#B91C1C` | 错误态文字、错误图标、destructive |
| `--danger-surface` | `#FEF2F2` | 错误态背景 |

### 色彩约束

CTA 橙色只出现在主操作按钮上，全页面最多两处。Primary teal 用于选中态和品牌标识，面积不超过 15%。其余全部暖灰中性。不用蓝色、紫色、粉色作为功能色。不用渐变。

### Markers 语义色（仅用于口播脚本表演标记）

| 标记类型 | 背景 | 文字 |
---|---|---|
| 语气 | `#F0FDFA` / `--primary-surface` | `#0F766E` / `--primary` |
| 停顿 | `#FEF9C3` | `#854D0E` |
| 重音 | `#FFEBE9` | `#9F1239` |
| 情绪 | `#E0E7FF` | `#4338CA` |

## 字体层级

单一族 `Plus Jakarta Sans`，表演标记用 `JetBrains Mono`。

| 角色 | weight | size | line-height | 用途 |
---|---|---|---|---|
| Display | 800 | 28px | 1.2 | 首页主标题 |
| H1 | 700 | 22px | 1.3 | 视图标题 |
| H2 | 600 | 17px | 1.35 | 区块标题、概念标题 |
| H3 | 600 | 14px | 1.4 | 卡片标题、段落功能标签 |
| Body | 400 | 15px | 1.7 | 正文、脚本内容 |
| Body-sm | 400 | 13px | 1.6 | 辅助说明、meta |
| Label | 600 | 13px | 1.4 | 按钮文字、表单标签 |
| Mono-sm | 500 | 12px | 1.4 | 表演标记 chips |
| Code | 400 | 13px | 1.5 | 行内 code / mono span |

字间距 = 0。正文 `text-wrap: pretty`。标题 `text-wrap: balance`。

## 间距与栅格

8dp 系统：`4 / 8 / 12 / 16 / 20 / 24 / 32 / 48 / 64`

| 场景 | 值 |
---|---|
| 组件内 padding | 12-16px |
| 组件间 gap | 12-16px |
| 区块间距 | 24px |
| 页面 padding (移动) | 16px |
| 页面 padding (桌面) | 32px |
| 内容最大宽度 | 720px (`max-w-3xl`) |

桌面侧栏 240px 固定。内容区右贴，不居中（左对齐工作区感）。

## 圆角

| 组件 | 半径 |
---|---|
| 按钮 | 8px |
| 输入框 / textarea | 8px |
| 卡片 | 10px |
| 标记 chip | 5px |
| segmented track | 8px |
| segmented 选项 | 6px |
| 图标容器 | 8px |
| 头像 / 步骤圆 | 50% |

嵌套规则：外半径 = 内半径 + padding。

## 边框与阴影

### 边框

结构分割线用 1px `--border`。输入框边框用 1px `--border-strong`，focus 时切换为 2px `--primary` ring。卡片边框用 1px `--border`。

### 阴影系统

| 层级 | 值 | 用途 |
---|---|---|
| `shadow-elevated` | `0 1px 2px rgba(0,0,0,0.04)` | 卡片静止态——比 border 更轻 |
| `shadow-selected` | `0 0 0 1px rgba(15,118,110,0.12)` | segmented 选中态——teal hairline ring |
| `shadow-overlay` | `0 4px 12px rgba(0,0,0,0.08)` | 暂未使用，预留 dropdown/modal |

卡片不用 border，用 `shadow-elevated`。输入框用 border。分割线用 border。

## 表面层级

| z-layer | 表面 | 背景 |
---|---|---|
| 0 | 页面底 | `--bg` |
| 1 | 卡片 / 输入区 / 输出区 | `--surface` + `shadow-elevated` |
| 2 | segmented track | `--surface-muted` |
| 3 | sticky mobile header | `--surface` + border-b |

不用卡片嵌套卡片。输出区内部分段之间用 border-b 分割，不再各自包卡片。

## 按钮

### CTA 按钮（主操作）

`bg-cta text-white h-11 px-6 rounded-lg font-semibold text-[13px]`
States: hover `bg-cta-hover`。active `scale-[0.96]` 150ms。disabled `opacity-40 cursor-not-allowed`，disabled 时不缩放。

### 次要按钮

带边框型：`bg-surface border border-border-strong text-ink h-9 px-4 rounded-lg font-medium text-[13px]`。hover `bg-surface-muted`。active `scale-[0.96]`。

### 推荐词 / chip 按钮

`bg-surface-muted text-ink-secondary px-3 py-2 rounded-lg text-[13px] font-medium h-9 min-h-[36px]`。hover `bg-primary-surface text-primary`。active `scale-[0.96]`。

### 生成按钮 loading 态

disabled + spinner（白色 border 圈）+ 文字变为"生成中..."。按钮宽度不变（不因文字变短而缩）。

全部 `transition-[background-color,transform] duration-150 ease-out`，不用 `transition: all`。

## 卡片

`bg-surface shadow-elevated rounded-[10px]`。不用 border。内 padding 20px。

首页工具入口卡片：同上，hover 时 `shadow-selected`（teal ring）替代 border 变色。`active:scale-[0.96]`。

## 表单

### Input / Textarea

`h-11 bg-surface-muted border border-border-strong rounded-lg px-4 text-[15px] text-ink`。
placeholder `text-ink-tertiary`。
focus: `border-primary ring-2 ring-primary/15 ring-offset-0 bg-surface`。
transition: `transition-[border-color,box-shadow,background-color] duration-150`。

### Label

Label 在 input 上方，`text-[13px] font-semibold text-ink-secondary mb-2`。不用 placeholder 替代 label。

### Validation

错误提示在 input 下方，`text-[13px] text-danger flex items-center gap-1.5 mt-2.5`。配 14px danger 图标。

## 分段控件 (Segmented Control)

Track: `inline-flex bg-surface-muted rounded-lg p-1 gap-0.5`。
选项: `seg-btn px-4 py-2.5 rounded-md text-[13px] font-semibold min-h-[44px]`。
选中态: `bg-surface text-primary shadow-selected`。
未选中: `text-ink-secondary hover:text-ink`。
transition: `transition-[color,background-color,box-shadow] duration-150 ease-out`。

时长三档在移动端 flex-1 等宽分布。

## 导航

### 桌面侧栏

240px 固定，`bg-surface border-r border-border`。Logo 行 64px 高。
Nav item: `w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-[13px] font-semibold min-h-[44px] text-ink-secondary hover:bg-surface-muted`。
Active: `bg-primary-surface text-primary`，图标变 `text-primary`。

### 移动端顶栏

`sticky top-0 bg-surface border-b border-border min-h-[56px] z-50`。
内嵌分段控件式导航：3 个按钮在 `bg-surface-muted rounded-lg p-1` 内。选中态同 segmented。文字简短"首页/话术/概念"。

## 脚本输出段

每段是 `flex gap-3 pb-4`，底部 `border-b border-border last:border-0`。
左侧色条：`w-[3px] rounded-full`，颜色按功能（钩子=cta，解释=primary，举例=ink-tertiary，总结=primary）。
功能标签：`text-[12px] font-semibold px-2 py-0.5 rounded`，语义色。
正文：`text-[15px] text-ink leading-[1.7] mt-2`。
Markers 行：`flex flex-wrap gap-1.5 mt-2.5`。

## 空状态

`bg-surface shadow-elevated rounded-[10px] py-16 px-12 text-center`。
图标容器：`w-12 h-12 rounded-full bg-surface-muted`，图标 `text-ink-tertiary`。
主文字：`text-[15px] font-semibold text-ink-secondary`。
次文字：`text-[13px] text-ink-tertiary mt-1`。
不用 dashed border，用 `shadow-elevated` 保持一致表面层级。

## 加载态

Card 内 `bg-surface shadow-elevated`。spinner + `text-[14px] text-ink-secondary font-medium`。
Skeleton 行：`skeleton h-4 rounded`，shimmer 动画 1.5s。
尊重 `prefers-reduced-motion`。

## 错误态

`bg-danger-surface border border-danger/20 rounded-[10px] py-12 px-8 text-center`。
图标圆 `bg-white` + `text-danger` 图标。
主文字 `text-[15px] font-semibold text-ink`。
详情 `text-[13px] text-ink-tertiary mt-1`。
重试按钮: CTA 样式。

## 步骤引导（首页工作流程）

编号圆 `w-7 h-7 rounded-full bg-primary-surface text-primary text-[12px] font-bold`。
步骤标题 `text-[14px] font-semibold text-ink`。
步骤说明 `text-[13px] text-ink-secondary mt-0.5 leading-relaxed text-pretty`。

## 交互状态总结

| 状态 | 视觉 | 动画 |
---|---|---|
| hover | 背景色加深 / shadow-selected | 150ms ease-out |
| active | scale(0.96) + 背景色更深 | 150ms ease-out |
| focus | 2px primary ring + 1px ring/15 | 150ms |
| disabled | opacity-40 + cursor-not-allowed | 无动画 |
| loading | spinner + 文字变更 + btn disabled | spinner 600ms |
| error | danger-surface + danger icon + retry CTA | 无 |
| success | 复制按钮变"已复制"+ checkmark | 150ms |
| empty | 图标 + 引导文字 | 无 |

## 响应式

| 断点 | 布局变化 |
---|---|
| < 768px | 侧栏隐藏，顶栏分段导航。内容 padding 16px。时长三档 flex-1 等宽 |
| >= 768px | 侧栏显示 240px。内容 padding 24px。 |
| >= 1024px | 侧栏 240px。内容 padding 32px。max-w-3xl 720px |
| >= 1280px | 同 1024，内容区居左不居中 |

移动端所有按钮 min-h 44px。touch target 间距 >= 8px。

## 禁止

不渐变。不 glassmorphism。不阴影堆叠（最多一层 elevated）。不 emoji 图标。不卡片嵌套卡片。不营销 hero。不 rounded-full 大圆角。不 transition: all。不 fixed px 宽度容器。不单色调主导。不用 blue/purple/pink 功能色。
§END
