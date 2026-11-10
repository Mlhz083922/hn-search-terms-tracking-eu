# HN Search Terms Tracking EU 只读站

把 `docs/` 目录发布到 GitHub Pages，供团队只读查看**亚马逊德国站（DE）**女装泳装关键词的 ABA 排名与搜索量数据。

本仓库与 `hn-search-terms-tracking`（美国站）**完全独立**：独立仓库、独立 Pages、独立浏览器缓存（IndexedDB / localStorage 键名均带 EU 后缀），互不影响。

- 数据源：本机亚马逊运营工作台（8767）的 DE 热搜词追踪模块 `/Users/yang/amazon-workbench/app/public/hotsearch-de`
- 数据目录：`/Users/yang/amazon-workbench/data/搜索词Data-DE/运行数据`（可用环境变量 `HOTSEARCH_DE_DATA_DIR` 覆盖）

## 首次启用（一次性）

1. 打开仓库 `Settings → Pages`，`Source` 选择 **Deploy from a branch**，分支选 `main`，目录选 `/docs`，保存。
2. Pages 部署完成后，团队共享链接为：

   https://mlhz083922.github.io/hn-search-terms-tracking-eu/

3. 推送凭据：把 GitHub Token 写入 `~/.config/hn-search-terms-tracking-eu/github-credentials`，格式：

   ```
   https://Mlhz083922:<你的TOKEN>@github.com
   ```

   （与美国站的 `~/.config/hn-search-terms-tracking/github-credentials` 互不影响）

## 更新数据快照

主站 DE 页面顶部有「更新团队链接」按钮，点击后自动完成下面三步；也可以手动执行：

1. 在本地主站完成编辑后，重新生成只读快照：

   ```bash
   node build-readonly.mjs
   ```

2. 提交并推送 `main` 分支：

   ```bash
   git add -A
   git commit -m "update EU read-only snapshot"
   git push origin main
   ```

GitHub Pages 会自动重新发布，网址保持不变。

## 访问密码

只读站密码与主站一致：`HN2026`（24 小时内免重复验证）。
如需修改：`node -e "console.log(require('crypto').createHash('sha256').update('新密码').digest('hex'))"`
生成新哈希，替换 `build-readonly.mjs` 顶部的 `READONLY_PASSWORD_HASH`，重新 build 并推送。
