# Project Roadmap: Pegatron RMA Intelligent Vision & Automation

**Last Updated:** 2026-04-08  
**Project Lead:** Kaige Liao (Leo)  
**Timeline:** 14-24 weeks (PoC through deployment)

---

## 📅 High-Level Timeline

```
Week 1-2 (Apr 8-21)     │ Week 3-6 (Apr 22-May 19)  │ Week 7-14 (May 20-Jul 8)   │ Week 15-24 (Jul 9-Sep 2)
─────────────────────────┼────────────────────────────┼─────────────────────────────┼──────────────────────────
Inception & Planning     │ PoC Design & Team Kickoff  │ PoC Execution & Validation  │ Full Design & Deployment
      (PHASE 0)         │         (PHASE 1A)         │         (PHASE 1B)          │       (PHASE 2-3)
```

---

## 🎯 Phase 0: Project Inception & Planning (Weeks 1-2)

**Objective:** Establish repo structure, validate supply chain options, finalize PoC scope, confirm team.

### Deliverables

| Deliverable | Owner | Due | Status |
|-------------|-------|-----|--------|
| GitHub repo architecture + CI/CD skeleton | Kaige | Apr 10 | 🟡 In Progress |
| Supply chain rapid assessment (3 vendors) | TBD | Apr 12 | ⏳ Not Started |
| PoC specification finalized | Kaige + Tech Lead | Apr 15 | ⏳ Not Started |
| Team roles & skills matrix defined | Kaige | Apr 10 | ⏳ Not Started |
| Budget & resource request submitted | Kaige | Apr 15 | ⏳ Not Started |

### Key Tasks

**Week 1 (Apr 8-14)**
- [ ] **Repo Setup** (Kaige)
  - Finalize directory structure
  - Create core docs (charter, README, contributing)
  - Set up GitHub Projects board
  - Configure branch protection rules

- [ ] **Supply Chain Kick-Off** (Hardware Engineer TBD)
  - Contact 3+ vision tunnel vendors (Basler, IDS, FLIR)
  - Collect spec sheets, pricing, lead times
  - Create vendor comparison matrix in `docs/02_SUPPLY_CHAIN_ANALYSIS.md`

- [ ] **Team Assembly** (Kaige)
  - Confirm ML engineer availability
  - Confirm systems/integration engineer
  - Brief team on project scope & phase
  - Create team Slack/async comms channel

**Week 2 (Apr 15-21)**
- [ ] **PoC Specification Lock** (Kaige + Tech Lead)
  - Finalize hardware Bill of Materials (BoM)
  - Lock first station selection (likely: Receiving + Deep Diagnosis)
  - Define success criteria (latency, accuracy, cost)
  - Create `docs/03_POC_SPECIFICATION.md`

- [ ] **Architecture Skeleton** (Systems Engineer)
  - Design edge gateway deployment topology
  - PLC communication protocol selection (Modbus vs OPC-UA)
  - Data flow diagram (receiving → diagnosis → dispatch)
  - Start `docs/04_TECHNICAL_ARCHITECTURE.md`

- [ ] **Budget & Procurement** (Kaige)
  - Finalize hardware budget (target: $50K for PoC)
  - Submit POs for long-lead items (vision tunnel, Jetson)
  - Identify contingency vendors

### Success Criteria
- ✅ Repo ready for active team collaboration
- ✅ Supply chain options narrowed to 1-2 preferred vendors
- ✅ PoC scope locked & communicated
- ✅ Team confirmed & onboarded
- ✅ Hardware procurement underway

### Next Phase Gate
→ Proceed to **Phase 1A** if all above complete. If supply chain delays, initiate plan B vendor.

---

## 🟡 Phase 1A: PoC Design & Team Kickoff (Weeks 3-6)

**Objective:** Detailed design, procure PoC hardware, set up local development environment, establish Pegatron communication.

### Deliverables

