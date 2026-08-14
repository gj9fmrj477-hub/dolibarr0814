# Autonoma Planner CI（Dolibarr）

本仓库是 `Dolibarr/dolibarr` 的 fork。GitHub Actions 会 checkout **本仓库全量源码树**（浅历史），并运行 Autonoma Planner 生成测试用例。

## 分支

- 默认上游分支：`develop`
- CI 工作流所在分支：`autonoma-ci`

## 配置 Secrets

仓库 → **Settings → Secrets and variables → Actions**，添加：

| Secret | 必填 | 说明 |
|--------|------|------|
| `AUTONOMA_API_TOKEN` | 是 | Autonoma → Settings → API keys |
| `AUTONOMA_APPLICATION_ID` | 是 | 建议新建 Dolibarr 专用 App 的 ID |
| `AUTONOMA_GENERATION_ID` | 是 | 控制台「Upload test artifacts」命令里的 generation id |
| `AUTONOMA_SHARED_SECRET` | 否 | App Shared Secret |
| `ANTHROPIC_API_KEY` | 否 | 仅当 `coding_agent=claude` 时需要 |

建议在 Autonoma 新建应用并关联本仓库：`gj9fmrj477-hub/dolibarr0814`。

## 触发

1. 打开 **Actions** → **Autonoma Planner · Dolibarr full scan**
2. **Run workflow**，选分支 `autonoma-ci`
3. 推荐首次：`coding_agent=none`（只扫代码生成套件）；`fresh` 按需勾选

Dolibarr 体量大，单次可能 **1 小时+**，并消耗较多 credits。

## 说明

- 生成用例 ≠ 执行用例；浏览器执行仍需公网预览 URL + deployment-signal。
- 工作流默认 `coding_agent=none`，避免缺 Claude key 导致整次失败。
