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

## Recommendation: **Prioritize Passkeys First, Then Risk-Based AI**

### Why Passkeys First?

**1. Directly Solves the Biggest Pain Point: Multi-Screen Complexity & Authentication Failures**

**Current Flow (7-8 steps with frequent failures):**
- Open app → Enter email → Select SSO (3 confusing options) → Redirect to browser → Enter password → Open authenticator app → Enter 6-digit code → Redirect back to app
- **Inigo Insurance**: Authentication loop **fails to return to app** (critical blocker)
- **CitiBank**: "Redundant page" with 3 SSO options causes confusion

**With Passkeys (2 steps, zero failures):**
- Open app → Face ID/Touch ID → Logged in
- **Eliminates**: Email entry, SSO selection, browser redirect, password entry, authenticator app, code entry, redirect failures
- **Result**: Multi-screen complexity completely removed

**2. Eliminates Critical Failure Points**
- **1,990 cases** of mobile SSO redirect failures → **Zero** (no redirects needed with passkeys)
- **Inigo Insurance blocker** (authentication loop fails) → **Solved** (no browser redirects)
- **242 cases** of 2FA/authenticator issues → **Eliminated** (biometric replaces 2FA)
- **2,772 onboarding cases** → **Simplified** (biometric enrollment familiar to users from other apps)

**3. Faster Authentication, Even at Same Frequency**
- **Current**: 5-7 logins/day × 10 minutes each = **50-70 minutes wasted per day**
- **With Passkeys**: 5-7 logins/day × 5 seconds each = **35-49 seconds per day**
- **With Risk-Based AI alone**: 1 login/day × 10 minutes = **10 minutes per day** (still slower than passkeys)
- **Impact**: 98% reduction in time spent authenticating

**4. Immediate Mobile Adoption Impact**
- **CitiBank**: 1-15% adoption due to "multi-step confusion" → Passkeys removes all confusing steps
- **L'Oreal**: External users blocked by MFA complexity → Biometric MFA is familiar and simple
- **Training burden**: No more videos/documentation needed to explain login flow

---

### Why Risk-Based AI Second?

**1. Reduces Frequency After Flow is Fixed**
- Passkeys makes each authentication **fast** (5 seconds)
- Risk-Based AI makes authentication **infrequent** (1x/day vs 7x/day)
- **Combined**: 1 authentication/day × 5 seconds = **5 seconds total vs current 50-70 minutes**

**2. Addresses Remaining Pain Points**
- **Hitachi Energy data**: 231,009 mobile re-authentications in 30 days (excessive frequency)
- **User quote**: "Logging in takes 10 mins or more **every time**"
- Risk-based AI builds trust profiles so users don't re-authenticate from trusted devices/contexts

**3. Handles Edge Cases**
- New device setup (first-time passkey enrollment)
- Device migration scenarios
- Lost device recovery
- High-risk transactions requiring step-up

**4. Creates Complete Solution**
- **Passkeys**: Solves "how" (fast, simple biometric)
- **Risk-Based AI**: Solves "how often" (only when risk detected)
- **Together**: 733K help page visits → projected <100K; users only authenticate meaningfully

---

### Why Push Notifications Last (Limited Scope)?

**Push Notifications Only Solves One Narrow Problem:**
- Replaces **typing 6-digit code** with **tapping "Approve"**
- **Does NOT solve**:
  - Multi-screen complexity (still 7 steps, just step 7 is easier)
  - Browser redirect failures (Inigo Insurance blocker persists)
  - App switching (still switch to notification, just no code entry)
  - Frequency of authentication (still authenticate every time)
  - Onboarding complexity (still need SSO setup, now + push notification setup)

**When Push Notifications IS Valuable:**
- As **step-up authentication** after Passkeys + Risk-Based AI are deployed
- When risk is detected and user needs to approve: "Unusual login from new location - tap to approve"
- Complements Risk-Based AI for medium-risk scenarios (low risk = no prompt, high risk = full re-auth, medium risk = push approval)

**Why NOT as primary solution:**
- **CitiBank quote**: "If we could just make the **number of screens** lesser" → Push doesn't reduce screens
- **733K help page visits** → Users stuck in multi-step flow, not struggling with code entry specifically
- **Inigo Insurance**: Redirect failures → Push doesn't eliminate redirects

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
| **1** | Q3-Q4 2026 | **Passkeys** | Eliminate 7-step login flow → 2 steps; remove browser redirect failures; 98% reduction in authentication time |
| **2** | Q1-Q2 2027 | **Risk-Based AI Step-Up** | Reduce authentication frequency from 5-7x/day to 1x/day in trusted contexts; builds on passkey trust model |
| **3** | Q3 2027 | **Push Notifications** | Step-up authentication for medium-risk scenarios detected by Risk-Based AI; completes adaptive security model |

