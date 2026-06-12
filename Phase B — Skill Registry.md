# TUNGNS Trading OS

# Phase B — Skill Registry

## Purpose

Chuyển robot từ:

```text
Folder-based Architecture
```

sang:

```text
Capability-based Architecture
```

Mục tiêu:

* mở rộng dễ dàng;
* cô lập trách nhiệm;
* giảm coupling;
* hỗ trợ Long Horizon;
* hỗ trợ Evolution OS;
* hỗ trợ Memory OS.

---

# Philosophy

Agent không chứa logic.

Agent chỉ điều phối.

Năng lực thực sự nằm trong Skills.

```text
Agent
↓
Skill
↓
Evidence
↓
Memory
↓
Evolution
```

---

# Old Architecture

Hiện tại:

```text
market/
strategy/
execution/
guard/
optimization/
```

Đây là cấu trúc theo module kỹ thuật.

Nhược điểm:

* khó mở rộng;
* khó tái sử dụng;
* logic phân tán;
* khó tiến hóa.

---

# New Architecture

Tạo:

```text
backend/app/skills/
```

Cấu trúc:

```text
backend/app/skills/

market-analysis/
setup-detection/
risk-engine/
execution-engine/
hedge-engine/
optimization-engine/
journal-engine/
portfolio-analysis/
backtesting/
regime-analysis/
```

---

# Principle

Một skill chỉ làm một việc.

Không tạo:

```text
super_strategy.py
```

Không tạo:

```text
ultimate_agent.py
```

Ưu tiên:

```text
Small Files
Single Responsibility
```

---

# Skill Contract

Mọi skill bắt buộc có:

```text
skill.md
config.json
examples/
tests/
metrics/
```

Ví dụ:

```text
market-analysis/

skill.md
config.json
examples/
tests/
metrics/
```

---

# Standard Interface

Input:

```json
market_state
```

Output:

```json
{
  "decision": "...",
  "confidence": 0.87,
  "evidence": [],
  "metadata": {}
}
```

---

# Market Analysis Skill

Trách nhiệm:

* market structure;
* trend;
* momentum;
* volatility.

Không được:

* đặt lệnh;
* tính risk;
* ghi journal.

---

# Setup Detection Skill

Trách nhiệm:

* breakout;
* pullback;
* reversal;
* continuation.

Không được:

* quản lý vốn;
* execution.

---

# Risk Engine Skill

Trách nhiệm:

* position size;
* stop loss;
* exposure;
* daily risk.

Ưu tiên:

```text
Capital Protection
↓
Survival
↓
Profit
```

---

# Execution Engine Skill

Trách nhiệm:

* open trade;
* modify trade;
* close trade;
* sync broker.

Không được:

* phân tích thị trường.

---

# Hedge Engine Skill

Trách nhiệm:

* correlation;
* hedge;
* portfolio exposure.

---

# Optimization Engine Skill

Trách nhiệm:

* parameter search;
* statistics;
* strategy evaluation.

Không được:

* gửi lệnh.

---

# Journal Engine Skill

Trách nhiệm:

Lưu:

* entry;
* exit;
* setup;
* evidence;
* result.

Journal là nguồn dữ liệu của Memory OS.

---

# Portfolio Analysis Skill

Trách nhiệm:

* total exposure;
* correlation;
* concentration risk.

Robot không đánh giá từng lệnh riêng lẻ.

Robot đánh giá toàn bộ danh mục.

---

# Backtesting Skill

Mục tiêu:

Không chứng minh chiến lược đúng.

Mục tiêu là tìm:

* điểm yếu;
* drawdown;
* regime phù hợp;
* điều kiện thất bại.

---

# Regime Analysis Skill

Phân loại:

```text
Trending
Ranging
Volatile
News
Low Liquidity
```

Mỗi regime kích hoạt skill khác nhau.

---

# Migration Plan

Di chuyển dần:

```text
market/
→ market-analysis/

strategy/
→ setup-detection/

execution/
→ execution-engine/

guard/
→ risk-engine/

optimization/
→ optimization-engine/
```

Không rewrite toàn bộ một lần.

Áp dụng:

```text
Generate
↓
Verify
↓
Publish
```

---

# Final Architecture

```text
10 Agents
↓
100+ Skills
↓
Memory OS
↓
Governance OS
↓
Evolution OS
↓
Trading OS
```

---

# Ultimate Goal

Robot không phải tập hợp file Python.

Robot là hệ thống năng lực có thể học và tiến hóa theo thời gian.
