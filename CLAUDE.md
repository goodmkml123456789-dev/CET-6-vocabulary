# 六级词汇按词义划分

单文件静态学习页：`六级词汇按词义划分.html`（959 KB，7178 行，UTF-8 with BOM）。
结构：`<style>` 在 5–123 行，12 个 `.domain` / 305 个 `.group` / 5637 个 `.entry`，JS 在 6792 行起。
9 个 PDF 是源材料，已在 `.gitignore` 中排除（`*.pdf`），不入库。

## 编辑须知

- 文件超 Read 工具上限：用 `grep -n` 定位 + `Read offset/limit`，不要整读。
- 每次 Edit 后跑 `git diff --stat`：Edit 会把 CRLF 改写成 LF，可能出现整文件伪 diff。
- `.domain` 上的 `content-visibility: auto` 是释义总开关流畅的前提（否则全文档重排约 600ms），勿删。
- 打印样式在 `@media print` 里覆盖：强制释义展开、隐藏总开关。

## 行为约定（勿"修正"）

- 搜索高亮必须用 CSS Custom Highlight（`::highlight(vocab-hit)`），**不要插入 `<mark>` 或改写 entry 的 innerHTML**：在 5637 条 + `content-visibility` 的文档里这么做会让 Chrome 158 触发渲染 CHECK（STATUS_BREAKPOINT，chrome.dll+0xE53B520），表现为输入搜索词时偶发崩溃。
- 清空搜索（× / Esc / 删空）必须回到**搜索前的滚动位置**（`scrollBefore` 快照），不能停在文档开头。
- 组开关：组内任意一个展开就显示「隐藏本组」，点击全部收起；全关时显示「显示本组」，点击全部展开；只影响本组，文案随状态自动刷新。
- 点单词：首次只记录 + 预加载音频，**不发音**；再次点才朗读。
- 关闭释义只能由右上角总开关或本组开关触发；点已展开的词只重读。
- 发音主路径：`https://dict.youdao.com/dictvoice?audio=<词>&type=2`（type=2 = 美音），失败回落 speechSynthesis。

## 验证

- 渲染：`msedge --headless --screenshot` 截图对比，布局不能因性能优化而变。
- 交互：往 DOM 里注入桩脚本后用 `--dump-dom` 断言类名与调用序列。
- 用户实际用 Chrome 158（不是 msedge）；渲染/崩溃类问题必须在**有头 Chrome** 复现，headless Edge/Chrome 都不复现。Chrome 崩溃转储在 `%LOCALAPPDATA%\Google\Chrome\User Data\Crashpad\reports`。
- 音频：headless 无法验证（无用户手势 → `NotAllowedError`），需人工点击确认。
