# agent-plugins

Seamus 的 Codex 插件市场。插件在独立仓库维护，本仓库提供统一目录和安装入口。

## 安装

```powershell
codex plugin marketplace add seamusmore/agent-plugins --ref main
codex plugin marketplace upgrade seamusmore
codex plugin add rtk-rewrite@seamusmore
```

安装后按 Codex 提示审查并信任插件 hook，开启新任务加载。

## 插件

| 插件 | 版本 | 用途 |
|---|---|---|
| [rtk-rewrite](https://github.com/seamusmore/rtk-rewrite) | 1.3.2 | 原生 PreToolUse hook 自动通过 RTK 改写简单终端命令；要求 Python 3.10+ 和 PATH 中的 RTK；Windows 使用 PowerShell 和 RTK 0.49.0+ |

RTK 条目固定到提交 `801311c6dbbca42fdeb6b51eed22672d6df58475`。市场更新应在插件修复通过审查并合并后合并。
Windows 插件自行处理 RTK 的沙箱目录查询兼容问题，仅为本次子进程补齐路径并恢复已有环境；直接使用原安装的 RTK，全局 PATH、Claude 文件和 Codex 环境配置保持原样。
包含管道、变量和复合控制语法的命令保留原样。Windows 显式指定其他 shell 时保留原命令。
统计直接使用 `rtk gain`；只读沙箱仍限制统计数据库写入，持久统计需要单独授权数据目录写权限。
Hermes 继续使用同一个插件仓库的原有入口。

## 登记和更新

1. 在独立插件仓库完成代码审查和验证。
2. 在 `.agents/plugins/marketplace.json` 的 `plugins` 数组追加条目，名称与插件清单一致。
3. 仓库根目录插件使用 `source: "url"`，子目录插件使用 `source: "git-subdir"`；优先固定经过审查的提交 SHA。
4. 提供 `policy.installation`、`policy.authentication` 和 `category`。
5. 验证目录清单、实际安装和 hook 加载，通过 PR 交由仓库所有者审查合并。

市场标识为 `seamusmore`，显示名称为 `Seamus Plugins`。
主分支保护和 `.github/CODEOWNERS` 要求所有者审查，绕过权限由所有者本人保留。

## 参考

- [Codex 插件与市场文档](https://developers.openai.com/plugins/build/plugins)
- [Codex Hooks](https://learn.chatgpt.com/docs/hooks)
