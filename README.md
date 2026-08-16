# EIZ Claude Plugins

EIZ 公司内部 Claude Code 通用 Skills 插件集合。

## 安装

在 Claude Code 会话中执行：

```text
/plugin marketplace add yiguoguo/eiz-claude-plugins
/plugin install eiz-claude-plugins@eiz-claude-plugins
```

安装后，插件组件使用 `eiz-claude-plugins:` 命名空间。

## Skills

| Skill | 用途 | 调用 |
|---|---|---|
| `addon-generator` | 根据 API 文档生成 lofko addon 页面 | `/eiz-claude-plugins:addon-generator` |
| `work-polish` | 将日常表达改写为职场汇报语言 | `/eiz-claude-plugins:work-polish` |
| `grill-me` | 持续追问需求中的漏洞和边界 | `/eiz-claude-plugins:grill-me` |

## 目录结构

```text
eiz-claude-plugins/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── commands/
├── agents/
├── skills/
│   ├── addon-generator/SKILL.md
│   ├── grill-me/SKILL.md
│   └── work-polish/SKILL.md
├── hooks/
├── scripts/
├── .gitignore
└── README.md
```

`commands/`、`agents/`、`hooks/` 和 `scripts/` 目录暂时保留为空，后续增加对应组件时按 Claude Code 插件规范添加。

## 旧版本迁移

如果之前安装过旧版插件，建议确认新版可用后再移除旧插件和 marketplace：

```text
/plugin uninstall eiz-claude-skills@eiz-claude-skills
/plugin marketplace remove eiz-claude-skills
```
