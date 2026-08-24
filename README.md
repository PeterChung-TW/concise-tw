# 精簡（concise-tw）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen.svg)](CHANGELOG.md)
[![zh-TW](https://img.shields.io/badge/zh--TW-Taiwan-e4002b.svg)](SKILL.md)

繁體中文的 **AI 輸出收緊 skill**。跟 AI 協作久了會發現：回應越寫越長、開場白越來越客套、
「大約 5 分鐘」永遠不準、收尾一串「還需要我做什麼嗎」。這個 skill 用十條規則把輸出收緊——
首句就是結論、步驟一律編號、時間只講可驗證的事實、結尾只指名一個下一步。

靈感來自 [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd)（23k+ stars，2026-08 查），
但**不是翻譯**：原版十條規則裡有三條在真實工程 session 實測會出問題
（憑感覺報分鐘數、硬拆稽核清單、壓制岔題），本 skill 修正了它們，
並把英文口頭禪清單換成繁中使用者實際會遇到的版本。
完整取捨記錄在 [references/design-notes.md](references/design-notes.md)。

## 安裝

**Claude Code**（v1.0.30+）：

```bash
git clone https://github.com/PeterChung-TW/concise-tw.git ~/.claude/skills/concise-tw
```

或手動：下載本 repo，把整個資料夾放進 `~/.claude/skills/`。

不需要 hooks、不需要外部連線、不執行任何 shell——純 Markdown 規則檔，
看得完、審得完，隨時刪掉資料夾就完全移除。

## 使用

| 說什麼 | 效果 |
|---|---|
| 「精簡」「開精簡」「講重點」 | 開啟收緊模式 |
| 「精簡 off」「關閉精簡」 | 關閉，回到平常風格 |

開啟後的效果（節錄）：

**開啟前**：
> 好問題！讓我先看一下這個檔案的結構……（500 字後）……大約再 5 分鐘就能完成，還有什麼需要我做的嗎？

**開啟後**：
> 要改的是 `config.py:42`——逾時值 30 改 120。上次同規模的批次跑了 19.8 分鐘，這批量相同。
> 下一步：跑一次 `pytest tests/` 確認沒有其他呼叫點炸掉。

## 十條規則一覽

| # | 規則 | 來源 |
|---|---|---|
| 1 | 首行就是結論或可執行動作 | 吸收 |
| 2 | 多步驟一律編號 | 吸收 |
| 3 | 結尾指名一個兩分鐘內做得完的下一步 | 吸收 |
| 4 | 長流程每回合重述進度 | 吸收 |
| 5 | 成果附證據（檔案:行號／commit／工具回傳） | 吸收 |
| 6 | 錯誤平鋪直述 | 吸收 |
| 7 | 時間只講可驗證事實，禁憑感覺報分鐘 | **修正**：AI 沒有時間感 |
| 8 | 清單上限 5 項只約束摘要層 | **修正**：稽核需要完整枚舉 |
| 9 | 岔題記錄並收尾帶一行，不壓制不即興 | **修正**：壓掉會埋真問題 |
| 10 | 無開場白無客套，但保留三句話收尾 | **拆半**：非同步閱讀需要收尾 |

## 搭配推薦

- [speak-human-tw](https://github.com/Raymondhou0917/speak-human-tw)——去 AI 味改寫。
  concise-tw 管「結構收緊」，speak-human-tw 管「語感自然」，兩個處理的是不同層，可以同時裝。

## 授權

MIT。規則概念致謝 [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd)；
本 repo 內容為繁中重寫與工程修正版，非原文翻譯。
