# Decision Log

**Owner:** Kaige Liao (Leo)  
**Last Updated:** 2026-04-08

---

## How to Use This Log

Every **strategic decision** (scope change, vendor selection, architecture choice, timeline shift) is documented here with:
- **Date & Decision ID**
- **What we decided**
- **Why we decided it** (context, options evaluated, tradeoffs)
- **Impact** (cost, timeline, risk)
- **Who decided** (decision-maker)
- **Status** (active, superseded, archived)

This creates a transparent, auditable trail of project evolution.

---

## Decision Log

### Decision D001: Project Scope - RMA vs Production Line

**Date:** 2026-04 (during on-site investigation)  
**Decision ID:** D001  
**Status:** ✅ **Active**

#### What We Decided
Project focus is **RMA (Return Merchandise Authorization) sold-after diagnostics & automation**, NOT production-line quality inspection.

#### Context & Options Evaluated
| Option | Pros | Cons | Vote |
|--------|------|------|------|
| **Production line QC** | Standardized defects, stable volume | Commoditized, low ROI, intense competition | ❌ |
| **RMA sold-after (chosen)** | High labor cost, non-standard damage, high ROI | Requires deep vendor collaboration | ✅ |

#### Why This Decision
1. **ROI optimization:** Non-standard damage (liquid, physical abuse, private repairs) forces labor-intensive manual triage. AI intervention ROI = 30-40% labor reduction.
2. **Business alignment:** Pegatron's margin pressure in RMA is acute; production margins already optimized.
3. **Differentiation:** RMA automation creates defensible customer stickiness; production automation is easily replicated.
4. **Collaboration:** Pegatron RMA center manager explicitly requested this (vs. theoretical production line need).

#### Impact
- **Scope expansion:** Now includes 5 RMA stations, not just 1 PCB inspection station
- **Timeline:** No change (2-phase structure still valid)
- **Budget:** +15% (more comprehensive stations, more on-site time)
- **Risk:** Higher collaboration overhead; must understand Pegatron's full RMA workflow

#### Who Decided
Kaige (Project Lead) based on stakeholder input + on-site investigation

