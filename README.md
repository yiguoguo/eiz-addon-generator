# EIZ Claude Plugins

公司内部 Claude Code 插件集合，包含可复用 skills 和 EIZ Remote MCP 使用手册。

## 安装

在 Claude Code 会话中执行：

```bash
/plugin marketplace add yiguoguo/eiz-claude-plugins
/plugin install eiz-claude-plugins@eiz-claude-plugins
```

安装完成后，插件中的 skill 使用 `eiz-claude-plugins:` 命名空间。

如果之前安装过旧版 `eiz-claude-skills`，建议先安装新版并确认可用，再移除旧 marketplace：

```text
/plugin uninstall eiz-claude-skills@eiz-claude-skills
/plugin marketplace remove eiz-claude-skills
```

## MCP 配置

插件根目录的 `.mcp.json` 已内置 EIZ Remote MCP，无需手动执行 `claude mcp add`：

```text
https://eiz-mcp.wangyii.org/mcp
```

首次使用 MCP 时：

1. 在 Claude Code 中运行 `/mcp`。
2. 选择 `eiz-mcp`，完成 OAuth 授权。
3. 如果刚安装插件后没有看到 MCP，运行 `/reload-plugins` 或重启 Claude Code。

授权完成后，Claude Code 会根据 MCP Server 当前提供的工具进行搜索和调用。MCP 工具名称以当前会话显示的名称为准，不要使用其他客户端中的旧工具名。

## Skills

### `/eiz-claude-plugins:addon-generator` — 接口文档转页面

根据 API 文档自动生成 lofko addon 页面，Claude 根据接口结构自动判断页面类型（表格/卡片/详情/图表），生成完整 Next.js + Tailwind 项目，可选 Vercel 一键部署。

```
/eiz-claude-plugins:addon-generator https://petstore.swagger.io/v2/swagger.json --deploy
/eiz-claude-plugins:addon-generator 一个商品库存查询接口，GET /api/inventory，返回商品名、SKU、数量、价格
```

<details>
<summary>页面类型自动推断规则</summary>

| 接口返回特征 | 页面类型 |
|---|---|
| 数组 + 标量字段 | 数据表格 |
| 数组 + 图片/标题/价格 | 卡片网格 |
| 单对象 + 多字段 | 详情页 |
| 数值/统计字段 | Dashboard 图表 |

</details>

<details>
<summary>lofko addon 工作流程</summary>

1. 管理员在 lofko 后台注册 addon，填入部署 URL
2. 用户点击 addon，lofko 自动追加 `?token=xxx`
3. 页面用 token 请求后端接口（`Authorization: Bearer <token>`）

</details>

---

### `/eiz-claude-plugins:work-polish` — 职场语言包装

大白话变专业汇报语言，两种力度可选。

```bash
/eiz-claude-plugins:work-polish --轻度 帮老王改了登录页面的颜色
/eiz-claude-plugins:work-polish --重度 明天要上线但还有 3 个 bug 没修完
```

**轻度**（日常周报）：
> 输入：帮老王改了登录页面的颜色
> 输出：协助前端完成登录模块的视觉优化，提升界面一致性

**重度**（向上汇报）：
> 输入：明天要上线但还有 3 个 bug 没修完
> 输出：项目已进入上线冲刺阶段，核心功能验证完毕，剩余 3 项非阻塞性问题正在并行修复，不影响主链路交付

- **轻度**：加 2-3 个术语，见好就收，适合日常周报
- **重度**：拉满，PPT 标题级输出，适合向上汇报

---

### `/eiz-claude-plugins:grill-me` — 需求拷问

每轮问 2-3 个具体问题，持续挖掘需求里的漏洞、边界情况和隐含假设，直到确认没有歧义，最后输出结构化需求确认清单。

```bash
/eiz-claude-plugins:grill-me 做一个商品管理后台
/eiz-claude-plugins:grill-me 接入微信支付
```

---

### `/eiz-claude-plugins:eiz-mcp-guide` — EIZ Remote MCP 使用手册

项目内置 `eiz-mcp` Remote MCP 配置，地址为：

```text
https://eiz-mcp.wangyii.org/mcp
```

首次使用时运行 `/mcp`，完成 OAuth 授权。授权后，Claude Code 会根据 MCP Server 当前提供的工具进行搜索和调用。

使用手册：

```text
/eiz-claude-plugins:eiz-mcp-guide
```

## 示例

`examples/` 目录包含可直接作为 `/eiz-claude-plugins:addon-generator` 输入的示例：

- [examples/dashboard/](examples/dashboard/) — Dashboard 图表页面
