# Login Enhancement Feature Prioritization
**Data-Driven Recommendation for Engineering | April 30, 2026**

---

## Problem Statement
Concur requires username + password with 2FA (6-digit authenticator code) on **every login**. This creates "login fatigue" and drives **>11,000 login/authentication support cases per quarter** (Q1 2025 data).

---

## Feature Comparison

| Feature | LOE | Problem Solved | Value to Web Login | Value to Mobile App |
|---------|-----|----------------|-------------------|---------------------|
| **Risk-Based AI Step-Up** | High | Eliminates repetitive 2FA for trusted contexts | **High**: Reduces 2FA prompts by ~90% for routine logins; prompts only for anomalies | **Critical**: Adaptive auth for travelers; maintains security across network changes |
| **Push Notifications** | Medium | Replaces typing 6-digit codes | **High**: One-tap approval on mobile; eliminates app-switching | **High**: Modernizes UX; creates brand "halo effect" |
| **Passkeys** | Med-High | Eliminates passwords entirely | **High**: Passwordless via laptop biometrics (Touch ID/Windows Hello) | **Critical**: Native credential integration; replaces Face ID "shim" with true passwordless |

---

## Recommendation: **Prioritize Risk-Based AI Step-Up**

### Why This Feature First?

**1. Highest Impact on Support Volume**
- Addresses root cause: excessive authentication friction for routine logins
- Projected 50%+ reduction in quarterly support cases (from >11K to <5.5K)
- Reduces 2FA prompts by 70-90% for established users in trusted contexts

**2. Foundation for Future Features**
- Risk engine infrastructure enables Push Notifications and Passkeys
- AI context (device trust, location, behavior) informs when to step-up
- Creates intelligent fallback strategies

**3. Immediate Value to Largest User Segment**
- **Existing users** (~90%): Instant relief from daily 2FA fatigue
- **Travelers** (high support volume): Adaptive auth based on network trust
- **Routine users**: Frictionless expense submission and approvals

**4. Security-First Approach**
- Maintains 2FA for genuinely risky scenarios (new devices, unusual locations)
- ML-driven anomaly detection with full audit trail
- Does NOT reduce security; shifts authentication to risk-appropriate moments

---

## Data Insights from Q1 2025 Support Cases (BERTopic Analysis)

**Key Findings:**
- **>11,000 cases/quarter** indicate significant login friction pain
- **30 languages, 79% English** → solution must work globally
- **Top patterns:** Users locked out after 2FA failures, expired codes, password resets, mobile app confusion
- **User contexts:** High volume from travelers (untrusted networks) and routine users (daily 2FA frustration)

---

## Implementation Roadmap

| Phase | Timeline | Feature | Expected Outcome |
|-------|----------|---------|------------------|
| **1** | Q3-Q4 2026 | Risk-Based AI Step-Up | 70-90% reduction in 2FA prompts; 50%+ drop in support cases |
| **2** | Q1 2027 | Push Notifications | One-tap approval for step-up; modernized UX |
| **3** | Q2-Q3 2027 | Passkeys | True passwordless experience; eliminate password resets |

---

## Success Metrics (6 Months Post-Launch)

| Metric | Baseline (Q1 2025) | Target |
|--------|-------------------|--------|
| Login support cases | >11,000/quarter | <5,500/quarter (-50%) |
| Daily 2FA prompts/user | ~5-7 | <1 (trusted contexts) |
| User satisfaction | TBD | 80%+ |
| Password reset requests | TBD | -60% (Phase 3) |

---

## Risk Mitigation

- **AI false positives**: Conservative thresholds; user feedback loop; manual override
- **Compliance (GDPR, SOC2)**: Auditable risk decisions; transparent to users; opt-out for high-security accounts
- **Implementation complexity**: Leverage ML infrastructure; partner with proven vendors (Okta, Auth0); phased pilot rollout

---

## Next Steps

1. **Engineering feasibility review** for Risk-Based AI (Week of May 6, 2026)
2. **Define pilot group**: 500-1K frequent web users + 500 mobile travelers
3. **Establish risk factors**: Device fingerprint, IP reputation, geolocation, time-of-day, user behavior
4. **Create monitoring dashboard** for success metrics

---

**Conclusion**: Risk-Based AI Step-Up delivers the highest ROI by addressing the core pain point (>11K quarterly cases), creating foundation infrastructure, and balancing security with user experience. Phased approach ensures iterative value delivery toward passwordless authentication by 2027.

---

**Contact**: [Your Name] | **Data Source**: Topic Modeling Analysis by Weikun Hu (weikun.hu@sap.com)