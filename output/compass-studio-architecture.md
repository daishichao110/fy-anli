# 指南针代码工作室官网 - 架构设计与技术方案文档

## 1. 架构设计目标
- **高性能静态架构**：采用高复用、低耦合的原生 Vanilla HTML5 + CSS3 Variables + ES6 JavaScript 架构。
- **纯前端零部署门槛**：可直接通过 Nginx / Vercel / GitHub Pages / 任何静态托管一键部署，无后端依赖风险。
- **无缝集成案例库**：精准映射与管理 `deploy_html/` 目录下 50 个独立高保真 HTML 案例文件。
- **高可维护性组件化**：将 UI 结构解耦为 CSS Token 变量、结构化组件模块、逻辑控制器对象 (StudioApp)。

---

## 2. 系统技术栈选择

| 层级 | 技术选型 | 理由与说明 |
|:---|:---|:---|
| **标记语言** | HTML5 Semantic Markup | 良好的 SEO 结构、无障碍访问 (a11y)、标准 DOM |
| **样式语言** | CSS3 Native Custom Properties (Variables) | 灵活的暗/亮色调控，极高的渲染性能，无 Tailwind 打包负担 |
| **脚本逻辑** | ES6+ Modular Vanilla JS | 纯原生运行，免构建步骤，极速加载与事件代理机制 |
| **图标系统** | Lucide Icons (SVG / Web Font Standard) | 专业矢量级统一风格图标，替代粗劣 Emoji 和杂乱 PNG |
| **动画效果** | CSS Transitions & `@keyframes` | 硬件加速、流畅丝滑的 60fps 微交互 |
| **预览容器** | Dynamic iFrame Sandbox Modal | 安全防干扰隔离预览 `deploy_html/*.html` |

---

## 3. 文件组织与模块规划

```
/anli/
├── index.html                   # 官网主入口（整合 Hero、案例大厅、估算器、服务流程等）
├── deploy_html/                 # 50 个高保真商业案例库
│   ├── 01-car-wash.html
│   ├── 02-billiards-pingpong.html
│   ├── ...
│   └── 50-recycling-waste-collection.html
└── output/                      # Super Dev 体系工程产物
    ├── compass-studio-research.md
    ├── compass-studio-prd.md
    ├── compass-studio-architecture.md
    └── compass-studio-uiux.md
```

---

## 4. 核心逻辑架构与数据模型

### 4.1 50 个案例的结构化 JSON 数据模型 (`COMPASS_CASES_DATABASE`)
在 `index.html` 的 JS 中维护统一的案例元数据列表：
```javascript
const COMPASS_CASES_DATABASE = [
  {
    id: "01",
    file: "deploy_html/01-car-wash.html",
    title: "24H无人自助洗车/预约洗车系统",
    category: "life", // 分类 key
    categoryName: "生活与服务预约",
    tags: ["智能排队", "站点定位", "洗车卡包"],
    description: "覆盖智能站点地图定位、时段在线预约、洗车套餐充值与洗车设备物联网接口对接。",
    highlights: ["地图站点地图", "套餐月卡充值", "扫码开闸模拟"]
  },
  // ... 02 到 50 案例依次映射
];
```

### 4.2 案例分类映射字典 (`CASE_CATEGORIES`)
- `all`: 全部案例 (50)
- `life`: 生活与服务预约 (01洗车、03自习室、05茶室、24到家清洁、25家电清洗、27移动洗车、29私厨订制)
- `sports`: 休闲文娱与体育 (02棋牌桌球、04琴房音乐、06健身房、07剧本杀、30青少年体育、32徒步俱乐部、35室内滑雪冲浪)
- `beauty`: 美业与健康管理 (11美甲美睫、12理发店、13牙科诊所、14产后小儿推拿、15皮肤管理、16心理咨询、17瑜伽普拉提、18按摩艾灸、26上门spa)
- `pet`: 宠物经济与服务 (19宠物洗护寄养、20宠物医院疫苗、21宠物上门喂养、22宠物领养配种、23宠物殡葬)
- `rental`: 共享租赁与体验 (08露营装备、09无人机相机、10服装汉服、36西装旗袍定制、37鲜花订制、38烘焙蛋糕、39营地民宿、40奢侈品回收、41玩具绘本)
- `event`: 现场活动与社群 (31手工作坊、33少儿编程、34农场采摘、42活动摄影直播、43展会门票、44二手置换、45校友会商会)
- `enterprise`: 企服法务与工业 (46企业报修工单、47法律咨询合同、48私域商城、49施工质检物流、50废品回收)

### 4.3 需求在线估算器核心算法 (`EstimatorEngine`)
```javascript
// 估算器逻辑公式：
// BaseCost = BasePrice[ProjectType]
// FeaturesCost = Sum(SelectedFeaturePrices)
// UrgencyMultiplier = UrgencyFactor[Speed]
// TotalCost = (BaseCost + FeaturesCost) * UrgencyMultiplier
// EstimatedDays = BaseDays + Sum(FeatureDays)
```

---

## 5. 前端交互与性能优化策略

1. **DOM 事件代理机制**：
   - 案例大厅的筛选、分类切换、搜索响应均通过父级容器事件代理完成，减少 DOM 绑定开销。
2. **防抖与模糊搜索**：
   - 案例搜索输入框绑定 150ms Debounce，实现丝滑即时响应。
3. **iFrame 沙盒安全与防死锁**：
   - 案例预览弹窗加载 `iframe` 时设置 `loading="lazy"`，并在弹窗关闭时释放 `src=""`，避免内存泄露与后台音视频持续播放。
4. **CSS 原生 GPU 加速**：
   - 模态框展开、卡片悬浮提升使用 `transform: translateY()` 与 `opacity`，启用 GPU 硬件合成渲染层。