---

## Success Metrics (6 Months Post-Launch)

| Metric | Baseline (Q1 2025) | Target (Post-Passkeys) | Target (Post-Risk AI) |
|--------|-------------------|----------------------|---------------------|
| "Need help signing in" page visits | 733,744 (Feb-Apr 2026) | <150,000/quarter (-80%) | <100,000/quarter (-86%) |
| Login support cases | >11,000/quarter | <3,000/quarter (-73%) | <2,000/quarter (-82%) |
| Authentication time per day | 50-70 minutes | 35-49 seconds (-98%) | 5 seconds (-99.9%) |
| Mobile app adoption (enterprise) | 1-15% | 40%+ | 60%+ |
| Mobile SSO redirect failures | 1,990 cases/quarter | 0 (no redirects) | 0 (no redirects) |
| Password reset requests | TBD | -100% (no passwords) | -100% (no passwords) |

---

## Risk Mitigation

**Passkeys (Phase 1):**
- **Device compatibility**: Start with iOS/Android native support; web fallback for older devices
- **Lost device**: Implement cloud-synced passkeys (iCloud Keychain, Google Password Manager) + account recovery flow
- **Enterprise MDM**: Partner with Inigo Insurance type customers to test corporate device policies early
- **Migration**: Phased rollout - offer passkeys to new users first, then opt-in for existing users

**Risk-Based AI (Phase 2):**
- **AI false positives**: Conservative thresholds; user feedback loop; manual override
- **Compliance (GDPR, SOC2)**: Auditable risk decisions; transparent to users; opt-out for high-security accounts
- **Trust model**: Builds on passkey device trust; AI layers context on top of proven credential

**Push Notifications (Phase 3):**
- **Notification delivery**: Test across iOS/Android; handle notification permission denials
- **User confusion**: Clear messaging "Approve login from [device]" with context

---

## Next Steps

**Phase 1: Passkeys (Start Immediately)**
1. **Engineering feasibility review** for passkey implementation (Week of May 6, 2026)
2. **Platform selection**: Evaluate native platform authenticators (iOS/Android) vs cross-platform solutions
3. **Define pilot group**: 500 new mobile users + 200 existing power users (opt-in)
4. **Partner with enterprise customers**: Inigo Insurance (test MDM compatibility), CitiBank (high volume validation)
5. **Design enrollment flow**: Minimize steps, leverage existing Face ID/Touch ID familiarity
6. **Build account recovery**: Cloud-synced passkeys + fallback mechanisms

**Phase 2: Risk-Based AI (Post-Passkeys Launch)**
1. Establish risk factors: Device fingerprint, geolocation, time-of-day patterns, passkey usage history
2. Build trust profiles for users with established passkey patterns
3. Define step-up triggers: New device, unusual location, high-value transaction

**Success Criteria for Phase 1 (Passkeys):**
- <3 steps to complete authentication
- Zero authentication redirect failures
- 80%+ pilot user satisfaction
- 50%+ mobile adoption increase in pilot group

---

**Conclusion**: **Passkeys should be prioritized first** because it directly eliminates the multi-screen complexity and authentication redirect failures that drive 733K help page visits and block mobile adoption (1-15% at enterprise customers). Risk-Based AI follows to reduce authentication frequency once the flow is fixed. Push Notifications serves as step-up authentication for medium-risk scenarios. Combined, these features reduce daily authentication time from 50-70 minutes to 5 seconds while maintaining security.

**Key Data Points Supporting Passkeys First:**
- **1,990 mobile SSO redirect failure cases** → Passkeys eliminates redirects entirely
- **7-8 step flow reduced to 2 steps** → Directly addresses CitiBank "number of screens" feedback
- **Inigo Insurance critical blocker** (authentication loop fails) → Solved with no browser redirects
- **98% reduction in authentication time per day** (50-70 min → 35-49 sec) even before frequency reduction

---

**Contact**: Smrithi Jayarajan | **Data Sources**: 
- Topic Modeling Analysis by Weikun Hu (weikun.hu@sap.com)
- Customer Interviews: CitiBank, Inigo Insurance, L'Oreal, Hitachi Energy, Sekisui House
- Support Data: Q1-Q4 2024, Q1 2025, "Need help signing in" page analytics (Feb-Apr 2026)