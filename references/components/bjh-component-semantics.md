# 百家号 PC 组件语义库

## 使用口径

组件不是 UI 元素清单，而是功能语义的承载器。执行百家号 PC 页面设计时，先完成框架匹配，再把需求自然语言转换为功能语义、用户任务、交互意图、组件候选和组件组合。

组件语义识别链路：

```text
PRD 自然语言
→ 功能语义
→ 用户任务
→ 交互意图
→ 组件候选
→ 组件组合
→ 设计结构
```

示例：

```text
“支持用户按订单状态、创建时间、负责人筛选订单，并批量导出结果”
→ 对象管理 + 查询筛选 + 批量操作 + 导出反馈
→ 用户需要对多条结构化数据执行同一动作
→ 需要筛选区、选择机制、批量操作入口、导出结果反馈
→ Input/Select/DatePicker + Tabular.rowSelection + Button + Toast/Progress/Modal
→ FilterBar + Tabular + BatchActionBar + ExportButton + Feedback
```

## 强制复用规则

- 优先复用百家号 PC Figma 组件库中的组件语义和样式，不自创新组件名、组件形态或脱离组件库的视觉语言。
- 先判断功能意图，再选择组件。不要把“按钮”直接匹配成 Button，也不要把“表格”直接匹配成 Tabular。
- 组件属于内容层和实现层，不能改变已锁定的页面框架。框架决定区域关系，组件决定区域内如何承载任务。
- 若语义库已有组件可表达需求，必须使用已有组件；只有当语义库没有覆盖且需求确实不可替代时，才标注为“缺口组件/待补充”，不得直接自创。
- 反馈类组件如 Modal、Toast、Notification、Loading 不作为页面主结构组件，只作为操作结果、确认、等待或风险说明的辅助机制。
- 输出组件方案时必须同时写明“适用语义”“不适用边界”“常见组合”和“复用来源/缺口判断”。

## 语义模式

### 对象管理工作区

适用语义：
- 管理作品、素材、话题、商品、商单等对象集合。
- 需要搜索、筛选、分页、批量选择、批量处理、行内操作。

优先组件组合：
- Input + Select + DatePicker + Button
- Tabs + FilterBar + Tabular + Pagination
- Tabular.rowSelection + BatchActionBar + Button
- Empty + Button
- Modal/Toast 仅用于确认和结果反馈

百家号场景：
- 作品管理、素材管理、话题管理、商品管理、商单列表。

### 数据探索工作区

适用语义：
- 围绕内容、主页、收益、经营表现进行时间筛选、指标查看、趋势阅读。
- 用户目标是理解状态，而不是直接管理对象。

优先组件组合：
- Tabs + SelectDate/DatePicker + DataDisplay
- DataDisplay + Tooltip + Progress
- DataDisplay + Tabular
- Empty/Loading 作为数据状态

百家号场景：
- 内容分析、号主页分析、收入中心、首页数据概览。

### 表单录入与提交

适用语义：
- 创建、编辑、配置、申请、上传资料、提交设置。
- 用户需要录入结构化字段，并最终保存或提交。

优先组件组合：
- FormItem + Input/Textarea/InputNumber/Select/Radio/Checkbox/Switch
- DatePicker/TimePicker 用于时间字段
- Upload + Alert + Progress
- ButtonGroup 放在表单底部或局部操作区

百家号场景：
- 账号配置、内容设置、收益设置、认证申请、素材上传。

### 资源发现与参与

适用语义：
- 浏览课程、话题、商品、活动、任务或资源，并选择参与、报名、查看详情。
- 对象通常依赖图片、标签、状态和转化动作，不一定适合表格。

优先组件组合：
- Tabs + Tag + Button + Pagination
- ResourceCard 语义若组件库缺失，先用现有 Card/List 容器模式承载，并标注缺口。
- Badge/Tooltip/Popover 用于资源状态和规则说明
- Empty 用于无结果

百家号场景：
- 学习中心、搜索话题、电商带货、度星选商单。

### 风险操作与反馈

适用语义：
- 删除、禁用、提交审核、退出编辑、保存失败、权限不足、规则风险。

优先组件组合：
- Button.danger + Modal + ButtonGroup
- Alert + Link/Button
- Toast/Notification 用于操作结果
- Loading/Progress 用于等待和进度

百家号场景：
- 删除作品、禁用设置、提交审核、上传失败、收益异常说明。

