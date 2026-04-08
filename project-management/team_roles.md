# Team Roles & Responsibilities

**Document Version:** v1.0  
**Last Updated:** 2026-04-08  
**Owner:** Kaige Liao (Leo)

---

## 👥 Team Structure

```
┌─────────────────────────────────────────────────────┐
│ Project Lead: Kaige Liao (Leo)                      │
│   • Strategic direction, Go/No-Go decisions         │
│   • Stakeholder communication (Pegatron, business)  │
│   • Risk management, timeline enforcement           │
└─────────────────────────────────────────────────────┘
           ▼           ▼            ▼           ▼
    ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌──────────┐
    │ ML Eng  │  │Hardware │  │Systems/ │  │ (Optional)
    │ (1 FTE) │  │Engineer │  │Integr.  │  │ Frontend │
    │         │  │(0.5 FTE)│  │Engineer │  │ Engineer │
    │         │  │         │  │(1 FTE)  │  │(0.5 FTE) │
    └─────────┘  └─────────┘  └─────────┘  └──────────┘
```

---

## 🎯 Role Definitions & KPIs

### Role: Project Lead (Kaige Liao / Leo)

**Reports To:** Stakeholder board (implicit)

**Key Responsibilities:**
1. **Strategic Vision & Roadmap**
   - Define project phases and success criteria
   - Maintain alignment with Pegatron's business needs
   - Pivot strategy if data suggests course correction needed

2. **Team & Resource Management**
   - Recruit and onboard team members
   - Allocate capacity across phases
   - Facilitate async communication and decision-making

3. **Stakeholder Engagement**
   - Weekly/bi-weekly sync with Pegatron RMA center manager
   - Regular ROI analysis and business case updates
   - Present findings and recommendations to leadership
   - Manage contract and compliance obligations

4. **Risk & Budget Oversight**
   - Track project spend vs. budget ($50K PoC, $80K-150K full system)
   - Identify and escalate risks early
   - Approve change requests and scope adjustments

5. **Decision Making**
   - Final authority on technical trade-offs (cost vs. performance)
   - Schedule and facilitate milestone gates
   - Log all strategic decisions in `decision_log.md`

**Key Metrics / KPIs:**
- Project delivered on time & within budget
- Stakeholder satisfaction (Pegatron feedback)
- Team velocity & morale
- ROI analysis accuracy (within 10% of actual)

**Success Criteria for This Role:**
- ✅ Phase 0 complete by Apr 21 (repo, supply chain, team confirmed)
- ✅ PoC deployed by Jun 2, validated by Jun 16
- ✅ Pegatron Go/No-Go decision by Jul 8
- ✅ Zero surprises; all decisions logged and communicated

**Communication Cadence:**
- Async: Daily status updates (GitHub Issues/Discussions)
- Sync: Weekly 30-min optional standup (team)
- Sync: Bi-weekly with Pegatron (as negotiated)
- Decision logs: Real-time as decisions made

---

### Role: ML (Machine Learning) Engineer

**Reports To:** Project Lead (Kaige)

**Allocation:** 1 FTE for PoC phase (weeks 1-14), 0.5 FTE for Phase 2-3

**Key Responsibilities:**

1. **Data Strategy & Collection**
   - Define defect taxonomy (crack, cold solder, corrosion, etc.)
   - Plan on-site image collection (dates, lighting, angles)
   - Coordinate with Pegatron for access to RMA boards

2. **Model Development**
   - Select baseline architecture (YOLOv8m recommended)
   - Train on Pegatron-specific board types
   - Optimize for edge deployment (TensorRT quantization, latency <100ms)
   - Iterate on accuracy (target >85% F1)

3. **Validation & Field Testing**
   - Deploy model to edge gateway
   - Run 2-week field validation at Pegatron (week 9-10)
   - Compare predictions vs. technician assessments
   - Document false positives/negatives

4. **Documentation**
   - Model card: architecture, training data, performance metrics
   - Training runbook: data prep, fine-tuning, evaluation
   - Field notes: defect taxonomy, model limitations, retraining strategy

**Key Deliverables:**
- [ ] Week 4: Baseline model (YOLOv8m on public PCB datasets)
- [ ] Week 6: Fine-tuned model v1.0 (trained on Pegatron data)
- [ ] Week 10: Field validation report (precision, recall, F1)
- [ ] Week 14: Production-ready model + retraining playbook

**Success Criteria:**
- ✅ Model F1 >85% on field data (week 10 validation)
- ✅ Inference latency <100ms per board
- ✅ Clear documentation of dataset, methodology, limitations
- ✅ Model reproducible from code + config (no black boxes)

**KPIs:**
- Model accuracy (F1 score)
- Inference latency (ms per board)
- Time-to-accuracy (weeks to reach 85% F1)
- Field validation pass rate

**Communication:**
- Daily: Short async update (Slack/GitHub)
- 2x weekly: Sync with Systems Engineer (integration testing)
- Weekly: Status for project lead
- On-site presence: Weeks 5 (data collection), 9-10 (field validation)

