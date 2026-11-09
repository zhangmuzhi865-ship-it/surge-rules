# surge-rules

Surge 远程规则集，按用途拆成多个 `.list` 文件，在 Surge 里按需订阅。

## 规则列表

| 文件 | 说明 | Surge 引用 |
| --- | --- | --- |
| `rules/ai.list` | AI 类：ChatGPT、Claude、Gemini、Grok、DeepSeek、Qwen、Kimi、豆包、智谱等聊天 / API 服务 | 见下方 |

## 用法

在 Surge 配置的 `[Rule]` 段加入：

```
RULE-SET,https://raw.githubusercontent.com/zhangmuzhi865-ship-it/surge-rules/main/rules/ai.list,PROXY
```

国内访问慢，可用 jsDelivr 镜像（同一个文件）：

```
RULE-SET,https://cdn.jsdelivr.net/gh/zhangmuzhi865-ship-it/surge-rules@main/rules/ai.list,PROXY
```

把结尾的 `PROXY` 换成你自己的策略组名即可，例如 `PROXY`、`美国节点`、`DIRECT`。

## 说明

- 每个 `.list` 都是纯文本规则，一行一条，`#` 开头为注释。
- 只含 AI 服务本身的域名，不含 `google.com`、`microsoft.com` 等通用域名，避免把无关流量也走代理。
- 不要往这个公开库里放节点、密码、私有域名，只放规则。
