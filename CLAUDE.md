# 六级词汇按词义划分

单文件静态学习页：`六级词汇按词义划分.html`（948 KB，6922 行，UTF-8 with BOM）。
结构：`<style>` 在 5–87 行，12 个 `.domain` / 305 个 `.group` / 5637 个 `.entry`，JS 在 6751 行起。
9 个 PDF 是源材料，已在 `.gitignore` 中排除（`*.pdf`），不入库。

## 编辑须知

- 文件超 Read 工具上限：用 `grep -n` 定位 + `Read offset/limit`，不要整读。
- 每次 Edit 后跑 `git diff --stat`：Edit 会把 CRLF 改写成 LF，可能出现整文件伪 diff。
- `.domain` 上的 `content-visibility: auto` 是释义总开关流畅的前提（否则全文档重排约 600ms），勿删。
- 打印样式在 `@media print` 里覆盖：强制释义展开、隐藏总开关。

## 行为约定（勿"修正"）

- 点单词：首次只记录 + 预加载音频，**不发音**；再次点才朗读。
- 关闭释义只能由右上角总开关触发；点已展开的词只重读。
- 发音主路径：`https://dict.youdao.com/dictvoice?audio=<词>&type=2`（type=2 = 美音），失败回落 speechSynthesis。

## 验证

- 渲染：`msedge --headless --screenshot` 截图对比，布局不能因性能优化而变。
- 交互：往 DOM 里注入桩脚本后用 `--dump-dom` 断言类名与调用序列。
- 音频：headless 无法验证（无用户手势 → `NotAllowedError`），需人工点击确认。
