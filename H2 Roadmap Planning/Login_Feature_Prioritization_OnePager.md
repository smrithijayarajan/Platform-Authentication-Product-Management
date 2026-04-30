# Login Enhancement Feature Prioritization
**Data-Driven Recommendation for Engineering | April 30, 2026**

---

## Problem Statement
Concur requires username + password with 2FA (6-digit authenticator code) on **every login**. This creates "login fatigue" and massive user friction:
- **733,744 visits** to "Need help signing in" page (Feb 1 - Apr 29, 2026)
- **>11,000 login/authentication support cases per quarter** (Q1 2025)
- **100% of sampled mobile app negative reviews** cite login difficulties
- **Enterprise customers** report only 1-15% mobile app adoption due to login barriers

---

## Feature Comparison

| Feature | LOE | Problem Solved | Value to Web Login | Value to Mobile App |
|---------|-----|----------------|-------------------|---------------------|
| **Risk-Based AI Step-Up** | High | Eliminates repetitive 2FA for trusted contexts | **High**: Reduces 2FA prompts by ~90% for routine logins; prompts only for anomalies | **Critical**: Adaptive auth for travelers; maintains security across network changes |
| **Push Notifications** | Medium | Replaces typing 6-digit codes | **High**: One-tap approval on mobile; eliminates app-switching | **High**: Modernizes UX; creates brand "halo effect" |
| **Passkeys** | Med-High | Eliminates passwords entirely | **High**: Passwordless via laptop biometrics (Touch ID/Windows Hello) | **Critical**: Native credential integration; replaces Face ID "shim" with true passwordless |

---

## Top 5 Pain Points - What the Data Shows

1. **Login Difficulties & Authentication Complexity** - 733K+ help page visits, 4K+ support cases; affects all users daily
2. **2FA/Authenticator App Friction** - QR code failures, expired codes during app switching, "had to call 100 times to reset"
3. **Password Reset Issues** - Cannot self-serve, require IT escalation, circular dependencies (need 2FA to reset password)
4. **Mobile Session Management Failures** - Forced re-auth every time, SSO redirect failures on managed devices (Inigo Insurance: critical blocker)
5. **Initial Onboarding Complexity** - 2,772 cases blocked at profile creation, new employees need IT support just to log in first time

---

## Recommendation: **Prioritize Risk-Based AI Step-Up**

### Why This Feature First?

**1. Highest Impact on Support Volume & User Pain**
- Addresses root cause: excessive authentication friction for routine logins
- Projected 50%+ reduction in quarterly support cases (from >11K to <5.5K)
- Reduces help page visits (currently 733K over 3 months)
- Eliminates daily 2FA fatigue affecting 90% of routine logins
- **CitiBank feedback**: "If we could just make the number of screens lesser then it would be better"
- **Customer quote**: "Onboarding takes about a day because user tries it, doesn't understand, raises query"

**2. Foundation for Future Features**
- Risk engine infrastructure enables Push Notifications and Passkeys
- AI context (device trust, location, behavior) informs when to step-up
- Creates intelligent fallback strategies

**3. Immediate Value to Largest User Segment**
- **Existing users** (~90%): Instant relief from daily 2FA fatigue
- **Travelers** (high support volume): Adaptive auth based on network trust; addresses mobile SSO failures
- **Routine users**: Frictionless expense submission and approvals
- **Enterprise customers**: Reduces training burden and eliminates multi-step mobile login confusion
- **Mobile adoption**: Removes primary barrier cited by CitiBank (1-15% adoption) and L'Oreal (external users blocked)

**4. Security-First Approach**
- Maintains 2FA for genuinely risky scenarios (new devices, unusual locations)
- ML-driven anomaly detection with full audit trail
- Does NOT reduce security; shifts authentication to risk-appropriate moments

---

## Data Insights from Support Cases & Customer Interviews

**Quantitative Evidence (Q1 2025 Support Data & BERTopic Analysis):**
- **733,744 visits** to "Need help signing in" page (Feb 1 - Apr 29, 2026)
- **6,343+ cases** directly about login/authentication issues
- **2,772 cases** about onboarding/profile creation (largest single topic)
- **1,990 cases** specifically about mobile SSO failures
- **242 cases** about 2FA/authenticator problems
- **30 languages, 79% English** → solution must work globally

**Qualitative Evidence (Mobile App Reviews):**
- "Logging in takes 10 mins or more every time"
- "Easier to access area 51 than log on to this"
- "I get a headache weeks before I know I'll have to submit an expense"
- "Had to email and call like 100 times to reset [authenticator]"
- "This app has taken me weeks just to be able to log in"

**Enterprise Customer Pain Points (CitiBank, Inigo Insurance, L'Oreal):**
1. **Multi-step mobile login** - Users must enter email, then select from 3 confusing SSO options (CitiBank: "redundant page")
2. **Authentication loop failures** - Mobile redirects to Edge/browser for SSO but fails to return to app (Inigo Insurance: critical blocker)
3. **Low mobile adoption** - Only 1-15% use mobile app due to login complexity (CitiBank); requires training videos just to explain login
4. **Forced re-authentication** - Mobile requires credentials every time vs. web's seamless automated SSO (CitiBank)
5. **External user barriers** - L'Oreal had to hire temporary workers to process expenses because external users can't access mobile with MFA

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
| "Need help signing in" page visits | 733,744 (Feb-Apr 2026) | <350,000/quarter (-50%) |
| Login support cases | >11,000/quarter | <5,500/quarter (-50%) |
| Daily 2FA prompts/user | ~5-7 | <1 (trusted contexts) |
| Mobile app adoption (enterprise) | 1-15% | 40%+ |
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

**Conclusion**: Risk-Based AI Step-Up delivers the highest ROI by addressing the core pain point (733K help page visits, >11K quarterly cases, and enterprise mobile adoption barriers), creating foundation infrastructure, and balancing security with user experience. Customer interviews confirm login complexity as the #1 barrier to mobile adoption. Phased approach ensures iterative value delivery toward passwordless authentication by 2027.

---

**Contact**: Smrithi Jayarajan | **Data Sources**: 
- Topic Modeling Analysis by Weikun Hu (weikun.hu@sap.com)
- Customer Interviews: CitiBank, Inigo Insurance, L'Oreal, Hitachi Energy, Sekisui House
- Support Data: Q1-Q4 2024, Q1 2025, "Need help signing in" page analytics (Feb-Apr 2026)