**Risks:**
- Model accuracy plateaus at <80%: Activate data augmentation, architecture search
- Hardware unavailable: Use CPU simulation, delayed edge deployment
- Pegatron data insufficient: Extend data collection, augment with synthetic data

---

### Role: Hardware Engineer

**Reports To:** Project Lead (Kaige)

**Allocation:** 0.5 FTE for PoC phase (weeks 1-6), 1 FTE for Phase 2-3

**Key Responsibilities:**

1. **Vendor Evaluation & Procurement**
   - Research 3+ vision tunnel / multi-spectral camera vendors
   - Collect specs, pricing, lead times
   - Create comparison matrix (`docs/02_SUPPLY_CHAIN_ANALYSIS.md`)
   - Recommend best fit (cost + lead time + capability)

2. **Bill of Materials (BoM)**
   - Compile detailed BoM with part numbers, qty, cost
   - Track lead times and expected delivery dates
   - Identify long-lead items; escalate delays early

3. **Hardware Integration**
   - Design vision tunnel mounting (mechanical drawings)
   - Specify cabling (GigE, power, misc.)
   - Coordinate with Systems Engineer on connectivity
   - Create hardware setup guide for on-site deployment

4. **On-Site Hardware Setup** (Weeks 7-8)
   - Oversee hardware installation at Pegatron
   - Validate camera calibration, lighting
   - Troubleshoot connectivity issues
   - Create setup documentation

**Key Deliverables:**
- [ ] Week 1-2: Vendor comparison + recommendation
- [ ] Week 3: Hardware BoM locked + POs submitted
- [ ] Week 4: Hardware specs confirmed with suppliers
- [ ] Week 8: Hardware installed & validated on-site

**Success Criteria:**
- ✅ Hardware delivered on schedule (no slippage >1 week)
- ✅ Vision system captures high-quality images (>95% usable)
- ✅ Multi-spectral lighting setup reproducible across sites
- ✅ All BoM documented for future replication

**KPIs:**
- Lead time accuracy (actual vs. quoted)
- Hardware cost vs. budget
- Installation time (on-site setup)
- Image quality metrics (resolution, clarity, consistency)

**Communication:**
- Daily: Vendor coordination (email/calls)
- Weekly: Status for project lead + supply chain update in `docs/02_...`
- Coordination sync: 1x weekly with Systems Engineer
- On-site presence: Weeks 7-8 (installation), potentially week 20-24 (scaling)

**Risks:**
- Vendor delays (chip shortage): Activate plan B vendor, adjust timeline
- High cost: Negotiate bulk pricing, consider alternative hardware
- Image quality issues: Extended characterization, lighting redesign

---

### Role: Systems / Integration Engineer

**Reports To:** Project Lead (Kaige)

**Allocation:** 1 FTE for PoC phase (weeks 1-14), 1 FTE for Phase 2-3

**Key Responsibilities:**

1. **Edge Gateway Design & Implementation**
   - Select hardware (NVIDIA Jetson Xavier NX / Orin)
   - Set up dev environment (Docker, CUDA, YOLOv8 runtime)
   - Deploy TensorRT for optimized inference
   - Create baseline image for easy replication

2. **PLC Integration**
   - Design communication protocol (Modbus TCP / OPC-UA)
   - Implement PLC client/server (Python or equivalent)
   - Route vision output → diagnostic decision → PLC command
   - Test message passing end-to-end

3. **Data Flow & Auditability**
   - Design message schema (defect findings, confidence, timestamp)
   - Plan data logging & archival (local storage or optional cloud)
   - Ensure OSHA/compliance-friendly traceability
   - Document data retention policy

4. **Monitoring & Health Checks**
   - Deploy health check agent (system status, model inference timing)
   - Create alerting (if inference latency exceeds threshold, alert)
   - Set up remote observability for field-deployed systems

5. **On-Site Deployment & Support**
   - Coordinate installation with Hardware Engineer
   - Deploy edge gateway, validate connectivity
   - Run smoke tests (vision capture, inference, PLC commands)
   - Provide 24/7 escalation support during validation phase

**Key Deliverables:**
- [ ] Week 2: Edge gateway design document + tech stack rationale
- [ ] Week 4: Edge gateway baseline image (working YOLOv8 + TensorRT)
- [ ] Week 4: Modbus client implementation + documentation
- [ ] Week 6: Integration test (vision → diagnosis → PLC)
- [ ] Week 8: On-site deployment & validation
- [ ] Week 12: Monitoring dashboard + health check playbook

**Success Criteria:**
- ✅ End-to-end latency <200ms (vision → PLC command)
- ✅ System uptime >95% during 2-week validation
- ✅ All communication logged & auditable
- ✅ Clear runbooks for on-site troubleshooting

**KPIs:**
- System availability (uptime %)
- Inference latency (ms)
- Message delivery reliability (% delivered on first attempt)
- Support response time (hours to resolution)

**Communication:**
- Daily: Sync with ML Engineer (integration testing)
- Weekly: Status for project lead + architecture updates
- 2x weekly: PLC integration check-in with Pegatron IT
- On-site presence: Weeks 7-8, 9-10 (validation), 20-24 (deployment)

