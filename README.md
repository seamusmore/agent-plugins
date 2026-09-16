# agent-plugins

Seamus 的 Codex 插件市场。插件在独立仓库维护，本仓库提供统一目录和安装入口。

## 安装

```powershell
codex plugin marketplace add seamusmore/agent-plugins --ref main
codex plugin marketplace upgrade seamusmore
codex plugin add rtk-rewrite@seamusmore
```

安装后按 Codex 提示审核并信任插件 hook，开启新任务加载。

## 插件

| 插件 | 版本 | 用途 |
|---|---|---|
| [rtk-rewrite](https://github.com/seamusmore/rtk-rewrite) | 1.3.1 | 原生 PreToolUse hook 自动通过 RTK 改写简单终端命令；要求 Python 3.10+ 和 RTK 位于 PATH |

RTK 条目固定到已验证的提交 `de2c3c66ccdcbbee33690e417f4227210e5622b5`。市场 PR 应在该插件修复提交审核合并后合并。
PowerShell 继续作为执行 shell；包含管道、变量和复合控制语法的命令保留原样。
统计直接使用 `rtk gain`。Hermes 继续使用同一插件仓库的原生入口。

Windows 沙箱运行条件见插件 README：RTK 0.42.0 存在用户目录解析失败问题；本机验收使用独立 RTK 0.49.0 和真实 `CLAUDE_CONFIG_DIR`。只读沙箱会限制统计数据库写入，需单独授权数据目录权限后持久化统计。

## 登记和更新

1. 在独立插件仓库完成代码审核和验证。
2. 在 `.agents/plugins/marketplace.json` 的 `plugins` 数组追加条目，名称与插件清单一致。
3. 仓库根目录插件使用 `source: "url"`，子目录插件使用 `source: "git-subdir"`；优先固定已审核的提交 SHA。
4. 包含 `policy.installation`、`policy.authentication` 和 `category`。
5. 验证目录解析、实际安装及 hook 加载，通过 PR 交由仓库所有者审核合并。

市场标识为 `seamusmore`，显示名称为 `Seamus Plugins`。
主分支保护与 `.github/CODEOWNERS` 负责所有者审核；绕过权限由所有者保留。

## 参考

- [Codex 插件与市场配置](https://developers.openai.com/plugins/build/plugins)
- [Codex Hooks](https://learn.chatgpt.com/docs/hooks)
