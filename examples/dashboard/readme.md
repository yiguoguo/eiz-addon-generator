# 需求

根据 api.md 中的 API 文档，生成一个 Dashboard 图表页面，展示：

- 近30天销售趋势折线图
- 今日/本周/本月/本季度销售额卡片

# 使用方式

1. 调用 skill：
   ```
   /addon-generator 参考 examples/dashboard/api.md --deploy --name eiz-dashboard
   ```

2. 部署前提条件：需要先安装 [Vercel CLI](https://vercel.com/cli) 并登录
   ```bash
   npm i -g vercel && vercel login
   ```

3. 部署完成后，返回 Vercel 分配的地址（例如：`https://eiz-dashboard-xxx.vercel.app`）

4. 将部署地址反馈给系统管理员，添加到Addon系统