**Risks:**
- PLC communication protocol mismatch: Parallel protocol evaluation
- Latency exceeds budget: Model quantization, hardware upgrade
- Network instability at Pegatron: Redundancy design, fallback modes

---

### Role: Frontend Engineer (Optional, 0.5 FTE)

**Reports To:** Systems Engineer (Kaige as escalation)

**Allocation:** 0.5 FTE for weeks 4-14, 1 FTE for Phase 2+

**Key Responsibilities:**

1. **Monitoring Dashboard**
   - Real-time display of defect detections
   - System health metrics (uptime, latency)
   - Alerts & notifications
   - Historical trend analysis

2. **Admin Interface** (Phase 2+)
   - System configuration (camera calibration, model thresholds)
   - Data export & reporting (CSV, PDF)
   - User management (if multi-location)

3. **UX & Accessibility**
   - Accessible to shop-floor technicians (simple, clear)
   - Mobile-friendly status view (optional)
   - Compliance with factory floor lighting/usage conditions

**Tech Stack:**
- Frontend: React + TypeScript
- Backend: Node.js API or direct WebSocket to Jetson
- Deployment: Docker container on edge gateway

**Success Criteria:**
- ✅ Dashboard loads in <1 second
- ✅ Readable in factory lighting
- ✅ No missed alerts
- ✅ Simple enough for technician self-service

---

## 📝 Team Onboarding Checklist

### New Team Member (Any Role)

- [ ] **Week 1:**
  - [ ] Read `docs/01_PROJECT_CHARTER.md`
  - [ ] Review `ROADMAP.md` and understand current phase
  - [ ] Review `decision_log.md` to understand context
  - [ ] Schedule 1:1 with Project Lead (30 min)
  - [ ] Access GitHub repo, understand structure

- [ ] **Week 2:**
  - [ ] Attend weekly team sync (if available)
  - [ ] Review relevant technical docs for your role
  - [ ] Claim first task (e.g., `good first issue`)
  - [ ] Submit first PR (can be docs-only)

- [ ] **Week 3+:**
  - [ ] Integrated into async workflow
  - [ ] Contributing to core deliverables

---

## 🤝 Collaboration Norms

### Decision Making
- **Small decisions:** PIC (person in charge) decides, logs in Issue
- **Medium decisions:** 24-48hr async discussion, lead decides
- **Large decisions:** Formal decision call (lead + stakeholders), documented

### Escalation Path
If blocked or need urgent guidance:
1. Try async in GitHub Issue (most cases)
2. Ping on Slack (escalation, not first choice)
3. Schedule sync call (blocking entire team)

### Async Conventions
- Daily standup: GitHub comment on `#standup` issue (2-3 lines)
- Decision updates: Post in Issues with context + options
- Code review: 24hr response target
- Questions: Asked in public channels (Discussions) to share knowledge

### Sync Meetings
- Weekly standup: 30 min, optional attendance
- Milestone gates: Mandatory attendance (decision points)
- 1:1s: As needed per role

---

## 🎓 Training & Skill Building

### Recommended Learning (Self-Directed)
- **All roles:** YOLOv8 basics (YouTube series, ~2 hours)
- **ML Engineer:** TensorRT optimization, edge inference patterns
- **Systems Engineer:** Modbus/OPC-UA protocol deep dive
- **Hardware Engineer:** Precision camera calibration, GigE streaming

### Knowledge Sharing
- Post learnings in Discussions → `#knowledge-base`
- Document discoveries in relevant `docs/` file
- Pair programming encouraged (async code reviews)

---

## 📊 Success Metrics for Team

| Metric | Target | How We Measure |
|--------|--------|-------|
| **Team velocity** | 80%+ planned work completed per phase | GitHub Issues closed / milestone |
| **Quality** | Zero critical bugs in production | Field support tickets |
| **Communication** | <24hr response to async asks | Issue/PR response times |
| **Morale** | High (subjective) | 1:1 feedback, sprint retrospectives |
| **Documentation** | Complete & accurate | Code reviews, field validation |

---

## 📍 Contingency & Skill Gaps

### If ML Engineer Unavailable
- Hire contract ML specialist (budget: $50K-100K for PoC phase)
- Use commercial API (e.g., AWS Lookout) as fallback
- Impact: 2-4 week delay, additional cost

### If Systems Engineer Unavailable
- Project lead picks up PLC integration (reduced bandwidth for strategy)
- Hire integrations contractor
- Impact: 2-3 week delay, additional cost

### If Hardware Engineer Unavailable
- Project lead manages vendor coordination
- Coordinate with Pegatron's procurement team
- Impact: 1-2 week delay, possible cost premium

---

## 🎯 Individual Development Plans (IDPs)

To be completed in first sync with Project Lead:

### [Role Name] Development Plan
- **Current skills:** [list]
- **Gaps to address:** [list]
- **Learning goals (next 3 months):** [list]
- **Stretch opportunities:** [e.g., present findings to Pegatron leadership]

---

*Last Updated: 2026-04-08 by Kaige Liao (Leo)*  
*Next Review: End of Phase 0 (Apr 21, 2026)*
