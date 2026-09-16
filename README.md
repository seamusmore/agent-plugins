# agent-plugins

Seamus 的 Codex 插件市场。各插件在独立仓库维护，本仓库提供统一目录和安装入口。

## 当前状态

市场已初始化，插件列表为空。插件将于适配和验证完成后逐项登记。

- 市场标识：`seamusmore`
- 显示名称：`Seamus Plugins`
- 索引文件：`.agents/plugins/marketplace.json`

## 添加市场

在支持插件管理的 Codex CLI 中执行：

```powershell
codex plugin marketplace add seamusmore/agent-plugins --ref main
```

插件上架后，使用实际插件名称安装：

```powershell
codex plugin add <plugin-name>@seamusmore
```

安装后开启新任务，以加载插件。当前空目录尚无可安装插件。

刷新市场目录：

```powershell
codex plugin marketplace upgrade seamusmore
```

## 登记插件

1. 在插件独立仓库中准备有效的 Codex 插件清单和所需文件。
2. 在市场索引的 `plugins` 数组中追加条目，名称与插件清单一致。
3. 指定 Git 仓库来源；根目录插件使用 `source: "url"`，子目录插件使用 `source: "git-subdir"`。
4. 明确填写 `policy.installation`、`policy.authentication` 和 `category`。发布条目优先固定到已验证的版本标签或提交 SHA。
5. 验证 JSON、来源引用及实际安装结果，再合并目录更新。

插件源码、测试和版本发布由各自仓库管理。

## 参考

- [Codex 插件打包与市场配置](https://developers.openai.com/plugins/build/plugins)
- [Codex Hooks](https://learn.chatgpt.com/docs/hooks)
