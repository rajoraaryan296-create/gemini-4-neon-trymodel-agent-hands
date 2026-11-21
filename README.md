# Gemini 4 Neon 上线 Trymodel：编程 Agent 成绩领先，网页里直接实测

2026 年 11 月 18 日，Google DeepMind 发布了 Gemini 4 Neon。官方博客 [Introducing Gemini 4 Neon](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/) 给它的定位很明确：把前沿级智能，和把一项复杂任务从头到尾做完的速度放在一起，面向软件工程、知识工作和科学研究。

现在也可以直接在第三方平台 [Trymodel](https://trymodel.chat/zh) 里选用。Trymodel 不是 Google 或 Gemini 的官方网站，而是一个把多家模型放在同一界面里用的产品。Gemini 4 Neon 需要 Pro 套餐。打开中文入口 [https://trymodel.chat/zh](https://trymodel.chat/zh)，在对话页顶部点开模型名称，列表里它在 Gemini 4 Argon 和 Gemini 4 Hydrogen 之间。

![在 Trymodel 模型列表里，Gemini 4 Neon 位于 Argon 和 Hydrogen 之间](https://upload.maynor1024.live/file/1795244964274_01-model-picker.png)

选中后，输入框上方会显示 Gemini 4 Neon，就可以直接开聊。

![聊天页已选中 Gemini 4 Neon，可以开始输入](https://upload.maynor1024.live/file/1795244967365_02-model-selected.png)

## 官方跑分：19 项里领先 16 项

标题里的成绩，对应的是 Google 公开对比表，对手是 Claude Opus 5.5 和 GPT-6.2 Sol。评测方法说明在 [Gemini 4 Neon evals methodology](https://deepmind.google/models/evals-methodology/gemini-4-neon)。下面按公开数字整理，不改写。

| 评测 | Gemini 4 Neon | Claude Opus 5.5 | GPT-6.2 Sol |
| --- | --- | --- | --- |
| AA Index v5.0.1 | 61 | 59 | 57 |
| Vals Index v2.2 | 70.9% | 70.1% | 66.1% |
| CursorBench 4.1 | 65.4% | 58.1% | — |
| Terminal-bench 4.1（cheating-adjusted） | 65.2% | 65.8% | 61.5% |
| FrontierCode 2.0 main | 46.2% | 47.3% | 43.8% |
| SWE-sweep provider harness | 39.0% | 10.1% | 8.3% |
| SWE-sweep Mini-SWE harness | 12.8% | 3.6% | 11.6% |
| AutomationBench | 56.3% | 42.5% | 41.3% |
| Agents' Last Exam v1.1 | 75.8% | 71.6% | 73.0% |
| RiemannBench | 84.0% | 80.0% | 80.0% |
| Terminal-Bench-Science 0.1 | 70.5% | 63.3% | 68.0% |
| HLE-Diamond | 71.3% | 67.9% | 64.0% |
| MKA Climb WSR | 56.5% | 53.0% | 52.7% |
| Chartography | 73.5% | 66.3% | 75.1% |
| LVBench | 89.0% | 83.7% | 87.6% |
| GraphWalks 256k to 1M BFS F1 | 95.2% | 66.8% | 80.1% |
| CWE-Bench v2 | 70.7% | 67.1% | 66.0% |
| SEC-bench Pro | 90.5% | — | 88.3% |
| WebExploitBench v1.2 | 51.3% | 37.1% | — |

按表中 19 行逐项看，Gemini 4 Neon 领先 16 项。没有拿下的 3 项是：Terminal-bench 4.1（cheating-adjusted）上 Claude Opus 5.5 为 65.8%，略高于 Neon 的 65.2%；FrontierCode 2.0 main 上 Opus 5.5 为 47.3%，略高于 Neon 的 46.2%；Chartography 上 GPT-6.2 Sol 为 75.1%，高于 Neon 的 73.5%。

另外两项官方成绩也值得记下。根据 [Gemini 4 Neon in Google Antigravity](https://antigravity.google/blog/gemini-4-neon-in-google-antigravity/)，Artificial Analysis Coding Agent Index 上 Gemini 4 Neon 以 58.6 分排在第 1；Intelligence Index 在 xhigh thinking 下得到 61 分，总榜第 3，和表中第一行的 AA Index v5.0.1 对得上。

按官方分层，Carbon 对应更难、跨度更长的工作，Hydrogen 偏向日常快速协助，Neon 则是在深度和效率之间取平衡。

## 在 Trymodel 里实测一道编码题

为了看它在网页对话里的实际表现，我们在 [Trymodel](https://trymodel.chat/zh) 新建对话，选中 Gemini 4 Neon，出了下面这道题：写一个合并重叠区间的 Python 函数，只要求函数、两行短注释和 3 个 assert，不要长说明。

> 写一个 Python 函数 merge_intervals(intervals)，把可能重叠的闭区间合并成不相交区间。输入如 [[1,3],[2,6],[8,10],[15,18]]，应返回 [[1,6],[8,10],[15,18]]。只给函数、两行简短注释，以及 3 个 assert 示例。不要写长说明。

![在 Trymodel 中向 Gemini 4 Neon 发送合并区间的编程题](https://upload.maynor1024.live/file/1795244971360_06-coding-prompt.png)

模型思考了 17.0 秒后给出完整代码，一次写完函数、注释和断言，没有再补长篇说明。截图里第一行 assert 因为代码块较宽，右侧被滚动条挡住了一点，完整文本如下。

![Gemini 4 Neon 思考 17 秒后返回 merge_intervals 函数和三条断言](https://upload.maynor1024.live/file/1795244969401_07-coding-result.png)

```python
def merge_intervals(intervals):
    if not intervals:
        return []
    # 按区间起点升序排序
    sorted_intervals = sorted(intervals, key=lambda x: x[0])
    merged = [sorted_intervals[0][:]]
    # 遍历并合并重叠的闭区间
    for start, end in sorted_intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    return merged

assert merge_intervals([[1, 3], [2, 6], [8, 10], [15, 18]]) == [[1, 6], [8, 10], [15, 18]]
assert merge_intervals([[1, 4], [4, 5]]) == [[1, 5]]
assert merge_intervals([]) == []
```

这段实现会先按起点排序，再依次合并重叠或首尾相接的闭区间。三条断言分别覆盖了题目给出的例子、首尾相接的区间，以及空输入。

## 在 Trymodel 怎么用

在 Trymodel 里，Gemini 4 Neon 需要 Pro 套餐，按实际用量扣积分。想自己试一次，打开 [https://trymodel.chat/zh](https://trymodel.chat/zh)，在模型列表里选中 Gemini 4 Neon 即可。
