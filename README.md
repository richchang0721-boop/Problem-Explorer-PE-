# Problem Explorer (PE)

A problem clarification tool. Explore your problem before asking AI.

問題釐清工具。在問 AI 之前，先搞清楚你真正的問題是什麼。

---

## Live Demo / 線上體驗

👉 https://richchang0721-boop.github.io/Problem-Explorer-PE-/

No API key required to try the example conversation.
不需要 API 金鑰，可直接體驗範例對話。

---

## What Problem Explorer Does / 這個工具做什麼

**EN**
Most people don't get useful answers from AI because they haven't defined their problem clearly.

Problem Explorer helps you clarify what you're really asking — before you ask AI.

It does not give answers.
It does not tell you what to decide.
It helps you see the structure of your own problem.

**中文**
大多數人從 AI 得到的答案沒有幫助，不是因為 AI 不夠強，而是因為問題本身沒有定義清楚。

Problem Explorer 幫助你在問 AI 之前，先把你真正的問題說清楚。

它不給答案。
它不告訴你該怎麼決定。
它幫你看清楚自己問題的結構。

---

## How It Works / 運作方式

**EN**
Problem Explorer uses a structured dialogue approach based on reverse RSTA logic.

Instead of tracking how AI output drifts, it tracks how clearly you have defined your problem.

The system asks questions. You answer. The questions come from what you've already said — not from AI assumptions.

When enough structure has emerged, the system outputs:

- What you described as your problem
- The current situation as you stated it
- The options you mentioned yourself
- The parts that are still unclear

The system never adds options you didn't mention.
The system never tells you which option is better.
The system stays neutral throughout.

**中文**
Problem Explorer 使用基於反向 RSTA 邏輯的結構化對話方式。

它不追蹤 AI 輸出的漂移，而是追蹤你對問題定義的清晰程度。

系統提問，你回答。問題來自你已經說過的內容，不是 AI 的假設。

當足夠的結構浮現後，系統輸出：

- 你描述的問題
- 你陳述的現況
- 你自己提到的選項
- 目前還不清楚的部分

系統不會加入你沒有提到的選項。
系統不會告訴你哪個選項比較好。
系統全程保持中性。

---

## Core Design Principles / 核心設計原則

**EN**

**1. Neutral by design**
The system does not evaluate your options, reinforce your biases, or suggest directions. All judgments stay with you.

**2. Your words, not AI words**
Every option and judgment in the output comes from what you said. The AI organizes — it does not invent.

**3. No forced convergence**
The system does not collapse your situation into a single answer. It preserves the structure of your decision space.

**4. Stops when you stop**
If you don't think you have a problem, the system stops. No pressure, no judgment.

**中文**

**1. 設計上的中性**
系統不評價你的選項，不強化你的既有偏見，不暗示方向。所有判斷留給你自己。

**2. 你的語言，不是 AI 的語言**
輸出裡的所有選項和判斷，來自你說過的內容。AI 負責整理，不負責發明。

**3. 不強迫收斂**
系統不把你的情況壓縮成單一答案。它保留你決策空間的結構。

**4. 你停它就停**
如果你認為自己沒有問題，系統停止。沒有壓力，沒有評判。

---

## Tracking Dimensions / 追蹤維度

**EN**
Problem Explorer tracks six dimensions of problem clarity during the conversation:

| Dimension | What It Detects |
|---|---|
| Problem Boundary | Is the problem specific and bounded? |
| Goal Clarity | Does the user know what they want to be different? |
| Agency | Does the user know what parts they can decide? |
| Emotional Attachment | Is strong emotion affecting how the problem is described? |
| Attribution Direction | Is the problem entirely attributed to external factors? |
| Avoidance Signal | Is the user deliberately vague about certain parts? |

The first three are actively pursued through questions.
The last three are only noted when clearly present — never forced open.

**中文**
Problem Explorer 在對話過程中追蹤六個問題清晰度維度：

| 維度 | 偵測內容 |
|---|---|
| 問題邊界 | 問題是否具體、有範圍？ |
| 目標清晰度 | 使用者是否知道自己希望什麼不一樣？ |
| 自主性 | 使用者是否知道哪些部分是自己能決定的？ |
| 情緒附著 | 強烈情緒是否影響了問題的描述方式？ |
| 歸因方向 | 問題是否全部歸因於外部因素？ |
| 迴避信號 | 使用者是否對某些部分刻意模糊？ |

前三個維度需要主動追問。
後三個維度只在偵測到明顯信號時輕觸，從不強迫展開。

---

## Stop Conditions / 停止條件

**EN**
The conversation stops when any of the following occur:

- The user has described at least one specific situation, one desired change, and two possible directions
- Each active dimension has been explored for a maximum of two rounds
- The conversation reaches seven turns total
- The user indicates they don't think they have a problem

**中文**
以下任一條件發生時，對話停止：

- 使用者已說出至少一個具體情境、一個希望的改變、以及兩個可能方向
- 每個主動追問維度最多追問兩輪
- 整體對話達到七輪上限
- 使用者表示不認為自己有問題

---

## Output Format / 輸出格式

```
────────────────────────────────────────
YOUR PROBLEM AS YOU DESCRIBED IT
你描述的問題

[Your words, not reinterpreted]
[你的語言，不加入 AI 的詮釋]
────────────────────────────────────────
YOUR CURRENT SITUATION
你提到的現況

[Facts you stated, listed without judgment]
[你陳述的事實，條列，不加評價]
────────────────────────────────────────
OPTIONS YOU MENTIONED
你提到的選項

[Directions you brought up yourself]
[你自己提到的方向]
────────────────────────────────────────
WHAT IS STILL UNCLEAR
目前還不清楚的部分

[Gaps identified — no suggestions for how to fill them]
[指出缺口，不暗示如何填補]
────────────────────────────────────────
```

---

## Supported Backends / 支援的後端

| Mode / 模式 | Provider / 服務 |
|---|---|
| Cloud API / 雲端 API | Claude (Anthropic) / GPT (OpenAI) |
| Local LLM / 本地模型 | Ollama (Llama / Mistral / Qwen) |

No data is stored. Your conversation stays in your session.
不儲存任何資料。對話僅存在於當前 session。

---

## Part of the PIDA Lab Toolchain / PIDA Lab 工具鏈的一部分

**EN**
Problem Explorer is the first layer of the PIDA Lab decision toolchain.

**中文**
Problem Explorer 是 PIDA Lab 決策工具鏈的第一層。

```
Problem Explorer  →  STME           →  RSTA
(Clarify)            (Structure)       (Stabilize)
問題釐清             決策結構保留        語意連續性穩定
```

- **Problem Explorer** — Clarify what your problem actually is / 釐清你的問題真正是什麼
- **STME** — Preserve decision structure without forcing convergence / 保留決策結構，不強迫收斂
- **RSTA** — Maintain semantic stability in long-horizon AI interaction / 維持長程 AI 互動中的語意穩定

---

## Related Repositories / 相關 Repo

- [STME](https://github.com/richchang0721-boop/stme)
- [RSTA](https://github.com/richchang0721-boop/rsta-semantic-dynamics)
- [PIDA Lab](https://www.pida-lab.com)

---

## License

Apache License 2.0
