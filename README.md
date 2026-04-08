# Pegatron RMA Intelligent Vision & Automation Turnkey Project

**English** | [中文](#中文)

---

## Overview

This repository documents the **AI-driven vision & process automation** retrofit project for the **Pegatron (America) RMA (Return Merchandise Authorization) center** in Indiana. The project aims to replace manual diagnostics and process bottlenecks with intelligent vision recognition, multi-spectral hardware, and edge computing—creating a scalable, reproducible automation model for electronics repair centers.

### Quick Facts
- **Client:** Pegatron RMA Center (Indiana, USA)
- **Project Lead:** Kaige Liao (Leo)
- **Stage:** Project Inception & Planning
- **Timeline:** 14-24 weeks (PoC through deployment)
- **Scope:** Five core RMA process stations (receiving → diagnosis → repair → dispatch → closeout)

---

## 🎯 Core Problem & Solution

### The Problem
Pegatron's RMA center processes thousands of **non-standard damaged devices** (liquid damage, physical abuse, unauthorized repairs) monthly. Current workflow:
- **Manual bottlenecks:** Parcel scanning, B2B/B2C classification, appearance assessment
- **L2/L3 technician dependency:** Manual board inspection to spot micro-defects (high cost, human fatigue → missed detects)
- **Process confusion:** Manual work assignment, no digital traceability

### The Solution
**Phased AI + Automation retrofit** targeting high-pain, repetitive, error-prone stations:

| Station | Current State | AI/Automation Intervention |
|---------|---------------|--------------------------|
| **Receiving & Intake** | Manual scanning, sorting | AI vision tunnel + OCR auto-routing |
| **Appearance Assessment** | Human judgment (dispute-prone) | Digital imaging + rule-based liability assignment |
| **Deep Diagnosis** ⭐ | L2/L3 manual inspection | Multi-spectral AI vision → micro-defect detection |
| **Repair & Dispatch** | Manual work assignment | PLC auto-routing based on diagnostic output |
| **Closeout** | Manual cleaning & packaging | Automated wash + label generation |

**Expected Impact:**
- 30–40% reduction in L2/L3 labor
- <1% missed defect rate (vs. 5–8% manual baseline)
- 20–30% cycle time reduction
- Replicable "RMA automation standard model"

---

## 📂 Repository Structure

```
pegatron-rma-project/
├── README.md                                    # (This file)
├── CONTRIBUTING.md                              # Contribution guidelines
├── ROADMAP.md                                   # Project timeline & milestones
├── docs/
│   ├── 01_PROJECT_CHARTER.md                   # Full project definition & strategy
│   ├── 02_SUPPLY_CHAIN_ANALYSIS.md             # Mature solution evaluation (in progress)
│   ├── 03_POC_SPECIFICATION.md                 # PoC detailed design (in progress)
│   ├── 04_TECHNICAL_ARCHITECTURE.md            # System architecture blueprint
│   ├── 05_COMPLIANCE_CHECKLIST.md              # OSHA/UL/Data privacy requirements
│   └── 06_DEPLOYMENT_GUIDE.md                  # Field installation & training
├── hardware/
│   └── specifications/
│       ├── vision_tunnel_spec.md
│       ├── multispectral_camera_spec.md
│       ├── edge_gateway_spec.md
│       └── plc_integration_spec.md
├── software/
│   ├── models/                                  # Defect detection ML models
│   │   ├── board_defect_yolov8/
│   │   └── README.md
│   ├── edge-gateway/                            # Edge computing software
│   │   ├── src/
│   │   ├── requirements.txt
│   │   └── README.md
│   ├── dashboard/                               # Real-time monitoring UI
│   │   ├── src/
│   │   └── README.md
│   └── integrations/                            # PLC & external system connectors
│       ├── modbus_client.py
│       ├── opc_ua_connector.py
│       └── README.md
├── field-notes/
│   └── site_survey_indiana_2026_04.md          # On-site investigation record
├── project-management/
│   ├── milestones.md                           # Key project phases
│   ├── team_roles.md                           # Role definitions & ownership
│   ├── decision_log.md                         # Strategic decisions & rationale
│   └── risk_register.md                        # Risk tracking
├── .gitignore
├── LICENSE                                      # (Apache 2.0 or equiv.)
└── CHANGELOG.md
```

---

## 🚀 Getting Started

### For Project Members
1. **Read the charter:** Start with `docs/01_PROJECT_CHARTER.md`
2. **Understand the phase:** Check current milestone in `ROADMAP.md`
3. **Review your role:** See `project-management/team_roles.md`
4. **Follow contribution guidelines:** See `CONTRIBUTING.md`

### For Supply Chain / Partnership Discussions
- See `docs/02_SUPPLY_CHAIN_ANALYSIS.md` for mature vision solutions under evaluation
- See hardware specs in `hardware/specifications/`

### For PoC Development
- Check `docs/03_POC_SPECIFICATION.md` (being finalized)
- See software structure in `software/`

---

## 📋 Current Phase: Project Inception & Planning

### ✅ Completed
- [x] Needs assessment & problem definition
- [x] On-site investigation (Indiana, 2026-04)
- [x] Strategic approach finalized

### 🔄 In Progress (This Week)
- [ ] GitHub repo setup (core structure, CI/CD framework)
- [ ] Supply chain rapid evaluation
- [ ] PoC specification finalization
- [ ] Team role confirmation

### 📅 Upcoming Milestones
- **Week 1-2:** Repo framework + supply chain assessment
- **Week 3:** PoC detailed design + team kickoff
- **Week 4-6:** Formal engagement with Pegatron
- **Week 7-14:** PoC execution & validation

See `ROADMAP.md` for detailed timeline.

---

## 🏗️ Technical Architecture (Preview)

### Technology Stack
- **Vision & ML:** YOLOv8 + TensorRT (edge inference), OpenCV
- **Edge Computing:** NVIDIA Jetson Xavier NX / Orin (local processing)
- **Process Automation:** Modbus/OPC-UA bridge → PLC control
- **Monitoring Dashboard:** Node.js + React
- **Data Pipeline:** (PostgreSQL for audit trail, optional cloud logging with privacy)

### Design Principles
- **Decentralized inference:** All processing on-site (no cloud dependency, compliance-friendly)
- **Real-time responsiveness:** Sub-100ms defect detection latency
- **Modularity:** Each station can be validated independently before chain integration
- **Auditability:** Full traceability of decisions (images, timings, diagnostics)

---

## 📊 Success Metrics

| Metric | Baseline | Target |
|--------|----------|--------|
| **L2/L3 labor requirement** | 100% | 60-70% |
| **Missed defect rate** | 5-8% | <1% |
| **RMA cycle time** | 100% | 70-80% |
| **Diagnostic dispute rate** | High (subjective) | Minimal (rule-based) |
| **System availability** | N/A | >95% uptime |

---

## 🤝 How to Contribute

### For Team Members
1. **Claim a task:** Check Issues with `help wanted` label
2. **Document as you go:** Update relevant section in `docs/`
3. **Submit PRs early:** No polished-first culture; iteration is normal
4. **Async-first communication:** Use Issues/Discussions; sync standup optional

### Code Review & Merge
- All changes require approval from project lead
- PoC phase: rapid iteration, pragmatism over perfection
- Before production: full code review + testing

See `CONTRIBUTING.md` for detailed guidelines.

---

## 📞 Contact & Support

- **Project Lead:** Kaige Liao (Leo)
- **Primary Communication:** GitHub Issues, Discussions, Async
- **Weekly Sync:** (TBD based on team availability)

---

## 📜 License

This project is licensed under **Apache 2.0** — see `LICENSE` file.

---

## 📚 Additional Resources

### Internal Documentation (in this repo)
- Full project charter: `docs/01_PROJECT_CHARTER.md`
- Supply chain analysis: `docs/02_SUPPLY_CHAIN_ANALYSIS.md` (coming week 1)
- PoC specification: `docs/03_POC_SPECIFICATION.md` (coming week 1)
- Technical architecture: `docs/04_TECHNICAL_ARCHITECTURE.md` (coming week 2)

### External References
- Pegatron corporate site: https://www.pegatron.com
- OSHA compliance (general): https://www.osha.gov
- YOLOv8 docs: https://docs.ultralytics.com
- Jetson edge AI: https://developer.nvidia.com/embedded/jetson

---

## 🔄 Changelog

See `CHANGELOG.md` for version history and updates.

---

<a name="中文"></a>

# 美国和硕（Pegatron）笔记本售后 RMA 智能视觉与自动化交钥匙项目

**中文** | [English](#overview)

---

## 项目概览

本仓库记录了**和硕（美国）印第安纳州 RMA（售后维修）中心**的 **AI 智能视觉与流程自动化改造项目**的完整演进。项目通过部署智能视觉识别、多光谱硬件与边缘计算，替代人工诊断并消除流程瓶颈，打造可复制的电子产品维修中心自动化标准模型。

### 快速事实
- **客户：** 和硕 RMA 中心（美国印第安纳州）
- **项目负责人：** Kaige Liao (Leo)
- **阶段：** 项目立项与规划
- **周期：** 14-24 周（从 PoC 到部署）
- **范围：** 五大 RMA 工作站（收货 → 诊断 → 维修 → 分拨 → 出库）

---

## 🎯 核心问题与方案

### 问题现状
和硕 RMA 中心每月处理数千台**非标损伤设备**（进水、人为破坏、私拆）。现有工作流：
- **人工瓶颈：** 包裹扫码、B2B/B2C 分类、外观判责
- **L2/L3 技师依赖：** 人工检查电路板微小缺陷（成本高、人眼疲劳→漏检）
- **流程混乱：** 工作分配无数字化、不可追溯

### 解决方案
**分阶段 AI + 自动化改造**，优先锁定高痛点、高重复、高错误率的工站：

| 工站 | 现状 | AI/自动化干预 |
|------|------|------------|
| **收货与入库** | 人工扫码、分类 | AI 视觉隧道 + OCR 自动分流 |
| **外观定责** | 人眼判断（争议多） | 数字化影像 + 规则化定责 |
| **深度诊断** ⭐ | L2/L3 人工检查 | 多光谱 AI 视觉 → 微缺陷自动检出 |
| **维修与分拨** | 人工分配工位 | PLC 自动分流 |
| **出库与闭环** | 手工清洁、包装 | 自动化清洁 + 标签生成 |

**预期效果：**
- L2/L3 人力成本下降 30-40%
- 漏检率从人工的 5-8% 降至 <1%
- 周期缩短 20-30%
- 形成可复制的"售后自动化标准模型"

---

## 📂 仓库结构

见英文版本中的树形结构。核心文档：
- `docs/01_PROJECT_CHARTER.md` — 完整项目定义与战略
- `docs/02_SUPPLY_CHAIN_ANALYSIS.md` — 供应链评估（进行中）
- `docs/03_POC_SPECIFICATION.md` — PoC 详细设计（进行中）
- `docs/04_TECHNICAL_ARCHITECTURE.md` — 系统架构
- `project-management/` — 项目管理资料

---

## 🚀 快速开始

1. **阅读章程：** `docs/01_PROJECT_CHARTER.md`
2. **了解阶段：** `ROADMAP.md`
3. **查看角色：** `project-management/team_roles.md`
4. **遵守约定：** `CONTRIBUTING.md`

---

## 🔄 当前阶段：立项与规划

### ✅ 已完成
- [x] 需求评估与问题定义
- [x] 现场调研（印第安纳州，2026-04）
- [x] 战略方案定型

### 🔄 进行中（本周）
- [ ] GitHub 仓库初设
- [ ] 供应链快速评估
- [ ] PoC 规范化
- [ ] 团队确认

### 📅 后续里程碑
详见 `ROADMAP.md`

---

*最后更新：2026-04-08 | 项目负责人：Kaige Liao (Leo)*