| Deliverable | Owner | Due | Status |
|-------------|-------|-----|--------|
| PoC hardware & software BOM | Hardware Eng | Apr 28 | ⏳ Not Started |
| Edge gateway baseline image | Systems Eng | May 5 | ⏳ Not Started |
| ML dataset collection plan | ML Eng | Apr 26 | ⏳ Not Started |
| Pegatron engagement framework | Kaige | Apr 30 | ⏳ Not Started |

### Key Tasks

**Week 3 (Apr 22-28)**
- [ ] **Hardware Finalization** (Hardware Engineer)
  - Confirm selected vendors, finalize specs
  - Order vision tunnel, Jetson, GigE cables, mounting hardware
  - Create detailed BoM with part numbers, costs, lead times
  - Estimate hardware arrival date

- [ ] **Data Collection Planning** (ML Engineer)
  - Define defect taxonomy (crack, cold solder, corrosion, etc.)
  - Plan on-site image collection at Pegatron (dates, lighting setup)
  - Estimate dataset size needed (~1K-5K labeled images for MVP)
  - Create data annotation strategy

- [ ] **Pegatron Communication Kickoff** (Kaige)
  - Schedule formal engagement call with RMA center manager
  - Confirm on-site access dates for data collection
  - Discuss compliance requirements (data privacy, electrical safety)
  - Identify on-site technical point of contact

**Week 4 (Apr 29-May 5)**
- [ ] **Edge Gateway Baseline** (Systems Engineer)
  - Set up NVIDIA Jetson dev environment (Docker, CUDA toolkit)
  - Deploy YOLOv8 runtime + TensorRT
  - Create Modbus client stub
  - Document setup in `software/edge-gateway/README.md`

- [ ] **Integration Framework** (Systems Engineer)
  - Design vision → diagnosis → PLC routing logic
  - Create message schema (JSON payload: defect findings, confidence, timestamp)
  - Set up local simulator for testing (mock PLC, mock vision input)

- [ ] **ML Baseline Model** (ML Engineer)
  - Download YOLOv8m pre-trained weights
  - Evaluate on publicly available PCB defect datasets (if available)
  - Establish baseline performance metrics
  - Plan fine-tuning strategy for Pegatron-specific boards

**Week 5 (May 6-12)**
- [ ] **On-Site Data Collection** (ML Eng + Kaige)
  - Deploy to Pegatron facility for 2-3 days
  - Capture 200-500 high-quality images across common failure modes
  - Document lighting conditions, camera angles, board types
  - Preliminary annotation (taxonomy confirmation)

- [ ] **Dashboard Prototype** (Frontend Engineer)
  - Create minimal diagnostic dashboard
  - Real-time defect detection display
  - Simple alerts system
  - Stack: React + WebSocket to Jetson

**Week 6 (May 13-19)**
- [ ] **PoC Integration Test** (Systems Engineer + ML Engineer)
  - Connect vision input → edge gateway → mock PLC
  - Test latency end-to-end (<200ms target)
  - Validate message passing (defect output → PLC command)
  - Document test results

- [ ] **Model Fine-Tuning Sprint** (ML Engineer)
  - Annotate collected images (priority: top 10 failure modes)
  - Fine-tune YOLOv8m on Pegatron-specific boards
  - Evaluate accuracy (F1, precision, recall on validation set)
  - Freeze v1.0 model weights

- [ ] **Safety & Compliance Kick-Off** (Systems Engineer + Kaige)
  - Review OSHA electrical safety requirements
  - Design arc flash / electrical hazard mitigation
  - Confirm data privacy approach (local processing, no cloud)
  - Start `docs/05_COMPLIANCE_CHECKLIST.md`

### Success Criteria
- ✅ PoC hardware purchased & delivering on schedule
- ✅ On-site data collection complete (200+ images)
- ✅ Edge gateway runtime working (YOLOv8 + TensorRT)
- ✅ Vision → PLC message routing designed
- ✅ Baseline model trained & deployed to Jetson
- ✅ Dashboard functional (MVP level)
- ✅ Pegatron formally engaged, compliance questions documented

