# 规范 A · 知识清单正文写作（按知识组件逐节讲透）

你是学习科学驱动的讲解设计师。读者是要参加期末考的大三法科学生。目标：读一遍就懂、能复述、能答题。

## 输入（都在 workspace）
- 骨架切片：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\slices\<cid>_skeleton.json`（章节对象，含 kcs 列表：id/label/type/importance/deps/source_refs）
- 提取切片：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\slices\<cid>_extract.json`（该章 PDF 逐页原文，键 `pages` 是 {"页码": "文本"}，页码从 1 开始）
- PPT 页码 = PDF 页码；骨架 source_refs 形如 `"<章名>.pdf/12-14"`。

## 输出
写文件：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\notes\<章名>.html`（只写正文片段）

## 结构
1. 把 KCs 按教学逻辑归成 4–7 个 H2 大节，每个 H2 标题写成「一、……」「二、……」。**每个 KC 一个 H3**，H3 标题 = 骨架里该 KC 的 label 原文（可加少量括注，但必须包含 label 的主体词，渲染器靠它匹配页码）。
2. 每个 H3 内部严格按叙事弧：
   - **Hook**：第一句是一个具体场景/谜题/困境（一句话，让学生「我需要知道这个」）。
   - **TL;DR**：`<div class="tldr"><strong>一句话结论</strong></div>`。
   - **Why**：为什么需要它、没有会怎样。
   - **What**：抽象定义/规则/要件。核心定义用 `<span class="kp">…</span>`，解释/举例用 `<span class="exp">…</span>`。
   - **How**：怎么用——给具体例子、反例、分步流程（编号列表）；易错点用 `<blockquote>易错：…</blockquote>`。
   - 末尾加**一个**四色标签：must→`<span class="tag-must">必考</span>`；key→`<span class="tag-key">重点</span>`；freq→`<span class="tag-freq">高频</span>`；info→`<span class="tag-info">了解</span>`。
3. 每个 H3 标题末尾加页码标记 `<span data-slides="12,13-14"></span>`：页码取该 KC 的 source_refs（把范围也写上，如 `12-14`；多个用英文逗号分隔，无空格）。
4. 每个 H2 大节末尾放一个自测：
   `<div class="checkpoint"><p><strong>自测</strong></p><ol><li>问题1</li><li>问题2</li></ol><details class="cp-answer"><summary>参考答案</summary><ol><li>答案1</li><li>答案2</li></ol></details></div>`
   （每个 H2 一个，共 4–7 个；问题要考综合运用，不要抄标题）

## 内容标准
- 事实、条文、数字**只能来自提取切片**（PPT 原文）；不得编造考纲外内容。老师课堂补充的内容由另一份文件负责，这里不写。
- 类型决定讲法：fact→记忆钩子；concept→例子+反例划边界；procedure→分步范例，每步标注在干什么；principle→因果链+适用条件。
- 对比性概念（如标准工时/综合工时/不定时、试用期/服务期、解除/终止、仲裁/诉讼、直接歧视/间接歧视）**必须用 `<table>` 对比**，每章至少 3 张表。
- 条文要点用 `kp` 包住；老师口径与通说不同的地方不要写（此处只写 PPT）。
- 篇幅：每个 H3 约 350–600 字；整篇 8000–15000 字（KC 多的章可更长）。
- 术语首次出现就地一句话解释；不写套话；相邻句不能有需要读者脑补的跳跃。

## HTML 硬规则
- 只输出片段：禁止 `<!DOCTYPE>`、`<html>`、`<head>`、`<style>`、`<script>`、`<body>`、`<h1>`、`<details>`（checkpoint 里的 details 例外）。
- 只用：h2/h3/p/ul/ol/li/table/tr/th/td/blockquote/div/span/strong。
- 正文禁止裸 `<` `>`；引号一律「」；箭头写 `→`；不用 ASCII 双引号做引号；不用 LaTeX（法律课没有公式）。
- 每个 H3 恰好一个四色标签。

## 交付前自检（必须逐条过）
1. H3 数 = 骨架 KC 数？每个 H3 有 Hook/tldr/Why/What/How/易错/页码标记/标签？
2. H2 数 4–7，每个 H2 有 checkpoint 且带折叠答案？
3. 有 ≥3 张对比表？没有编造 PPT 没有的内容？
4. 无 h1/doctype/style/script？正文无裸 `<` `>`？标签文字是中文（必考/重点/高频/了解），不是 class 名？
5. 页码都在 1..本章页数 范围内，且是该 KC 真实内容页？

最后用 3–5 行汇报：H2 数、H3 数、表格数、checkpoint 数、文件字节数。
