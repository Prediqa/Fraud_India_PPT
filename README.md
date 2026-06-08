# FraudIQ India
https://youtu.be/VbAD9banZKo


**Unified Fraud Intelligence for Insurance & Healthcare — India Deployment**

[![Stage](https://img.shields.io/badge/stage-pilot-blue)]()
[![Compliance](https://img.shields.io/badge/compliance-IRDAI%20%7C%20MeitY%20%7C%20UIDAI-green)]()
[![Data Residency](https://img.shields.io/badge/data%20residency-India%20only-orange)]()
[![License](https://img.shields.io/badge/license-proprietary-red)]()

> **Reference platform:** [FraudIQ USA](https://prediqa.github.io/FraudIQ_USA/) — the US implementation this India deployment is re-architected from.

---

## What it is

FraudIQ India is a fraud-detection and claims-intelligence layer that sits between an insurer's core system (TCS BaNCS, Guidewire, Duck Creek, legacy) and its adjudication workflow. It scores every claim and application in real time, flags fraud and overbilling before payout, and produces audit-grade evidence packages for SIU and law-enforcement referral.

The platform is built India-first: CGHS package rates rather than US DRGs, NPPA drug-price ceilings, ICD-10-IN coding, NABH accreditation checks, Aadhaar/DigiLocker identity verification, multilingual document processing, and full data residency inside India under MeitY and IRDAI rules.

**Current status — honest framing.** A US reference platform is operational. The India platform is at **pilot stage**. All India figures in this repository and the accompanying documents are **design targets and projections**, not production results, unless explicitly labelled as live US metrics. See [Status & Targets](#status--targets).

---

## Who it's for

| Stakeholder | Pain point | What FraudIQ India does |
|---|---|---|
| **GIC Re** | Cross-cedant fraud blindness | Portfolio-level fraud intelligence + predictive reserving (Ind-AS 117) |
| **GIPSA (4 PSU insurers)** | Shared hospitals, siloed data | Consortium defence layer + unified blacklist, no raw-data sharing |
| **NHA / PM-JAY** | 50+ crore beneficiaries, ghost billing | AI provider profiling + beneficiary identity verification at scale |
| **Private insurers / TPAs** | Margin compression, manual SIU | Real-time scoring, auto-clear of low-risk claims, leakage reduction |
| **NABH hospitals** | Documentation quality, audit readiness | Clinical cross-match feedback + audit-trail verification |

---

## How it works — seven-stage pipeline

```
Claim / application entered
        │
   1. INGESTION        OCR (multilingual) → parse → de-dup → initial risk score
   2. IDENTITY         Aadhaar eKYC → DigiLocker → liveness → synthetic-ID score
   3. ELIGIBILITY      Plan coverage → prior-auth vs final → cross-payer COB
   4. DOCUMENT         Signature verify → metadata → impossible values → AI-fake detect
   5. CLINICAL         Bill vs notes vs labs → CGHS rate compare → NABH → ICD-10-IN → NPPA
   6. ADJUDICATION     Auto-clear / reduce / deny / SIU refer
   7. REPORTING        IRDAI report → Ind-AS 117 reserve → recovery → provider score
        │
   FIQ Score (0–100) drives the action at every gate
```

Each claim ends with a **FIQ Score (0–100)** and a tiered action:

| Score | Tier | Action | SLA (target) | Evidence package |
|---|---|---|---|---|
| 0–30 | Low | Auto-clear | 4 h | Score only |
| 31–60 | Medium | Reduce (overbilling) | 24 h | Peer comparison, rate diff |
| 61–85 | High | Deny (fraud) | 48 h | Full cross-match + forensics |
| 86–100 | Critical | SIU referral | 7 d | Complete + graph + LE package |

---

## Core capabilities

- **Ensemble ML scoring** — XGBoost + LightGBM + PyTorch, blended, with SHAP explainability on every decision.
- **Graph analytics (Neo4j)** — collusion-ring detection across member–provider–hospital–agent relationships; claim shopping, ghost agenting, billing-spike detection.
- **Document forensics** — custom CNN + OpenCV for tamper and AI-generated-fake detection, metadata and signature analysis.
- **Clinical cross-match** — bill-vs-notes-vs-labs reconciliation against CGHS package rates, NABH status, ICD-10-IN coding integrity, and NPPA ceiling prices.
- **Consortium intelligence** — federated learning + differential privacy so GIPSA members share fraud signals without sharing raw claims or competitive pricing data.
- **Multilingual** — Hindi, Tamil, Telugu, Marathi, Bengali, Gujarati, Kannada, Malayalam + English (IndicBERT + multilingual OCR).
- **Explainable by default** — feature importance, source-document links, peer comparisons, decision rationale for every flag (IRDAI audit + provider appeal).

---

## Compliance & data residency

- **IRDAI** — fraud-reporting dashboards, SIU workflow, automated regulatory submission.
- **Ind-AS 117 / IFRS 17** — explainable AI feeds predictive reserving.
- **MeitY data localization** — all data stored in India (AWS Mumbai `ap-south-1` primary, Hyderabad DR).
- **UIDAI** — offline Aadhaar + eKYC + liveness; targeting KUA certification.
- **IT Act 2000 (SPDI Rules)** — AES-256 at rest, TLS 1.3 in transit, consent management.
- **No data egress outside India** without explicit consent + IRDAI approval.

Target certifications: ISO 27001:2022, SOC 2 Type II, MeitY CSP empanelment, UIDAI KUA.

---

## Repository contents

| Document | Format | Purpose |
|---|---|---|
| `README.md` | Markdown | This file — orientation and quick reference |
| `TECH_STACK.md` | Markdown | Full technology stack, versions, rationale |
| `Architecture_Diagrams.docx` | Word | High-level + layered + consortium + deployment diagrams |
| `White_Paper.docx` | Word | Problem, market, solution, business case |
| `Technical_Architecture_Deep_Dive.docx` | Word | Layer-by-layer engineering reference |
| `Case_Studies.docx` | Word | Worked fraud scenarios and detection walkthroughs |

---

## Status & Targets

| Metric | US reference (live) | India (target, pilot) |
|---|---|---|
| Daily claims processed | 3,832+ | 10,000 (H2 2026 pilot) → 2M (2030) |
| At-risk exposure monitored | $47.2M/day | scaling with cedant onboarding |
| Auto-clear rate | 67% | 60% (conservative for new market) |
| Document forensics accuracy | 98.7% | re-baselining on Indian documents |
| SIU resolution time | 45 days avg | 30 days (target) |

**Three-year India roadmap:** GIC Re pilot (H2 2026) → GIPSA consortium (2027) → top-5 private insurers (H2 2027) → NHA PM-JAY pilot, 2 states (2028) → national rollout (H2 2028) → state health missions (2029) → full ecosystem coverage (2030).

---

## Engagement

**Dr. Tapan Shah, Senior Consultant** — Founder, Chief Architect & India Market Lead
Email: drtapan@hotmail.com · Phone: +91-8595133348
Reference platform: https://prediqa.github.io/FraudIQ_USA/

Preferred engagement models: technical deep-dive (2 h) · pilot proposal (4 weeks) · consortium workshop (1 day) · board presentation (30 min).

---

*FraudIQ India — built for scale, compliance, and Indian regulatory reality. Proven approach in the US, re-architected for India.*
# Fraud_India_PPT