### Risks & Mitigation
| Risk | Mitigation |
|------|-----------|
| Hardware supply delays | Activate plan B vendor; parallel setup with alternate hardware |
| Model accuracy <80% | Extend data collection; evaluate alternative architectures |
| Pegatron unavailable for 2-3 day visit | Schedule flexibility; virtual data collection alternative |

### Next Phase Gate
→ Proceed to **Phase 1B** if PoC hardware received, model F1 >80%, integration test passed.

---

## 🔵 Phase 1B: PoC Execution & Validation (Weeks 7-14)

**Objective:** Run PoC at Pegatron, validate ROI, design next station, gather customer feedback.

### Deliverables

| Deliverable | Owner | Due | Status |
|-------------|-------|-----|--------|
| PoC deployed & running at site | Systems Eng | Jun 2 | ⏳ Not Started |
| 2-week field validation complete | ML Eng + Kaige | Jun 16 | ⏳ Not Started |
| ROI analysis & business case updated | Kaige | Jun 20 | ⏳ Not Started |
| Next station design (Appearance Assessment) | Kaige | Jun 23 | ⏳ Not Started |

### Key Tasks

**Week 7-8 (May 20-Jun 2)**
- [ ] **PoC Field Deployment** (Systems Engineer + ML Engineer)
  - Ship Jetson + vision hardware to Pegatron
  - On-site installation (mounting, network, power)
  - Run smoke tests (vision captures, model inference, PLC communication)
  - Set up monitoring dashboard for remote observation

- [ ] **Parallel: Next Station Design** (Kaige + Tech Lead)
  - Finalize Receiving/Intake station automation design
  - OCR engine selection (Tesseract vs commercial API)
  - Physical routing mechanism (conveyor sensors, barcode scanners)
  - Begin `docs/03_POC_SPECIFICATION.md` **Part 2** (Receiving station)

**Week 9-10 (Jun 3-16)**
- [ ] **PoC Field Validation** (ML Eng, Systems Eng at site 1 week)
  - Run live diagnostics on 200+ actual RMA boards
  - Compare model predictions vs L2/L3 technician assessment
  - Log all false positives / false negatives
  - Measure latency, uptime, reliability

- [ ] **Data Analysis & Reporting** (ML Engineer)
  - Calculate precision, recall, F1 on field data
  - Identify failure modes (if any)
  - Cost-benefit analysis: PoC labor savings vs hardware cost
  - Document learnings in `field-notes/poc_validation_report_jun2026.md`

**Week 11-12 (Jun 17-30)**
- [ ] **ROI & Business Case Update** (Kaige)
  - Quantify labor reduction (L2/L3 technician hours saved)
  - Compare against hardware + software costs
  - Project payback period
  - Present to Pegatron leadership
  - Update financial assumptions in charter

- [ ] **Design Review & Decision** (Kaige + Pegatron)
  - Present PoC results to Pegatron stakeholders
  - **Go / No-Go decision:** Proceed to full design (Weeks 15+)?
  - If **Go:** Confirm scope for Phase 2 (multi-station rollout)
  - If **No-Go:** Document learnings, plan pivot

**Week 13-14 (Jul 1-8)**
- [ ] **Phase 2 Prep** (All teams)
  - If Go: Begin detailed design for Receiving + Appearance stations
  - Freeze PoC model, prepare for production optimization
  - Create deployment & training documentation
  - Plan Week 15 team onboarding for Phase 2 ramp-up

### Success Criteria
- ✅ PoC running live at Pegatron for 2+ weeks
- ✅ Model achieves >85% F1 on field data
- ✅ System uptime >95%
- ✅ Clear ROI demonstrated (payback <18 months)
- ✅ Pegatron approves Phase 2 scope
- ✅ Zero safety incidents

### Risks & Mitigation
| Risk | Mitigation |
|------|-----------|
| Model fails on real boards | Rapid fine-tuning loop; fallback to manual review |
| PLC communication unstable | Redundant Modbus setup; watchdog restart logic |
| Pegatron delays feedback | Pre-scheduled daily sync calls; weekly reports |

