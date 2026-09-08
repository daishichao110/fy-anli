# 实施任务清单：指南针代码工作室官网重构 (v1-compass-studio-official-site)

## 阶段 1：视觉代号与基础框架 (Design System & Foundation)
- [x] 锁定 CSS Tokens 系统（深灰背景 `--bg-app: #090D16`、主色 `--primary: #6366F1`、网格对齐、无低质渐变、无 Emoji）。
- [x] 引入 Lucide Icons 矢量图标库，准备矢量 SVG 图标渲染机制。

## 阶段 2：50 个案例全量元数据库搭建 (Case Portfolio Database)
- [x] 构建 `COMPASS_CASES_DATABASE` JavaScript 数组，将 `deploy_html/01-car-wash.html` ~ `50-recycling-waste-collection.html` 50 个高保真商业案例精准映射元数据（编号、标题、分类、场景标签、技术亮点、摘要）。
- [x] 配置 8 大行业分类选项卡字典与 Counts Badge 实时计算。

## 阶段 3：Hero 核心区与信任指标 (Hero Section & Trust Metrics)
- [x] 制作 Hero 区域：科技感网格背景、品牌定位主标题与副标题。
- [x] 制作 4 大信任数据浮动卡片（50+ 案例系统 / 100% 源码交付 / <24h 上手 / 0 隐形增项）。
- [x] 绑定 CTA 按钮导航定位。

## 阶段 4：案例大厅与高保真预览弹窗 (Case Showroom & Interactive Modal)
- [x] 实现 8 大行业 Tab 切换、搜索框防抖过滤与 Tag 快速筛选。
- [x] 实现案例卡片 Grid 布局：含案例编号、分类标签、核心功能点、在线预览按钮。
- [x] 实现高保真预览 Modal：📱 移动端 375px 手机框视角与 🖥️ 桌面端宽屏视角一键切换，动态加载 `iframe` 沙盒。

## 阶段 5：核心服务、技术标准与交互估算器 (Services, Engineering & Estimator)
- [x] 渲染核心服务矩阵 (微信小程序/SaaS后台/H5/UIUX重构)。
- [x] 渲染工程标准与 100% 源码交付承诺。
- [x] 实现【交互式项目预算在线估算器】：选择项目类型、勾选需求模块、估算工期与参考费用，支持一键携带清单发话。

## 阶段 6：敏捷流程、FAQ 与需求预约 Modal (Workflow, FAQ & Contact)
- [x] 渲染 5 步敏捷交付流程卡片。
- [x] 渲染 FAQ 常见问题解答区。
- [x] 实现【免费需求评估】在线提交 Modal 弹窗。

## 阶段 7：运行验证与去 AI 味细节打磨 (Verification & Quality Gate)
- [x] 检查网页全屏与移动端响应式兼容。
- [x] 测试全部 50 个案例链接调起与 iFrame 预览流畅度。
- [x] 确认代码极致干净、性能流畅、去 AI 味感突出。
