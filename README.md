# surge-rules

Surge 远程规则集，按用途拆成多个 `.list` 文件，在 Surge 里按需订阅。

## 规则列表

| 文件 | 说明 | 建议策略 |
| --- | --- | --- |
| `rules/ai-foreign.list` | AI 国外：ChatGPT、Claude、Gemini、Grok、Perplexity、Mistral、Meta AI 等 | PROXY |
| `rules/ai-domestic.list` | AI 国内：DeepSeek、Qwen、Kimi、豆包、智谱、文心、MiniMax 等 | DIRECT |
| `rules/apple-ai.list` | Apple AI：Private Cloud Compute 与 Siri 相关专用域名 | 见下方 |

## 用法

在 Surge 配置的 `[Rule]` 段加入：

```
RULE-SET,https://raw.githubusercontent.com/zhangmuzhi865-ship-it/surge-rules/main/rules/ai-foreign.list,PROXY
RULE-SET,https://raw.githubusercontent.com/zhangmuzhi865-ship-it/surge-rules/main/rules/ai-domestic.list,DIRECT
RULE-SET,https://raw.githubusercontent.com/zhangmuzhi865-ship-it/surge-rules/main/rules/apple-ai.list,DIRECT
```

国内访问慢，可用 jsDelivr 镜像（同一个文件），把上面链接换成：

```
RULE-SET,https://cdn.jsdelivr.net/gh/zhangmuzhi865-ship-it/surge-rules@main/rules/ai-foreign.list,PROXY
RULE-SET,https://cdn.jsdelivr.net/gh/zhangmuzhi865-ship-it/surge-rules@main/rules/ai-domestic.list,DIRECT
RULE-SET,https://cdn.jsdelivr.net/gh/zhangmuzhi865-ship-it/surge-rules@main/rules/apple-ai.list,DIRECT
```

把结尾的 `PROXY` / `DIRECT` 换成你自己的策略组名即可。

Apple AI 注意：`apple-ai.list` 的策略按位置定。在中国大陆想用 Apple Intelligence，PCC 常需走海外节点才能通过 IP 检查，此时把 `DIRECT` 换成你的海外策略组；在境外、Apple Intelligence 本来就能用的地方，用 `DIRECT` 即可。

## 说明

- 每个 `.list` 都是纯文本规则，一行一条，`#` 开头为注释。
- 只含相关服务本身的域名，不含 `google.com`、`microsoft.com`、`apple.com` 等通用域名，避免把无关流量也带走。
- 不要往这个公开库里放节点、密码、私有域名，只放规则。

## 维护

AI 厂商会加新域名、新 API 地址，也会下线旧域名。某个 AI 突然连不上了、或者开始用新的 AI 服务时，告诉我一声，我来更新对应的 `.list`；也可以定期让我检查一次。
