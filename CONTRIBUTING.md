# Contributing to Pegatron RMA Project

**English** | [中文](#中文)

---

## Welcome

We're excited you're interested in contributing to this critical automation & AI initiative for the Pegatron RMA center. This guide outlines how to collaborate effectively.

---

## Core Principles

### 1. **Async-First Collaboration**
- GitHub **Issues** & **Discussions** are our primary channels
- Synchronous standups are optional and time-boxed (30 min max)
- Decisions are documented in Issues/PRs before final merge

### 2. **Pragmatism Over Perfection**
- PoC phase: **iteration beats perfection**
- Submit work early, improve through review
- Document assumptions explicitly
- No "shiny object" syndrome—stay focused on milestone

### 3. **Transparent Decision-Making**
- Strategic decisions logged in `project-management/decision_log.md`
- Why we chose X over Y matters more than what we chose
- Dissent is encouraged; silence is assumed consent

### 4. **Modular Development**
- Each station (receiving, diagnosis, repair, dispatch, closeout) is independently validatable
- Code changes should isolate to one functional area
- Cross-station integration happens in planned phases

---

## How to Get Started

### 1. Check Current Phase
See `ROADMAP.md` to understand what's happening now.

### 2. Review Existing Docs
- **New team member?** Start with `docs/01_PROJECT_CHARTER.md`
- **Confused about scope?** See `docs/02_SUPPLY_CHAIN_ANALYSIS.md` (in progress)
- **Building PoC?** See `docs/03_POC_SPECIFICATION.md` (coming week 1)

### 3. Find Your Task
- **Issues tab:** Look for labels like `good first issue`, `help wanted`, `supplies-list`
- **Assignments:** Check `project-management/team_roles.md` for who owns what
- **Unassigned?** Comment in the Issue to claim it

### 4. Discuss Before You Code
- **Major changes?** Open an Issue first, get feedback
- **Uncertain about approach?** Post in Discussions
- **Quick fix?** PR is fine, but link to relevant Issue

---

## Workflow: Issue → Branch → PR → Merge

### Step 1: Understand the Issue
```
Example Issue Title:
[SUPPLY-CHAIN] Evaluate 3 vision tunnel vendors for PoC compatibility

Description:
- By end of week 1, assess Basler, IDS, FLIR solutions
- Criteria: cost, integration lead time, multi-spectral support
- Output: comparison table in docs/02_SUPPLY_CHAIN_ANALYSIS.md
```

### Step 2: Create a Branch
```bash
git checkout -b feature/supply-chain-vision-evaluation
# or
git checkout -b fix/edge-gateway-modbus-timeout
```

**Branch naming convention:**
- `feature/short-description` (new feature, research, spec)
- `fix/short-description` (bug fix, missing docs)
- `poc/station-name-task` (PoC-specific work)
- `refactor/short-description` (code cleanup)

### Step 3: Commit & Document
```bash
git commit -m "✨ [SUPPLY-CHAIN] Add vendor comparison table

- Basler aviator GigE: $3.2K, 8-week lead time
- IDS ensenso: $2.8K, 6-week lead time
- FLIR A70: $4.1K, 4-week lead time

Best fit for PoC: IDS (cost + speed)
See docs/02_SUPPLY_CHAIN_ANALYSIS.md for full evaluation"
```

**Commit style:**
- Emoji prefix: `✨` (feature), `🐛` (fix), `📝` (docs), `♻️` (refactor), `⚙️` (config)
- Link to Issue: `Closes #42` or `Ref #42`
- Be specific; explain the why, not just what

### Step 4: Submit PR
```markdown
## What does this do?
Completes supply chain assessment for vision tunnel hardware.

## Why is this needed?
PoC spec depends on finalized hardware selection by end of week 1.

## Evidence of work
- Contacted 3 vendors, received full specs
- Created comparison matrix
- Recommended IDS for PoC (cost, lead time, multi-spectral)

## Related Issue
Closes #12
```

### Step 5: Code Review & Merge
- **Reviewer:** Project lead or delegated tech owner
- **Review criteria:**
  - ✅ Aligns with current milestone
  - ✅ Clear, documented, follows conventions
  - ✅ No breaking changes to existing code
  - ✅ All links/references accurate
- **Approval:** 1 approval required for merge
- **Merge policy:** Squash + merge for clean history

---

## Documentation Standards

### Where Documentation Lives
- **High-level strategy & decisions:** `docs/` (Markdown files)
- **Code-level docs:** Docstrings in source code
- **Project management:** `project-management/`
- **Field notes & research:** `field-notes/`

### Markdown Template for New Docs

```markdown
# [SECTION] Title of Document

**Date Created:** 2026-04-08  
**Author:** Your Name  
**Last Updated:** 2026-04-08  
**Status:** Draft / In Review / Final  

## Overview
Brief summary (2-3 sentences).

## Key Findings / Recommendations
Bulleted insights.

## Next Steps
What happens next? Who owns it?

## References
Links to related docs, external resources.

---
*Last edited: [Name], [Date]*
```

### Code Documentation
```python
"""
Multi-spectral board defect detection module.

Uses YOLOv8 on edge gateway to detect micro-defects
(cracks, cold solder, corrosion) in <100ms per board.

Example:
    detector = BoardDefectDetector(model_path='./yolov8m-defect.pt')
    detections = detector.infer(image_array)
    
Inference: NVIDIA Jetson Xavier NX, INT8 quantization
"""
```

---

## Code Review Checklist

When reviewing a PR:
- [ ] **Is this solving the right problem?** (Check Issue/Milestone)
- [ ] **Are assumptions documented?** (Why this approach?)
- [ ] **Does code follow existing patterns?** (Consistency)
- [ ] **Is there a test or validation?** (PoC: manual is OK)
- [ ] **Will this break anything?** (Impact analysis)
- [ ] **Is documentation updated?** (If scope-change)

---

## Testing & Validation

### PoC Phase (Weeks 1-8)
- **Unit tests:** Nice to have; pragmatism first
- **Integration tests:** Manual validation is acceptable
- **Documentation of results:** Essential

### Pre-Production (Week 9+)
- **Unit test coverage:** 60%+ for critical paths
- **Integration tests:** Required before field deployment
- **Field validation:** On-site testing with Pegatron team

---

## Common Workflows

### "I found a bug in the PoC"
1. Open Issue: `[BUG] Brief description`
2. Attach error log, screenshot, reproduction steps
3. Label: `bug`, `priority-high` (if blocking)
4. Create PR to fix, link Issue

### "I need clarification on the technical architecture"
1. Post in **Discussions** → `Architecture & Design`
2. Project lead responds with pointer to doc or explanation
3. If guidance is new, we update `docs/04_TECHNICAL_ARCHITECTURE.md`

### "Supply chain vendor response just arrived"
1. Create Issue: `[SUPPLY-CHAIN] Vendor X response — evaluation needed`
2. Attach or summarize key info
3. Create PR updating `docs/02_SUPPLY_CHAIN_ANALYSIS.md`
4. Ping project lead for go/no-go decision

### "We need to change the PoC scope"
1. Open Issue: `[DECISION] Scope change proposal — [Title]`
2. Explain rationale, tradeoffs, impact
3. Get feedback in comments
4. Decision logged in `project-management/decision_log.md`
5. Update `ROADMAP.md` if timeline affected

---

## Dos & Don'ts

### ✅ Do
- Submit incomplete work early (WIP PRs welcome)
- Ask questions in Issues—there are no dumb questions
- Update docs as you learn something new
- Reference other Issues/PRs: "See #42"
- Communicate blockers immediately
- Celebrate wins (big and small)

### ❌ Don't
- Assume someone else will document your work
- Ignore comments on your PR
- Create mega-PRs (>500 lines) without discussion
- Work in isolation for weeks
- Commit directly to `main` branch
- Merge your own PR without review (except for docs-only changes)

---

## Getting Help

### "I'm stuck"
- **Quick question?** Comment in the Issue
- **Detailed help?** Post in Discussions, tag project lead
- **Emergency blocker?** Ping on async comms (Slack/email)

### "I need to add a tool/library/dependency"
- Check `software/*/requirements.txt` or `package.json` first
- Open Issue: `[INFRA] Propose adding [tool] for [reason]`
- Get approval before including in code

### "How do I run tests/build/deploy?"
- See `README.md` → Getting Started
- See relevant `software/*/README.md` for specifics
- If instructions are missing, document them in an Issue

---

## Decision-Making Process

### Small Decisions (code style, file location)
→ Decide in PR review, log if it changes precedent

### Medium Decisions (algorithm choice, vendor selection)
1. Open Issue with pros/cons
2. Discuss in comments for 24-48 hours
3. Project lead decides; log in `decision_log.md`
4. Update relevant doc

### Large Decisions (scope change, architecture pivot)
1. Open Issue with thorough analysis
2. Async discussion (48+ hours for input)
3. Formal decision call (project lead + key stakeholders)
4. Log decision + rationale in `decision_log.md`
5. Communicate impact across team

---

## Release / Deployment Checklist

When moving from PoC to next phase:
- [ ] All Issues for milestone closed or deferred
- [ ] Documentation updated (`docs/04_TECHNICAL_ARCHITECTURE.md`, etc.)
- [ ] Code review complete
- [ ] Field validation results documented
- [ ] CHANGELOG.md updated
- [ ] Team retrospective scheduled

---

<a name="中文"></a>

# 为和硕项目做贡献

**中文** | [English](#welcome)

---

## 欢迎加入

感谢你对这个关键的自动化与 AI 项目的贡献。本指南规范了协作方式。

---

## 核心原则

### 1. **异步优先协作**
GitHub Issues & Discussions 是主要沟通渠道。同步会议可选，控制在 30 分钟以内。

### 2. **务实优于完美**
PoC 阶段，迭代胜于完美。早期提交，通过评审改进。清晰文档化假设。

### 3. **透明决策**
所有战略决策记录在 `project-management/decision_log.md`。为什么比选了什么更重要。

### 4. **模块化开发**
每个工站（收货、诊断、维修、分拨、出库）独立可验证。代码变更只影响一个功能区。跨工站集成分阶段进行。

---

## 快速开始

1. **阅读项目章程：** `docs/01_PROJECT_CHARTER.md`
2. **查看当前阶段：** `ROADMAP.md`
3. **找到你的任务：** Issues 标签：`good first issue`, `help wanted`
4. **声明任务：** 在 Issue 中评论表示认领

---

## 工作流：Issue → 分支 → PR → 合并

### 分支命名
- `feature/短描述` (新功能、研究、规范)
- `fix/短描述` (bug修复、缺失文档)
- `poc/工站名称-任务` (PoC专项)
- `refactor/短描述` (代码重构)

### 提交信息规范
```
✨ [标签] 简短描述

- 详细说明
- 第二点
- 第三点

关联 Issue: Closes #42
```

**Emoji 前缀：**
- `✨` (功能), `🐛` (bug), `📝` (文档), `♻️` (重构), `⚙️` (配置)

### PR 审核
- 1 个批准即可合并
- 批准前检查：与里程碑对齐、文档清晰、无破坏性变更

---

## 文档标准

### 文件位置
- 高层战略 → `docs/`
- 代码文档 → 源代码注释
- 项目管理 → `project-management/`
- 现场记录 → `field-notes/`

### 新文档模板
```markdown
# [标签] 文档标题

**创建日期：** 2026-04-08  
**作者：** 你的名字  
**最后更新：** 2026-04-08  
**状态：** 草稿 / 审核中 / 最终  

## 概览
2-3 句摘要。

## 关键发现 / 建议
要点列表。

## 后续步骤
接下来做什么？谁负责？
```

---

## 常见工作流

### "我发现了 PoC 中的 bug"
1. 开 Issue: `[BUG] 简短描述`
2. 附加错误日志、截图、复现步骤
3. 标签：`bug`, `priority-high`

### "我需要理解技术架构"
1. 在 Discussions 发文章 → `Architecture & Design`
2. 项目负责人回复，可能更新文档

### "供应链厂商回复了"
1. 开 Issue: `[SUPPLY-CHAIN] 厂商 X 回复 — 需要评估`
2. 更新 `docs/02_SUPPLY_CHAIN_ANALYSIS.md`
3. 联系项目负责人决策

### "我们需要改变 PoC 范围"
1. 开 Issue: `[DECISION] 范围变更提议 — [标题]`
2. 解释原因、权衡、影响
3. 决策记录在 `project-management/decision_log.md`

---

## ✅ 要做的事

- 早期提交未完成的工作（WIP PR 欢迎）
- 在 Issues 中提问
- 学到新东西时更新文档
- 引用其他 Issue/PR
- 立即上报阻塞因素

---

## ❌ 不要做的事

- 假设别人会文档化你的工作
- 忽视 PR 评论
- 创建超大 PR（>500 行）而不讨论
- 孤立工作数周
- 直接提交到 `main` 分支
- 自己合并自己的 PR（除了纯文档变更）

---

## 获取帮助

- **快速问题？** 在 Issue 中评论
- **详细帮助？** 在 Discussions 中发文，标记项目负责人
- **紧急阻塞？** 异步通信（Slack/邮件）

---

*最后更新：2026-04-08 | 项目负责人：Kaige Liao (Leo)*
