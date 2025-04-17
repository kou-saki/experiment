# Token Limit Investigation

This branch contains a series of experiments related to token limit behavior in GPT models (primarily GPT-4-turbo).

## 📌 Purpose

The purpose of this investigation is to:

- Understand how GPT models behave near their token output limits
- Compare different character types (e.g., Japanese vs. English, frequent vs. rare)
- Observe compression patterns, truncation behavior, and output stability

## 📁 Files Included

| File Name | Description |
|-----------|-------------|
| `Token_Limit_Investigation_Single_Character_Repeat.md` | A markdown-based summary of output behavior across character types |
| `トークン限界調査実験：出力比較まとめ.md` | Japanese summary of output comparison results |
| `トークン限界値探査_日本語最頻_い.txt` | Output from repeating the most frequent Japanese character ("い") |
| `トークン限界値探査_日本語最小頻_ぬ.txt` | Output from repeating a rare Japanese character ("ぬ") |
| `トークン限界値探査_英語最頻_e.txt` | Output from repeating the most frequent English letter ("e") |
| `トークン限界値探査_英語最小頻_z.txt` | Output from repeating a rare English letter ("z") |

## 🔬 Notes

- This experiment is part of a broader investigation into the internal mechanics of GPT tokenization and output management.
- The outputs were generated using ChatGPT (GPT-4-turbo) with default settings.
- No external preprocessing or formatting was applied to raw outputs.

## 🧠 Motivation

The experiment aims to surface reproducible insights for:

- Prompt engineers
- AI researchers
- Anyone trying to understand GPT's token limits in practice

---

If you want to reproduce this experiment, we recommend:
- Using the ChatGPT interface (or API) with a prompt structure that encourages max-length generation.
- Comparing character types across different languages and frequency distributions.

---

## :page_facing_up:	LICENSE

- This project is licensed under the MIT License.