### Next Phase Gate
→ Proceed to **Phase 2** (Full Design) if PoC validated, ROI positive, Pegatron approves.  
→ If No-Go: Document pivot strategy, assess next opportunity.

---

## 🟢 Phase 2: Full System Design (Weeks 15-19)

**Objective:** Design all 5 stations, finalize architecture, prepare for deployment.

### High-Level Tasks
- Receiving + Intake automation (OCR + routing)
- Appearance Assessment (digital imaging + rule engine)
- Deep Diagnosis v2 (improved model, additional board types)
- Repair & Dispatch (PLC integration)
- Closeout (automated labeling)

### Deliverables
- Complete technical architecture (`docs/04_TECHNICAL_ARCHITECTURE.md`)
- Hardware & software BoM (full system)
- Deployment runbook (`docs/06_DEPLOYMENT_GUIDE.md`)
- Compliance approval checklist (`docs/05_COMPLIANCE_CHECKLIST.md`)

---

## 🟠 Phase 3: Implementation & Deployment (Weeks 20-24)

**Objective:** Build, test, deploy, train.

### High-Level Tasks
- Procure remaining hardware (Receiving sensors, cleaning equipment)
- Build software modules (OCR, PLC drivers, integrations)
- On-site installation & integration
- Staff training & operational handover
- Monitoring & optimization (first 4 weeks live)

### Deliverables
- Working system at Pegatron (all 5 stations)
- Operational documentation & runbooks
- Staff training completed
- 24/7 monitoring & support in place

---

## 📊 Success Metrics (End of Project)

| Metric | Target | Validation |
|--------|--------|-----------|
| **Labor reduction** | 30-40% fewer L2/L3 technicians | Time tracking data from Pegatron |
| **Defect detection accuracy** | >90% F1 across all board types | Field validation on 500+ boards |
| **System uptime** | >98% | Monitoring logs over 4 weeks |
| **RMA cycle time reduction** | 20-30% | Timestamp data from start → closeout |
| **Cost payback period** | <18 months | ROI analysis vs hardware/software costs |
| **Compliance** | OSHA + UL + data privacy | Audit report from Pegatron |
| **Replicability** | Clear playbook for next factory | Documented "standard model" |

---

## 📋 Assumptions & Dependencies

### Assumptions
- Pegatron provides on-site access during weeks 7-8, 9-10, 20-24
- Hardware vendors deliver within 4-6 weeks of PO
- 1,000+ labeled images sufficient for >85% model accuracy
- Current RMA volume enables 2-week validation window
- Budget remains as proposed

### External Dependencies
- NVIDIA Jetson availability (global chip shortage?)
- Vision hardware vendor lead times (currently 4-8 weeks)
- Pegatron facility downtime approval (likely weekend/night shifts)
- Data privacy compliance (state, federal data handling rules)

### Internal Dependencies
- ML engineer availability (>50% capacity, weeks 1-14)
- Systems engineer for PLC integration (weeks 1-24)
- Project lead decision-making cadence (weekly async)

---

## 🔄 Monitoring & Course Correction

### Weekly Sync (Optional, 30 min)
- Current week progress
- Blockers & asks
- Next week priorities

### Milestone Reviews (Mandatory)
- **Week 2 End (Apr 21):** Phase 0 → 1A gate
- **Week 6 End (May 19):** Phase 1A → 1B gate
- **Week 14 End (Jul 8):** Phase 1B → 2 gate (Go/No-Go)
- **Week 19 End (Aug 12):** Phase 2 → 3 gate

### Tracking
- GitHub Projects board for task visibility
- Milestone labels for filtering Issues
- Weekly status updates in Discussions

---

## 📝 Change Request Process

If scope or timeline needs adjustment:
1. Open Issue: `[CHANGE-REQUEST] Title`
2. Document impact (schedule, budget, risk)
3. Get approval from project lead
4. Update ROADMAP + `decision_log.md`
5. Communicate to team & stakeholders

---

*Last Updated: 2026-04-08 by Kaige Liao (Leo)*