## 组件语义速查

### Button 按钮

适用语义：
- 触发明确动作，如提交、保存、创建、发布、删除、批量处理。
- 在工具栏、表单底部、对话框底部表达操作优先级。

不适用：
- 展示状态或标签。
- 承载长说明文本。
- 表示页面分组导航。

常见组合：
- Toolbar + Button
- Form + ButtonGroup
- Modal + ButtonGroup
- Empty + Button
- Tabular + RowAction Button

执行提示：
- 先判断动作风险和主次。主路径用一级按钮，普通辅助用二级按钮，新增占位可用虚线按钮，删除/禁用等风险动作使用危险按钮。

### Link 链接

适用语义：
- 跳转详情、说明、帮助或外部资源。
- 在正文、表格行、提示文案中提供轻量入口。

不适用：
- 提交表单。
- 触发高风险操作。
- 承载主要页面主行动。

常见组合：
- Alert + Link
- Tabular + Link
- Tooltip + Link

执行提示：
- 点击后改变数据状态时优先用 Button；只是导航或打开说明时用 Link。

### Breadcrumb 面包屑

适用语义：
- 表达当前位置层级。
- 从详情页、编辑页回到上级列表。

不适用：
- 同级页面切换。
- 流程步骤表达。
- 页面内锚点定位。

常见组合：
- Breadcrumb + PageTitle
- Breadcrumb + DetailForm

执行提示：
- 进入对象详情或配置子页时使用；单页内分类切换不要用它替代 Tabs。

### Pagination 分页

适用语义：
- 拆分大量同构数据。
- 在列表或表格底部控制页码。
- 保持当前筛选条件下的对象集合浏览。

不适用：
- 少量固定内容。
- 步骤流程。
- 无限滚动信息流。

常见组合：
- FilterBar + Tabular + Pagination
- ResourceGrid + Pagination

执行提示：
- 出现大量对象集合、页码、每页数量或总条数时，把 Pagination 和列表/表格绑定考虑。

### Anchor 锚点

适用语义：
- 长页面内快速定位章节。
- 设置页或说明页内跳转到局部模块。

不适用：
- 跨页面导航。
- 对象列表筛选。
- 流程步骤状态。

常见组合：
- Anchor + LongFormSections
- Anchor + SettingsSections

执行提示：
- 长表单或长说明用 Anchor；多个互斥视图用 Tabs。

### Steps 步骤条

适用语义：
- 展示有顺序的多步骤任务。
- 表达当前步骤、已完成步骤和后续步骤。
- 申请、认证、开通、发布向导。

不适用：
- 普通状态枚举。
- 页面分类切换。
- 无固定顺序的设置分组。

常见组合：
- Steps + Form + ButtonGroup
- Steps + Alert + ResultFeedback

执行提示：
- 只有任务必须按顺序完成时才用 Steps；不同类别使用 Tabs 或 Select。

### Input 输入框

适用语义：
- 录入短文本。
- 搜索关键词、标题、昵称、链接、单行配置值。
- 需要即时校验或错误提示的文本字段。

不适用：
- 长段正文。
- 固定选项选择。
- 数字步进输入。

常见组合：
- FormItem + Input
- SearchBar + Input + Button
- Input + Tooltip

执行提示：
- 用户自由输入短文本时用 Input；选项可枚举时优先 Select/Radio/Checkbox。

### Textarea 文本域

适用语义：
- 录入多行文本。
- 填写简介、说明、拒绝原因、备注、回复内容。
- 需要字数统计或较长表达。

不适用：
- 短关键词搜索。
- 结构化字段集合。
- 富文本创作编辑器。

常见组合：
- FormItem + Textarea
- Modal + Textarea + ButtonGroup
- CommentReply + Textarea

执行提示：
- 输入自然语言段落时优先 Textarea，不要用多个 Input 拼长文本。

### InputNumber 数字输入框

适用语义：
- 录入数量、比例、金额、阈值等数字。
- 需要上下限、步进、单位或格式校验。

不适用：
- 普通文本。
- 少数几个固定数字选项。
- 展示统计指标。

常见组合：
- FormItem + InputNumber
- Slider + InputNumber
- Select + InputNumber

执行提示：
- 数字可手动输入且需要精确值时用 InputNumber；粗略范围调节可加 Slider。

### Select 选择器

