# COBOL Cookbook 🍳

> **SRM FOSS Club** × **IBM Z Workshop** — *Monday, 21 September 2026*

A collection of tiny COBOL programs written by first-time contributors during a 2-hour hands-on sprint. Every program solves a well-defined task, compiles cleanly with GnuCOBOL, and has a merged pull request to prove it.

## The Story

On 21 Sept 2026, 80+ students gathered in TP2 702 for a talk by **Senthil (IBM Z)** followed by a live open-source sprint. Most had never written COBOL. Many had never opened a pull request. By 2:30 PM, the contributor graph looked like this:

![Contributor graph will appear after event](https://contrib.rocks/image?repo=fossclubsrmktr/cobol-cookbook)

## Programs

| # | Program | Tier | Author | PR |
|---|---------|------|--------|----|
| 001 | BizzBuzz 1–50 | 🥉 | — | — |
| 002 | Name Banner | 🥉 | — | — |
| 003 | Simple Interest | 🥉 | — | — |
| 004 | °C ↔ °F Converter | 🥉 | — | — |
| 005 | Reverse String (no REVERSE) | 🥉 | — | — |
| 006 | Vowel Counter | 🥉 | — | — |
| 007 | Largest of 5 | 🥉 | — | — |
| 008 | Multiplication Table | 🥉 | — | — |
| 009 | Sum of Digits | 🥉 | — | — |
| 010 | Leap Year Checker | 🥉 | — | — |
| 011 | SRM-FOSS Game | 🥉 | — | — |
| 012 | Star Pyramid | 🥉 | — | — |
| 013 | Student Grades | 🥈 | — | — |
| 014 | Phone Formatter | 🥈 | — | — |
| 015 | Word Count | 🥈 | — | — |
| 016 | Toy Email Validator | 🥈 | — | — |
| 017 | Inventory Report | 🥈 | — | — |
| 018 | Week's Temperatures | 🥈 | — | — |
| 019 | Palindrome Checker | 🥈 | — | — |
| 020 | Currency Converter | 🥈 | — | — |
| 021 | Report Generator | 🥇 | — | — |
| 022 | FizzBuzz via JCL | 🥇 | — | — |
| 023 | COBOL vs Python | 🥇 | — | — |
| 024 | Expression Calculator | 🥇 | — | — |
| 025 | Caesar Cipher | 🥇 | — | — |

*Table auto-updated by merge bot after event.*

## Tier Guide

- 🥉 **Bronze** — Syntax & flow control (loops, conditionals, basic I/O)
- 🥈 **Silver** — Data handling (tables, string manipulation, formatted output)
- 🥇 **Gold** — Showoffs (reports, JCL, multi-language, parsing, crypto)

## Quick Start

```bash
# Install GnuCOBOL (Ubuntu/Debian)
sudo apt-get install gnucobol

# Or macOS
brew install gnucobol

# Compile & run any program
cobc -x -free programs/001-bizzbuzz/bizzbuzz.cbl -o bizzbuzz
./bizzbuzz
```

## License

- **Code**: MIT License — see [LICENSE](LICENSE)
- **Documentation**: CC BY-SA 4.0 — see [LICENSE.docs](LICENSE.docs)

## Credits

Organised by **SRM FOSS Club** with support from **IBM Z / Senthil**.