# Mercury Commerce Dashboard

基于 `cleaned_ecommerce_dataset.csv` 构建的交互式电商经营仪表盘。页面中的每个数字都来自 CSV 字段计算，不补造渠道、流量、成本、利润、库存或目标字段。

## 功能

- 日期、品类、城市、支付方式和时间粒度全局筛选
- GMV、paid 订单量、客单价、复购率、退款率、取消率实时联动
- 日、周、月趋势切换，以及上周期对比
- 品类、城市、支付方式和订单状态图表
- 履约天数与评分关系分析
- 新客与复购订单结构
- 订单明细搜索、排序、分页、导出和详情抽屉
- 数据质量检查与异常记录排除视图
- 浅色和深色主题
- 筛选状态同步到 URL，可直接分享当前视图

## 数据口径

- GMV、订单量、客单价、复购率、新客占比：仅统计 `status = paid`
- 取消率、退款率：按全部去重订单号计算
- 平均评分：所有存在评分的订单
- 平均配送天数：paid 订单中存在配送天数的记录
- 日期缺失记录保留在总量和数据质量面板中，但不参与时间趋势
- 默认口径不删除异常记录；页面可切换排除异常并实时重算

## 本地运行

```bash
npm install
npm run verify:data
npm run typecheck
npm run dev
```

打开 `http://localhost:3000`。

生产构建：

```bash
npm run build
```

静态文件输出到 `out/`。

## 项目结构

```text
app/                     Next.js App Router 页面与全局样式
components/dashboard.tsx 仪表盘主界面与图表配置
components/orders-table.tsx 订单表格
data/                    CSV 数据源
lib/data.ts              CSV 解析、Zod 校验与数据质量标记
lib/metrics.ts           指标、趋势与维度聚合
scripts/verify-data.mjs  数据基线与质量检查
```

## 部署

项目使用 Next.js 静态导出，可直接部署到 Vercel。生产分支更新后执行：

```bash
npx vercel --prod
```

也可以将 GitHub 仓库连接到 Vercel，由 Vercel 在 `main` 分支更新时自动执行生产部署。