适用语义：
- 从枚举选项中选择一个或多个值。
- 筛选状态、类型、分类、来源、排序。
- 节省横向空间的表单选择。

不适用：
- 少于 3 个且需要直接比较的互斥选项。
- 开关型布尔设置。
- 长层级树选择。

常见组合：
- FilterBar + Select
- FormItem + Select
- Select + Pagination

执行提示：
- 选项不需要全部露出且数量较多时用 Select；两个互斥项优先 Radio 或 Switch。

### TreeSelect 树选择

适用语义：
- 选择层级分类。
- 内容垂类、地区、组织、资源目录等多级结构。

不适用：
- 平铺少量选项。
- 自由输入分类。
- 普通状态筛选。

常见组合：
- FormItem + TreeSelect
- FilterBar + TreeSelect
- Popover + TreeSelect

执行提示：
- 需求暗示父子层级或多级目录时，TreeSelect 比 Select 更准确。

### Checkbox 多选框

适用语义：
- 从多个独立选项中选择任意项。
- 批量选择列表行。
- 协议确认、附加配置、组合条件。

不适用：
- 互斥单选。
- 即时开关设置。
- 主要动作触发。

常见组合：
- Checkbox + Tabular
- CheckboxGroup + Form
- Modal + Checkbox + Button

执行提示：
- 多选语义用 Checkbox；单个开关且立即生效用 Switch。

### Radio 单选按钮

适用语义：
- 在少量互斥选项中选择一个。
- 需要选项同时可见以便比较。
- 配置模式、发布范围、结算方式。

不适用：
- 多选条件。
- 大量选项。
- 即时启停功能。

常见组合：
- RadioGroup + FormItem
- Modal + RadioGroup
- FilterPanel + RadioGroup

执行提示：
- 2 到 5 个互斥选项且需要直接比较时用 Radio；数量更多时用 Select。

### Switch 开关

适用语义：
- 启用或关闭某项设置。
- 状态改变可立即生效。
- 表达开/关、是/否、启用/停用。

不适用：
- 需要提交按钮确认的复杂选择。
- 多个互斥选项。
- 风险较高且不可撤销的操作。

常见组合：
- SettingRow + Switch
- Alert + Switch
- Toast + Switch

执行提示：
- Switch 通常代表即时状态变化。若操作有风险，增加确认 Modal 或改用 Button 触发确认。

### Slider 滑动输入条

适用语义：
- 调整连续范围值。
- 表达比例、强度、阈值、区间。
- 允许用户快速试探一个近似值。

不适用：
- 需要精确数字录入。
- 离散文本选项。
- 只读进度展示。

常见组合：
- Slider + InputNumber
- FormItem + Slider
- Tooltip + Slider

执行提示：
- 精确值用 InputNumber，连续调节用 Slider，两者可组合满足粗调和精调。

### Upload 上传

适用语义：
- 上传图片、视频、证明材料或附件。
- 展示上传进度、失败重试、格式限制。
- 为空时提供添加入口。

不适用：
- 选择已有素材。
- 输入链接。
- 展示已经发布的媒体列表。

常见组合：
- Upload + Alert
- Upload + Progress
- Form + Upload + Button

执行提示：
- 本地文件进入系统用 Upload；从已有资源库挑选应使用资源选择器或列表。

### DatePicker 日期选择框

适用语义：
- 选择单日、日期范围或业务周期。
- 配合数据查询、发布时间、有效期设置。
- 需要日历心智的时间输入。

不适用：
- 具体时分秒选择。
- 相对时间快捷切换。
- 纯文本日期展示。

常见组合：
- DatePicker + Button
- FilterBar + DatePicker
- Tabs + DatePicker + DataDisplay

执行提示：
- 分析页和列表页常把 DatePicker 放在局部控制区；不要用普通 Input 让用户手打日期。

### SelectDate 日期快捷选择

适用语义：
- 在近 7 日、近 30 日等快捷周期和自定义日期间切换。
- 数据看板里的高频时间过滤。

不适用：
- 一次性精确日期录入。
- 与数据无关的表单字段。
- 复杂排期。

常见组合：
- SelectDate + DataDisplay
- SelectDate + Tabs
- SelectDate + Tabular

执行提示：
- 需要频繁切换统计周期时，SelectDate 比单纯 DatePicker 更贴近分析语义。

### TimePicker 时间选择框

适用语义：
- 选择时刻或时间段。
- 定时发布、活动时间、任务截止时间。