#### Related Issues
- [GitHub Issue #1] Initial scoping discussion (link when repo created)

---

### Decision D002: Strategy - "Don't Rebuild Wheels" Approach

**Date:** 2026-04 (during solution design)  
**Decision ID:** D002  
**Status:** ✅ **Active**

#### What We Decided
Prioritize **existing, market-tested Chinese 3C automation solutions** over building custom ML/hardware from scratch. Adapt + localize, don't invent.

#### Context & Options Evaluated
| Option | Pros | Cons | Vote |
|--------|------|------|------|
| **Custom architecture** | Tailored to Pegatron, cutting edge | 12+ months to production, high risk | ❌ |
| **Market solutions + adapt (chosen)** | 6-8 weeks to PoC, proven tech, lower cost | Less tailored, requires integration effort | ✅ |

#### Why This Decision
1. **Speed to market:** Pegatron needs solution in 6 months, not 12+
2. **De-risking:** Chinese 3C automation supply chain is mature; low technical risk
3. **Replicability:** Standardized solutions easily replicated across other factories
4. **Cost efficiency:** Avoid R&D spend; allocate budget to integration + customization
5. **Team capacity:** Small team (4-5 people); can't both invent + operationalize

#### Impact
- **Vendor evaluation:** Shifts to assessing multi-spectral cameras (Basler, IDS, FLIR), not building in-house
- **Timeline:** PoC in 6 weeks (vs. 16+ weeks for custom)
- **Budget:** -20% hardware/software cost, +10% integration cost
- **Risk:** Less technical uniqueness; dependent on vendor roadmap

#### Who Decided
Kaige + Tech Lead consensus after weeks 2-3 technical discussions

#### Related Issues
- [GitHub Issue #2] Vendor evaluation task (link when repo created)

---

### Decision D003: Hardware - NVIDIA Jetson as Edge Gateway

**Date:** 2026-04-08 (to be confirmed in week 2)  
**Decision ID:** D003  
**Status:** 🟡 **Pending Confirmation**

#### What We Decided (Proposed)
Use **NVIDIA Jetson Xavier NX** (or Orin if budget allows) as the edge compute gateway for:
- YOLOv8 inference (TensorRT optimization)
- Modbus client → PLC command routing
- Local data logging (no cloud dependency)

#### Context & Options Evaluated
| Option | Specs | Cost | Lead Time | Vote |
|--------|-------|------|-----------|------|
| **Jetson Xavier NX** | 8-core ARM, 8GB RAM, 100 TOPS | ~$800 | 6-8 weeks | ✅ |
| **Jetson Orin (premium)** | 12-core ARM, 12GB RAM, 275 TOPS | ~$1,400 | 8-10 weeks | 🤔 |
| **x86 (Intel NUC)** | Standard Linux, easier SW | ~$600 | 2-3 weeks | ❌ |
| **Raspberry Pi 5** | Low cost, long lead times | ~$150 | 6+ months backlog | ❌ |

#### Why This Decision (Rationale)
1. **NVIDIA ecosystem:** YOLOv8 + TensorRT officially supported, well-documented
2. **Performance:** Xavier NX sufficient for <100ms inference; Orin only if modeling exceeds capacity
3. **Compliance:** ARM-based, fanless operation fits factory floor safety (no dust circulation)
4. **Longevity:** NVIDIA maintains LTS support; vendor continuity strong
5. **Precedent:** Many 3C integrators use Jetson; existing supplier relationships in China

#### Tradeoff Analysis
- **Pro Xavier NX:** Cost efficient, adequate performance for Phase 1
- **Pro Orin:** Future-proofs capacity if models grow (multi-board simultaneous processing)
- **Recommendation:** Start with Xavier NX; upgrade path to Orin if validation shows need

#### Impact
- **Procurement:** Activate Jetson supplier ASAP (long lead time)
- **Development:** Engineer sets up CUDA dev environment (2-3 days effort)
- **Risk:** If inference latency >150ms with Xavier NX, must upgrade to Orin (cost: +$600, delay: 2 weeks)

#### Who Decided
Kaige + Systems Engineer (pending final sign-off week 2)

#### Related Issues
- [GitHub Issue #3] Hardware BOM finalization (link when repo created)

#### Approval Status
- [ ] Systems Engineer confirmed Xavier NX workload capacity
- [ ] Hardware Engineer sourced supplier, confirmed lead time
- [ ] Finance approved $800 / unit cost

---

### Decision D004: First PoC Station - Deep Diagnosis (Recommended)

**Date:** 2026-04-08 (pending validation in week 1-2)  
**Decision ID:** D004  
**Status:** 🟡 **Pending Stakeholder Confirmation**

#### What We Decided (Recommended)
Focus **Phase 1B PoC on Deep Diagnosis station** (L2/L3 technician inspection replacement), not Receiving intake.

#### Options & Rationale
| Station | Labor Cost | Complexity | Data Available | Suggested Timing |
|---------|-----------|-----------|-----------------|-----------------|
| **Receiving** (OCR + routing) | Medium | Low | Limited | Phase 2 (after PoC) |
| **Deep Diagnosis** (defect detection) | **High** | Medium | Abundant (1000+ boards/month) | **Phase 1B PoC** ✅ |
| **Appearance** (liability) | Low | High | Moderate | Phase 2 |

#### Why This Recommendation
1. **ROI clarity:** Highest labor impact (3-4 L2/L3 techs @ $60K/year each)
2. **Data richness:** Pegatron RMA center has massive dataset of damaged boards; easy to collect training images
3. **Validation speed:** 2-week field test can validate 200+ actual diagnostics
4. **Risk:** ML model performance on real data directly determines project viability; best to validate early
5. **Scope clarity:** Pure ML/vision problem; fewer external dependencies (no OCR libs, no PLC tuning)

#### Impact
- **Data collection (week 5):** 200-500 PCB images across top 10 failure modes
- **Model training (week 6):** Fine-tune YOLOv8m on Pegatron-specific boards
- **Field validation (weeks 9-10):** Run live diagnostics, compare vs. technician assessment
- **Scalability:** If successful, can replicate to other board types/factories; if unsuccessful, pivot to Receiving station

#### Tradeoff: Why Not Receiving First?
- ✅ Receiving would be faster to deploy (OCR is commodity tech)
- ❌ But it doesn't validate the **core risk** (can we detect defects better than humans?)
- ❌ Receiving success doesn't guarantee Pegatron buys; diagnosis success does

#### Who Decided
Kaige + Tech Lead recommendation; pending Pegatron RMA manager confirmation

#### Approval Status
- [ ] Pegatron confirms Deep Diagnosis is highest priority pain point
- [ ] Pegatron grants access to 1000+ recent RMA boards for training data
- [ ] Finance confirms $50K budget allocation for Deep Diagnosis PoC hardware

#### Related Issues
- [GitHub Issue #4] PoC specification (link when created)

---

### Decision D005: Data Privacy - Local Processing, No Cloud

**Date:** 2026-04-08  
**Decision ID:** D005  
**Status:** ✅ **Active**

#### What We Decided
All image processing & ML inference happens **on-site Jetson edge gateway**. No cloud upload, no external ML APIs. All logs stored locally (or optionally encrypted local cloud backup).

#### Context & Options Evaluated
| Option | Privacy | Performance | Cost | Compliance | Vote |
|--------|---------|-------------|------|-----------|------|
| **Local processing (chosen)** | Highest | Latency <100ms | $50K hardware | GDPR/HIPAA friendly | ✅ |
| **Cloud ML API (Azure/AWS)** | Lower (cloud provider governs) | <50ms but network dependent | $5K-10K/month | Requires data transfer agreement | ❌ |
| **Hybrid (local + cloud backup)** | Medium | Fast | $10K-15K/month | Depends on backup encryption | 🤔 |

#### Why This Decision
1. **Pegatron preference:** As major supplier to Walmart, Amazon (B2B) + own DTC channel, data residency is critical
2. **Compliance:** HIPAA (if processing any personal device data), GDPR (EU devices) all satisfied with local processing
3. **Cost:** No recurring cloud fees; 1-time hardware capex only
4. **Performance:** Eliminates network latency; more reliable in factory environment
5. **IP protection:** Training data never leaves Pegatron's facility; model can be kept proprietary

#### Impact
- **Inference pipeline:** All processing on Jetson; no external API calls
- **Logging:** Local SQLite or PostgreSQL database; historical data stored on-site
- **Backup strategy:** USB external drive or optional encrypted local NAS (decision deferred)
- **Monitoring:** On-site dashboard only (no public cloud dashboarding)

#### Risk Mitigation
- If edge hardware fails: Fallback manual review (temporary)
- If data loss: Daily backups to encrypted external drive

#### Who Decided
Kaige (Project Lead) + Pegatron IT security team confirmation

#### Related Issues
- [GitHub Issue #5] Compliance & data privacy checklist (link when created)

---

### Decision D006: Timeline - 14-24 Weeks Total (3 Phases)

**Date:** 2026-04-08  
**Decision ID:** D006  
**Status:** ✅ **Active**

#### What We Decided
Project structured in **3 phases over 14-24 weeks:**
- **Phase 0 (weeks 1-2):** Inception & planning
- **Phase 1A (weeks 3-6):** PoC design & team kickoff
- **Phase 1B (weeks 7-14):** PoC execution & validation
- **Go/No-Go gate (week 14):** Pegatron decides to proceed to full design
- **Phase 2 (weeks 15-19, if Go):** Full system design (all 5 stations)
- **Phase 3 (weeks 20-24, if Go):** Implementation & deployment

#### Alternative Timelines Considered
| Timeline | Pros | Cons | Vote |
|----------|------|------|------|
| **Fast-track (8 weeks)** | Quick to market | High risk, insufficient validation | ❌ |
| **Phased (14-24 weeks, chosen)** | Risk-managed, stakeholder buy-in at gates, iterative | Longer to revenue | ✅ |
| **Slow (36+ weeks)** | Over-engineered, pristine docs | Opportunity window closes, market moves | ❌ |

#### Why This Decision
1. **Risk management:** PoC validation (weeks 7-14) is non-negotiable before scaling to Phase 2
2. **Stakeholder alignment:** Go/No-Go gate at week 14 forces explicit Pegatron commitment; prevents scope creep
3. **Resource efficiency:** Phase 0 used to hire & equip; Phase 1 to validate model; Phase 2+ to scale
4. **Market window:** Pegatron has CEO visibility on this initiative; 6-month delivery shows momentum

#### Assumptions Behind Timeline
- Hardware arrives on schedule (4-6 weeks from PO)
- Pegatron provides access for data collection (week 5) and validation (weeks 9-10)
- ML model reaches >85% F1 on field data (achievable given robust training data)
- No major architectural pivots required

#### Risk Mitigation
- If hardware delayed: Parallel simulation environment (CPU-based inference, slower but validates logic)
- If model accuracy stalls: Extend week 6 data collection; add data augmentation; consider transfer learning from commercial PCB datasets
- If Pegatron unavailable: Virtual data collection + asynchronous feedback loops

#### Who Decided
Kaige (Project Lead) with input from Pegatron RMA center manager

#### Status
- ✅ Phase 0 start: Apr 8, 2026
- ⏳ Phase 1A start: Expected Apr 22, 2026 (contingent on Phase 0 completion)

#### Related Issues
- [GitHub Issue #6] ROADMAP.md, milestone tracking (link when created)

---

### Decision D007: Team Structure - 1 ML + 1 Systems + 0.5 Hardware (PoC Phase)

**Date:** 2026-04-08  
**Decision ID:** D007  
**Status:** 🟡 **Pending Recruitment**

#### What We Decided
Recruit **4-person core team for PoC phase (weeks 1-14):**
1. ML Engineer (1.0 FTE)
2. Systems/Integration Engineer (1.0 FTE)
3. Hardware Engineer (0.5 FTE)
4. Project Lead (Kaige, 0.8 FTE; remaining 0.2 FTE on other projects)

Optional: Frontend Engineer (0.5 FTE) for dashboard.

#### Justification
| Role | PoC Need | Phase 2+ Need | Rationale |
|------|----------|-------------|-----------|
| ML Engineer (1.0 FTE) | **Essential** | 0.5 FTE | Core technical risk; data collection & model tuning critical path |
| Systems Engineer (1.0 FTE) | **Essential** | 1.0 FTE | Edge gateway + PLC integration; on-site deployment support |
| Hardware Engineer (0.5 FTE) | Important | 1.0 FTE | Vendor evaluation (weeks 1-3); then part-time support through deployment |
| Frontend Engineer (0.5 FTE) | Optional | 1.0 FTE | Dashboard is nice-to-have for PoC; essential for Phase 2+ multi-location visibility |
| Project Lead (0.8 FTE) | **Essential** | 1.0 FTE | Stakeholder management, decision-making, risk ownership |

#### Why This Sizing
1. **PoC is tech-risk validation:** ML (model accuracy) + Systems (integration) are critical; Hardware (vendor procurement) is important but less complex
2. **Lean startup ethos:** 4-5 people enough for PoC; no excessive overhead
3. **Skill specialization:** Each role has clear ownership; no ambiguity
4. **Scalability:** Phase 2+ adds capacity as scope expands (multi-station, training, documentation)

#### Budget Impact
- **PoC phase labor (14 weeks):** ~$200K (2.3 FTE @ avg $65K/year)
- **Phase 2-3 labor (10 weeks):** ~$250K (4.5 FTE)
- **Total project labor:** ~$450K
- **Total hardware/software/services:** ~$130K-200K
- **Total project cost:** ~$580K-650K

#### Timeline for Recruitment
- [ ] Week 1 (Apr 8-14): Post job descriptions, screen candidates
- [ ] Week 2 (Apr 15-21): Interviews, offers
- [ ] Week 3 (Apr 22): Onboarding start (some roles may start mid-week)

#### Risks & Contingency
- **If ML candidate unavailable:** Contract ML consultant ($50K-100K for PoC phase)
- **If Systems candidate unavailable:** Kaige takes temporary lead; hire for Phase 2
- **If timeline pressure:** Add Frontend Engineer immediately (no waiting for Phase 2)

#### Who Decided
Kaige (Project Lead) based on scope + risk assessment

#### Status
- 🟡 **Recruiting:** ML Engineer, Systems Engineer open
- 🟡 **Recruiting:** Hardware Engineer (0.5 FTE, may be internal)

---

## Decision Templates

### For Future Decisions

```markdown
### Decision D00X: [Brief Title]

**Date:** YYYY-MM-DD  
**Decision ID:** D00X  
**Status:** 🟡 **Pending** | ✅ **Active** | ⚠️ **Superseded** | 🗑️ **Archived**

#### What We Decided
[Clear statement of decision]

#### Context & Options Evaluated
[Table of options + pros/cons]

#### Why This Decision
[Numbered reasoning]

#### Impact
[Bullet list of consequences]

#### Who Decided
[Name + role]

#### Related Issues
[Links to GitHub Issues]

#### Approval Status
- [ ] Stakeholder A confirmed
- [ ] Stakeholder B approved
```

---

## Decision Index (Quick Reference)

| ID | Title | Date | Status |
|----|----|------|--------|
| D001 | RMA vs Production Line | 2026-04 | ✅ Active |
| D002 | "Don't Rebuild Wheels" Strategy | 2026-04 | ✅ Active |
| D003 | Jetson Edge Gateway Hardware | 2026-04-08 | 🟡 Pending |
| D004 | Deep Diagnosis as PoC Station | 2026-04-08 | 🟡 Pending |
| D005 | Local Processing, No Cloud | 2026-04-08 | ✅ Active |
| D006 | 14-24 Week Timeline | 2026-04-08 | ✅ Active |
| D007 | Team Structure (4-5 people PoC) | 2026-04-08 | 🟡 Pending |

---

*Last Updated: 2026-04-08 by Kaige Liao (Leo)*  
*Next Update: Weekly during Phases 1-2*
