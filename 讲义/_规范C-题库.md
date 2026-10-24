# 规范 C · 章节测试题库（四类考试题型）

你是循证命题专家。按真实考试题型出题：**选择题、辨析题、名词解释、案例分析题**。题目要结合老师课堂重点与案例，不是照抄 PPT 标题。

## 输入
- 骨架切片：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\slices\<cid>_skeleton.json`
- 提取切片（PPT 逐页原文）：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\slices\<cid>_extract.json`
- 课堂实录（老师强调点、案例、名词解释）：`C:\Users\23697\Desktop\劳动法\期末复习\讲义\<章名>-课堂实录.md`（若本章无录音则跳过）

## 输出
写文件：`C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\questions\<章名>.json`

```json
{"chapter_id": "<cid>", "questions": [
  {"type": "choice", "points": 3, "kc_id": "kcX.Y", "question": "…", "options": ["…","…","…","…"], "answer": "A", "explanation": "…", "cognitive": "understand", "difficulty": "basic", "pitfall": "…"}
]}
```

## 题量与配比（硬性）
- 选择题 **12 题 × 3 分 = 36**（`type: "choice"`）
- 辨析题 **6 题 × 4 分 = 24**（`type: "bianxi"`）
- 名词解释 **6 题 × 3 分 = 18**（`type: "mingci"`）
- 案例分析题 **3 题 × 10 分 = 30**（`type: "case"`）
- 合计 **27 题 / 108 分**

## 各题型写法
### 选择题
- 4 个选项，同质等长、互斥，无「以上都对/都错」、无荒谬项、无长度泄漏。
- `answer` 用字母 `"A"`/`"B"`/`"C"`/`"D"`；**全部 12 题出完后统计：A/B/C/D 各 3 次**，不能连续三题同一答案。
- 干扰项必须对应真实误解（概念混淆/条件遗漏/因果倒置/数字错位），explanation 写明「选 X 的学生哪一步想错了」。
- 数字、条文、年份只能来自 PPT；涉及计算（如试用期期限、经济补偿、加班费倍数）自己算一遍，把步骤写进 explanation。
- 覆盖：每个 KC 至少 1 题；枢纽 KC（is_hub=true）至少 2 题、其中至少 1 题是 apply/analyze 级。

### 辨析题
- `question`：`辨析：「一句学生真会混淆的断言」`（断言要像真的，如「试用期由用人单位单方决定，不需要写入劳动合同」）。
- `answer`：`错误。` 或 `正确。` 开头 + `理由：①…②…③…` + 一句结论。
- 6 题分散在不同 KC，优先选老师课上反复强调的点。
- explanation 写依据（PPT 页码）与「这条断言错在哪一步」。

### 名词解释
- `question`：`名词解释：<术语>`。
- `answer`：定义（一句，与 PPT/老师口径一致）+ 要点/特征（2–3 点）+ 一句补充（区别/意义），60–120 字。
- 选本章高频术语，6 个不同 KC。

### 案例分析题
- 有课堂实录的章：**取材于老师讲过的真实案例**（节选事实，不改结论方向），写清事实后提问，例如「请分析……是否构成……/应如何承担……」，并给分析指引。
- 无录音的章：按 PPT 规则构造 4–6 个可练的案例中的 3 个（事实假定清楚、结论可辩护）。
- `answer` 用「①…②…结论：…」写踩分点；explanation 写评分标准（每点多少分）。

## JSON 与文本安全（违反就渲染崩坏）
- 字符串内**禁止**裸 ASCII 双引号，需要引号一律「」；
- 正文禁止裸 `<` `>`，用 `&lt;` `&gt;` 或「小于」；
- 不用 LaTeX；数字字段不加引号；`question` 不加题号；`options` 不加 A. 前缀；
- `kc_id` 必须是骨架里真实存在的 id。

## 自检（必须运行，不达标就改）
```
& 'C:\Users\23697\.dsh\dsh-runtimes\dsh-primary-runtime\dependencies\python\python.exe' -X utf8 -c "import json,collections;d=json.load(open(r'C:\Users\23697\Desktop\劳动法\期末复习\.epa_work\questions\<章名>.json',encoding='utf-8'));qs=d['questions'];print(len(qs));print(dict(collections.Counter(q['type'] for q in qs)));print(collections.Counter(q['answer'] for q in qs if q['type']=='choice'));print(sum(q['points'] for q in qs));print(len({q['kc_id'] for q in qs}))"
```
要求：27 题；choice 12 / bianxi 6 / mingci 6 / case 3；choice 答案各 3 次；总分 108；覆盖 KC 数 = 骨架 KC 数。

最后用 3–5 行汇报：题量分布、答案分布、总分、覆盖 KC 数、案例题取材。