不适用：
- 日期范围筛选。
- 相对周期快捷筛选。
- 只读时间展示。

常见组合：
- DatePicker + TimePicker
- FormItem + TimePicker

执行提示：
- 只有需要具体时分时使用 TimePicker；单纯日期或统计周期不要增加时间选择负担。

### Tabs 标签页

适用语义：
- 同一页面内切换互斥内容视图。
- 按状态、类型、频道或数据维度分组。
- 保持页面框架不变，仅切换主工作区内容。

不适用：
- 流程步骤。
- 长页面章节定位。
- 大量层级导航。

常见组合：
- Tabs + FilterBar + Tabular
- Tabs + DataDisplay
- Tabs + Empty

执行提示：
- Tabs 表达同级互斥视图。若顺序必须完成，用 Steps；若页面内定位，用 Anchor。

### Tabular 表格

适用语义：
- 展示多条结构化数据。
- 支持排序、筛选、分页、批量选择、行内操作。
- 对比对象的多个字段。

不适用：
- 展示少量关键字段。
- 强视觉内容卡片。
- 长文本阅读。

常见组合：
- FilterBar + Tabular + Pagination
- Toolbar + Tabular + BatchActionBar
- Tabs + Tabular + Empty

执行提示：
- 对象数量多且字段结构稳定时用 Tabular。若每个对象依赖图片和营销信息，考虑资源卡片或列表模式，不要硬套表格。

### DataDisplay 数据展示

适用语义：
- 展示关键指标、统计摘要或数据模块。
- 表达数值、趋势、分布、排行等分析内容。
- 帮助用户快速判断经营状态。

不适用：
- 录入数据。
- 长列表管理。
- 操作确认。

常见组合：
- SelectDate + DataDisplay
- Tabs + DataDisplay
- Tooltip + DataDisplay
- Progress + DataDisplay

执行提示：
- 如果需求是看数据状态而不是管理对象，优先考虑 DataDisplay，再按需要组合图表、表格或进度。

### Tooltip 文字提示

适用语义：
- 解释术语、指标、图标或禁用原因。
- 鼠标悬停出现的短说明。
- 降低界面文案拥挤。

不适用：
- 承载关键业务信息。
- 复杂操作面板。
- 错误反馈主通道。

常见组合：
- Icon + Tooltip
- FormLabel + Tooltip
- DataDisplay + Tooltip

执行提示：
- Tooltip 只放补充说明。用户必须知道的信息不要藏在悬停里。

### Popover 气泡卡片

适用语义：
- 承载比 Tooltip 更复杂的轻量内容。
- 局部说明、快捷操作、小型选择面板。
- 不离开当前上下文的辅助信息。

不适用：
- 完整表单流程。
- 高风险确认。
- 全局通知。

常见组合：
- Button + Popover
- Tag + Popover
- TableCell + Popover

执行提示：
- 局部看更多或做轻量选择时用 Popover；需要阻断并确认时用 Modal。

### Progress 进度条

适用语义：
- 展示任务完成度、上传进度、等级进度或指标达成率。
- 表达从当前值到目标值的距离。

不适用：
- 不确定等待状态。
- 普通统计数字。
- 状态标签。

常见组合：
- Upload + Progress
- DataDisplay + Progress
- Tooltip + Progress

执行提示：
- 有明确总量或目标时用 Progress；不知道耗时的加载等待用 Loading。

### Avatar 头像

适用语义：
- 展示账号、作者、用户或评论者身份。
- 和名称、等级、认证状态组合成身份入口。

不适用：
- 普通图标。
- 封面图。
- 商品图。

常见组合：
- Avatar + UserName + Badge
- CommentItem + Avatar
- Header + Avatar

执行提示：
- Avatar 表达身份，不要拿来做普通图片容器。

### Tag 标签

适用语义：
- 标记对象属性、状态、分类或轻量筛选条件。
- 让用户快速扫读内容类型和状态。

不适用：
- 主要操作按钮。
- 长文本说明。
- 强反馈通知。

常见组合：
- Tag + ResourceCard
- Tag + Tabular
- FilterBar + Tag

执行提示：
- Tag 是属性标记。若用户点击后触发主要动作，不要伪装成 Tag。

### Badge 徽标

适用语义：
- 提示未读数量、待处理数量、新内容或小状态。
- 附着在导航项、头像、图标或标签上。

