---
layout: post
title: "Day 1: challenge minggu 1 keluar, trade-note"
---

Challenge pertama resmi keluar. Namanya "trade-note": CLI yang manggil LLM lewat direct API (tanpa framework, tanpa LangChain) dan mengubah satu kalimat bebas soal trade menjadi JSON ketat.

Contoh input: "short BTC 5x kena stop di 61k, rugi 2.3%". Outputnya wajib valid terhadap schema: side, asset, leverage, outcome, pnl_pct, confidence. Field yang tidak disebut di teks harus null, bukan tebakan model.

![Kartu challenge W1 trade-note]({{ '/shots/2026-07-12-w1-trade-note.png' | relative_url }})

## Exit criteria

Yang bikin challenge ini bukan sekadar "panggil API terus print":

1. Runnable satu perintah, JSON valid ke stdout. Grader menjalankan 5 input sendiri, bukan percaya klaim saya.
2. Structured output dipaksa lewat tool schema / forced tool_choice, bukan "please output JSON" di prompt lalu regex.
3. Retry dengan exponential backoff untuk 429/5xx dan untuk schema-validation failure (re-ask maksimal 2x), dibuktikan dengan test.
4. Output yang tidak valid schema tidak pernah lolos ke stdout. Kalau gagal setelah retry, exit code bukan 0.
5. Setiap call mencatat token in/out plus estimasi biaya USD.

## Kenapa aturannya sekeras ini

Ini minggu 1 dari 16, fase LLM Engineering. Aturan mainnya dari awal: setiap deliverable harus bisa dijalankan orang lain, setiap klaim harus ada angkanya, dan yang menilai bukan saya sendiri tapi grader terpisah yang menjalankan kodenya dari nol. Kalau gagal, gagalnya ikut diposting.

Deliverable belum ada hari ini. Yang ada baru spec dan deadline. Besok mulai ngoding.
