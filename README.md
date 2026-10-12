# Muvyo 插件仓库

这是一个 Muvyo 第三方插件仓库。在 Muvyo「第三方插件 → 插件仓库」添加本仓库地址（`https://github.com/<你的用户名>/<仓库名>`），即可安装下面的插件。

当前插件：

| 插件 ID | 名称 | 说明 |
|---|---|---|
| `ks526.metatube` | MetaTube 刮削 | 把自建 MetaTube 服务接入 Vyo 媒体库，作为第三方刮削来源 |

## 开发者

**推荐 `src/` 不要上传。** 本地同一个目录里保留 `src/` 开发、`plugins/` 发布即可，不必额外维护分支或拆分仓库。模板已忽略 `src/`，这部分源码不会进入本仓库的 Git 历史或备份到 GitHub，请自行备份。

- 源码放 `src/<插件ID>/`（manifest.json、入口 JS、README.md），只留本地或独立私有开发仓库
- 签名凭据 `muvyo-signing.json`、签名脚本 `mv_addon.py` 放在仓库根目录，不提交
- 第一次克隆后启用提交检查：`git config core.hooksPath .githooks`
- 签名：`python3 mv_addon.py sign ./src/<插件ID> -o .`
- 只发布加密签名产物，不使用 `--no-encrypt`；不要移除 `src/` 忽略规则或根据许可证名称上传源码
- 仓库签名：首次用 `python3 .claude/skills/muvyo-addon-publish/scripts/sign_index.py init-key --key repo-signing.pem` 创建仓库专用私钥（仅限索引尚无公钥）；已有仓库必须沿用原私钥。私钥不提交，并自行安全备份
- 插件签名完成后执行 `python3 .claude/skills/muvyo-addon-publish/scripts/sign_index.py sign --key repo-signing.pem`，再执行同一工具的 `verify` 子命令验证索引签名
- 提交：`git add -A index.json index.json.sig plugins/<插件ID>`，再 commit、push；签名后改动索引必须重新签名

用 Claude Code 等 AI 编程工具时，直接说「发布插件」即可，按 `.claude/skills/muvyo-addon-publish` 的流程签名、检查并提交。

开发说明见 https://github.com/thsrite/muvyo-addon-guide