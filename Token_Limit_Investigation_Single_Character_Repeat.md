# Token Limit Investigation: Repeated Single-Character Output and Token Efficiency across Languages

## 🧪 Objective

This experiment aims to measure the **maximum output volume per response** and the **token efficiency** of ChatGPT (GPT-4) by instructing the model to repeat the following four characters to the token limit:

- Most frequent character in Japanese: "い"
- Least frequent character in Japanese: "ぬ"
- Most frequent character in English: "e"
- Least frequent character in English: "z"

**Instruction Sample**:

- Repeat the specified character.
- Only the designated character must be displayed—no substitutions are allowed.
- Use the token limit to its fullest extent.
- Display all characters visibly on screen.
- Conclude with the message: “トークン限界まで出力を完了しました” (“Token limit output completed”).

**Verification Method**:

- Results were analysed using OpenAI's [Tokenizer Tool](https://platform.openai.com/tokenizer) to measure token and character counts.

---

## 📊 Experimental Results

| Character Type       | Japanese "い" (8.00%) | Japanese "ぬ" (0.10%) | English "e" (11.41%) | English "z" (0.06%) |
| -------------------- | -------------------- | -------------------- | -------------------- | ------------------- |
| Total Tokens Used    | 4,005                | 4,026                | 4,023                | 4,023               |
| Total Characters     | 8,010                | 2,013                | 16,092               | 8,046               |
| Tokens per Character | **0.50**             | **2.00**             | **0.25**             | **0.50**            |

---

## 🔍 Analysis

- "い" is highly efficient, compressing to **2 characters per token**.
- "ぬ" is inefficient, consuming **2 tokens per character**.
- "e" is extremely token-efficient with **4 characters per token**.
- "z" shows inefficiency due to low frequency, resulting in **double the token cost compared to "e"**.
- The total tokens per response approached the known output limit of ~4096 tokens.
- These values are consistent with the assumption that prompt tokens also consume part of the available budget.
- Despite large differences in usage frequency, characters like "い" and "z" yielded nearly identical token counts, confirming that **language-based compression efficiency exists**.

---

## 🧭 Applications and Implications

- **Prompt engineering** should consider character/token efficiency, especially under output constraints.
- High-frequency character repetition can serve as a **benchmark test** for estimating output ceilings.
- Further tests (e.g., punctuation, emojis, symbols, line breaks) can help develop a **practical token compression map**.

---

## 🧪 Observed Output Discrepancy (“Hallucination”)

### Missing Completion Message

Although the instruction included an explicit ending message ("Token limit output completed"), the message was not rendered.  
Instead, the interface showed a **“Continue generation”** button.

### 🤖 Explanation (Three-Factor Hypothesis)

1. **Autonomous Token Allocation**

As the model nears the token ceiling, it evaluates whether to continue the current pattern or terminate.

- When the main output pattern (e.g., "zzzz…") dominates, supplementary phrases are discarded.
- This prioritises **maximum token consumption**, sacrificing closing statements.

> 🎯 *The final message was likely omitted due to token exhaustion.*

2. **Compression Block Conflict**

End-of-output phrases (like “Token limit output completed”) differ from the preceding uniform pattern.

- This change requires **10–20 new tokens suddenly**, which may not fit.
- The model discards the entire phrase rather than break the token ceiling.

> 🎯 *The final line could not be inserted due to token margin exhaustion.*

3. **Inference-Based Response Termination**

GPT often ends outputs based on inferred context rather than explicit commands.

- The strict instruction to “continue repeating” may have overruled the need for postscript.
- The model inferred the response was complete with the repeated pattern alone.

> 🧠 *GPT interpreted the repeated sequence as the sole expected output.*

> These insights stem from observed behaviour, and while hallucination remains a theoretical risk, the pattern aligns with prior experience.

---

## ✅ Conclusion

This document summarises the findings of the `Token Limit Investigation` and supports further efforts toward automatic benchmarking and introspective tooling.