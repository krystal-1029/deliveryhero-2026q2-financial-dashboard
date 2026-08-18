# Delivery Hero 2026Q2 看板版式对齐审计

- 本轮按 iFood FY26 基准生成财报看板，根元素设有 `data-dashboard-baseline="ifood-fy26"`；未生成或改写公司导览页。
- 交付文件：`deliveryhero_dashboard_local_preview/index.html`、`assets/sources/`、`start_preview.bat`、`README_如何打开.txt`、`server.cjs`、预览压缩包与本审计文件、指标定义文件。
- 页面结构为 Hero → Topline → Bottomline → 术语与口径 → 来源；按用户要求未设置运营侧，也未显示“财报分析”总标题。Hero 公司标识不再展示“最新实际披露至”的字样。
- 视觉保留 iFood 的暖白/浅米背景、橙色主强调、深色洞察卡、圆角图表卡，以及 `grid-2`、`chart-card`、`analysis`、`analysis-list`、`analysis-item`、`view-label`、`terms`、`source-grid` 层级。
- 前台不含 HTML 数据表、`table-wrap`、`forecast-table` 或 `data-table`；历史、地区与预测均由图表、tooltip 和简洁预测要点承载。
- 本轮增量修改：Hero 不再出现区域增长或地区组合观点；原有区域增长的图表、公司披露洞察与券商观点均保留并集中于 Topline。Hero 以即时零售的已披露运营事实替换原区域条目，且外部补充仅保留全年指引与监管情景。其余模块、图表类型、数据、文案与交互均延续上一版。
- 所有五张 SVG 图表本体均直接带有 `data-chart`，并保留原有图表卡容器、具体标题、图例、来源说明与键盘可聚焦 tooltip；图表数据集中于页面脚本的 `chartData` 对象，无外部 CDN。收入/GMV 与 Adjusted EBITDA/GMV 均使用独立百分比右轴，避免金额轴与比例轴混用。
- 数据来源、统一口径、H2 例外计算、缺失处理详见 `metric_definitions.md`。2026Q1 单季利润未披露，未伪造或补零。
- 验证完成：内联脚本通过 Node 语法校验；静态渲染链路确认五张 SVG 均由 `render` 调用并具备非空图形节点生成路径；根标记、`chartData`、IIFE、首次渲染入口、五张图的 `data-chart`、无外部 CDN、无前台数据表及无前台操作提示词均通过检查；全部五个前台来源链接均指向预览包内已复制的文件；压缩包通过完整性测试，且顶层目录命名正确。尝试通过 `server.cjs` 启动本地服务时，执行环境禁止监听本地端口（`EPERM`）；Playwright CLI 尝试受该受限环境阻断，故无法在此环境中完成真实浏览器控制台与悬停复核。交付内的 `server.cjs`、SPA fallback 与打开说明已备妥，需在本地环境复核该项。
- 未执行 GitHub 推送、Netlify 发布或其他外部操作。
- 本轮本地增量：Topline 新增 FY2025 实际与 FY2026 公司指引上限、UBS 预测的收入/GMV年度对比图；Bottomline 在 FY2025 右侧新增 UBS 与市场一致预期的 FY2026 Adjusted EBITDA 浅色预测柱。FY2026 Topline 金额按 FY2025 实际值乘以对应增长率计算，预测值不并入历史实际季度序列。
- 本轮本地验证：Node 脚本语法检查、预览页面真实浏览器打开、Topline/Bottomline 截图及预测柱显示均通过；控制台仅有本地 favicon 404，不影响页面交互。未执行任何外部推送。
- 本轮本地布局调整：Topline 年度预测图已并入左侧财务卡，与季度实际图共同呈现；删除 Topline 左侧预测表格及提示框，预测口径与计算值改为右侧核心观点文字说明。Bottomline 预测表格保持不变。
- 本轮本地文案调整：Topline 公司指引与 UBS 预测合并为右侧最下方的公司 / 券商观点，并删除按 FY2025 实际值计算的过程说明句；Bottomline 删除左侧预测卡片，并将市场一致预期 9.39 亿欧元补充至原 UBS 券商观点。