不适用：
- 完整状态说明。
- 重要错误提示。
- 大段统计数据。

常见组合：
- NavItem + Badge
- Avatar + Badge
- Tabs + Badge

执行提示：
- Badge 必须附着在某个对象上；独立提示请用 Alert/Toast/Notification。

### Empty 空状态

适用语义：
- 当前数据为空、搜索无结果、列表尚未创建对象。
- 解释状态并给出下一步行动。
- 替代表格/列表/卡片区域的内容状态。

不适用：
- 加载中。
- 错误失败。
- 权限不足且需强提示。

常见组合：
- Tabular + Empty
- FilterBar + Empty
- Empty + Button
- Empty + Link

执行提示：
- 空状态不是只写“暂无数据”。要说明为什么空，以及下一步能做什么。

### Alert 警告

适用语义：
- 页面内持续展示的重要提示。
- 风险、规则、异常、权限、审核说明。
- 需要用户在操作前看到的上下文信息。

不适用：
- 短暂成功反馈。
- 全局系统通知。
- 确认二次弹窗。

常见组合：
- Alert + Link
- Form + Alert
- Upload + Alert
- Tabular + Alert

执行提示：
- Alert 放在相关内容附近并持续可见；操作完成后的短反馈用 Toast。

### Modal 对话框

适用语义：
- 当前任务中的轻量确认。
- 不离开当前页面的小型表单。
- 删除、禁用、提交等风险操作确认。

不适用：
- 长流程配置。
- 多步骤复杂表单。
- 需要频繁对照上下文的信息录入。

常见组合：
- Modal + ButtonGroup
- Modal + Form
- Modal + Alert
- Tabular RowAction + Modal

执行提示：
- Modal 会打断任务，只用于必须聚焦的小型决策或录入；复杂流程应进入独立页面或抽屉式工作区。

### Toast 全局提示

适用语义：
- 操作后的短暂反馈。
- 成功、失败、保存中、复制成功等即时结果。
- 不要求用户立刻处理的轻量信息。

不适用：
- 需要持续阅读的规则。
- 高风险确认。
- 复杂错误修复指引。

常见组合：
- Button Action + Toast
- Switch + Toast
- Upload + Toast

执行提示：
- Toast 是结果反馈，不是决策界面。需要用户确认时用 Modal，需要持续提示时用 Alert。

### Notification 通知框

适用语义：
- 较完整的全局消息通知。
- 系统级变化、审核结果、任务提醒。
- 可包含标题、正文和操作入口。

不适用：
- 字段级错误。
- 页面内规则提示。
- 一闪而过的成功反馈。

常见组合：
- Notification + Link
- Header + Notification
- Badge + Notification

执行提示：
- Notification 比 Toast 更完整，适合可稍后处理的系统消息。页面局部提示仍优先 Alert。

### Loading 加载

适用语义：
- 数据请求、提交处理或局部模块刷新中。
- 表达系统正在处理且用户需等待。
- 配合按钮、表格、页面区域使用。

不适用：
- 有明确比例的进度。
- 空数据。
- 错误失败。

常见组合：
- Button + Loading
- Tabular + Loading
- DataDisplay + Loading

执行提示：
- 可预估进度用 Progress；不可预估等待用 Loading，并尽量限定在局部区域。

### Header 顶部导航

适用语义：
- 全局品牌、消息、账号和系统入口。
- 维持百家号 PC 的全局外壳一致性。

不适用：
- 页面内分类切换。
- 单个模块标题。
- 局部工具栏。

常见组合：
- Header + Sidebar + Workspace
- Header + Badge + Avatar

执行提示：
- Header 是全局壳层组件，通常不由业务需求单独新增；设计页面时保持它稳定。

## 输出模板

完成框架锁定后，对百家号页面必须追加以下组件语义输出：

```text
组件语义识别结果

功能语义：
- [语义1]：[来自需求的自然语言证据]
- [语义2]：[来自需求的自然语言证据]

组件候选：
- [组件]：适用语义 / 不适用边界 / 复用依据
- [组件]：适用语义 / 不适用边界 / 复用依据

组件组合：
- [组合1]：承载 [用户任务/交互意图]
- [组合2]：承载 [用户任务/交互意图]

复用校验：
- 已复用：[组件/组合]
- 不新增：[说明哪些需求由已有组件承载]
- 缺口：[仅当确实无法复用时填写，否则写“无”]
```
