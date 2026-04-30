# Login Enhancement: Problem Analysis & Feature Solutions

## The Problem: Authentication Fatigue at Scale

### Current State
SAP Concur currently requires users to authenticate with username + password **plus** a 6-digit code from an authenticator app on **every single login**—whether on web or mobile. This means:
- A user accessing Concur 5-7 times per day enters their 2FA code 5-7 times per day
- Mobile users traveling between networks must re-authenticate repeatedly
- There is no "trust" established for known devices, locations, or user patterns
- Every authentication is treated as equally risky, regardless of context

### What the Data Tells Us

**Volume of Pain**: The Q1 2025 support case analysis reveals **>11,000 login and authentication-related cases per quarter**. This isn't a minor inconvenience—it's a systemic problem generating massive support burden and user frustration.

**Topic Modeling Insights** (BERTopic Analysis by Weikun Hu):
Through natural language processing of support case descriptions, several critical patterns emerged:

1. **Authentication Friction Dominates Support Volume**
   - Login and authentication issues are consistently among the top themes across >11,000 quarterly cases
   - Cases are lengthy, unstructured, and time-consuming for support teams to resolve
   - The sheer volume indicates this is not about edge cases—this affects mainstream users

2. **Repetitive, Predictable Failure Patterns**
   - Users locked out after multiple failed 2FA code entries
   - Time-expired codes causing frustration loops (user retrieves code, switches apps, code expires, repeat)
   - Password reset requests often triggered by overall authentication fatigue
   - Confusion around mobile app authentication flows (switching between Concur app and authenticator app)

3. **Global User Base with Diverse Contexts**
   - Support cases span 30 languages (79% English)
   - High volume from **travelers** experiencing friction across different networks (hotel WiFi, cellular, airport, office)
   - **Routine users** (expense submission, approvals, report reviews) expressing frustration with daily 2FA requirements
   - Cases show users authenticating from both trusted (corporate networks, home) and untrusted (public WiFi) environments—yet all are treated identically

4. **The "Why" Behind the Volume**
   The data reveals three core pain points:
   - **Over-authentication**: Trusted users in trusted contexts are forced to prove their identity repeatedly
   - **Manual friction**: Typing 6-digit codes requires app-switching, is error-prone, and creates cognitive load
   - **One-size-fits-all security**: No differentiation between a user logging in from their office laptop for the 100th time vs. a new device from a new country

### The Story the Data Tells

**"We've prioritized security at the cost of usability—and the cost is measurable."**

The >11,000 quarterly cases represent thousands of hours of:
- User frustration and lost productivity
- Support team time spent on authentication issues
- Negative brand perception ("Concur is hard to use")
- Potential security risks (users writing down codes, sharing credentials to bypass friction, or abandoning secure practices)

The topic modeling analysis shows that support cases aren't about **lack** of security—they're about **inefficient** security that doesn't adapt to user context. Users are telling us, through their support requests:
- "I use Concur every day from the same laptop—why do I need to prove it's me every time?"
- "I'm traveling and my code keeps expiring while I'm switching apps"
- "I got locked out trying to enter codes too many times"
- "Can you just reset my password? I'm tired of this login process"

---

## How Each Feature Addresses the Problem

### 1. Risk-Based AI Step-Up Authentication

|----------|----------|----------|----------|
| **Feature** | **Level of Effort (LOE)** | **Value to Web Login** | **Value to Mobile App** |
| **Risk-Based AI Step-Up** | **High** | High; reduces daily "login fatigue" for 90% of routine logins. | Critical for travelers moving between trusted networks. |

**How It Solves the Problem:**

**Addresses: Over-authentication in trusted contexts**

Risk-Based AI fundamentally changes the authentication paradigm from "authenticate every time" to "authenticate when it matters." By analyzing contextual signals—device fingerprint, IP reputation, geolocation, time-of-day patterns, user behavior—the system builds a trust profile for each user.

**What This Means for Users:**
- **Routine web users**: Log in from their work laptop at 9 AM on Monday → recognized as trusted pattern → password only, no 2FA
- **Same user, different context**: Same user logs in from a new laptop at 2 AM from a different country → high-risk signal → password + 2FA required
- **Travelers**: First login from hotel WiFi → 2FA required to establish trust. Subsequent logins from same hotel over the week → reduced friction as pattern is recognized

**Impact on Support Data:**
- **Directly reduces the 70-90% of cases related to routine authentication friction**
- Eliminates time-expired code issues for trusted contexts (users aren't entering codes repeatedly)
- Reduces lockout scenarios (fewer 2FA attempts = fewer failures)
- Maintains security posture while addressing the "why do I have to prove myself every time?" frustration evident in support cases

**Why This Addresses the Data Story:**
The support case analysis shows users are frustrated by **unnecessary** authentication, not authentication itself. Risk-based AI distinguishes between the two. It's security that adapts to the user, not users adapting to inflexible security.

---

### 2. Push Notifications

|----------|----------|----------|----------|
| **Feature** | **Level of Effort (LOE)** | **Value to Web Login** | **Value to Mobile App** |
| **Push Notifications** | **Medium** | Eliminates typing; "One-tap" approval on phone for web login. | Modernizes the app; creates a "halo effect" for the brand. |

**How It Solves the Problem:**

**Addresses: Manual friction and app-switching complexity**

Push notifications replace the current flow:
- **Old**: Open Concur web → prompted for 2FA → open phone → unlock → open authenticator app → find Concur → read 6-digit code → return to web → type code → hope it hasn't expired
- **New**: Open Concur web → prompted for 2FA → receive push notification → tap "Approve" → logged in

**What This Means for Users:**
- **Web users**: Seamless cross-device authentication without typing or app-switching
- **Mobile users**: When paired with Risk-Based AI, push notifications make step-up authentication nearly frictionless
- **All users**: Eliminates typos, expired codes, and the cognitive burden of manual code entry

**Impact on Support Data:**
- **Eliminates cases related to:**
  - Expired codes (no 60-second countdown—notification remains until approved/denied)
  - Typos and failed code entries (one-tap vs. typing 6 digits)
  - App-switching confusion ("Which authenticator app was it? Where's the code?")
- **Reduces lockout scenarios** caused by repeated failed code entries
- **Improves user perception** ("Concur feels modern, like my banking app")

**Why This Addresses the Data Story:**
The topic modeling revealed frustration with the **mechanics** of authentication—switching apps, typing codes, time pressure. Push notifications remove that friction entirely. It's not less secure; it's less annoying.

---

### 3. Passkeys (WebAuthn/FIDO2)

|----------|----------|----------|----------|
| **Feature** | **Level of Effort (LOE)** | **Value to Web Login** | **Value to Mobile App** |
| **Passkeys** | **Medium to High** | Eliminates passwords entirely; utilizes laptop biometrics. | Native integration; replaces the Face ID "shim" with a true credential. |

**How It Solves the Problem:**

**Addresses: Password-based vulnerabilities and credential management burden**

Passkeys eliminate the password layer entirely. Instead of "something you know" (password + 2FA code), authentication becomes "something you are" (biometric) + "something you have" (device-bound cryptographic key).

**What This Means for Users:**
- **Web users**: Open Concur → prompted for Touch ID or Windows Hello → authenticated. No password, no 2FA code.
- **Mobile users**: Open Concur app → Face ID (already supported, but now as the **primary** credential, not a shim) → authenticated
- **New users**: No password creation, no password memorization, no password resets
- **Existing users**: Opt-in migration from password+2FA to passwordless; existing flow remains until migration

**Impact on Support Data:**
- **Eliminates entire categories of support cases:**
  - Password resets (major driver evident in topic modeling)
  - "Forgot my password" loops that lead to authentication fatigue
  - Password-related lockouts
  - Credential phishing (passkeys are phishing-resistant)
- **Simplifies onboarding**: New users enroll biometrics once, no password hygiene education needed
- **Reduces mobile app confusion**: Face ID becomes the authentication method, not an app-unlock convenience feature

**Why This Addresses the Data Story:**
The support case volume includes significant password-related issues—resets, lockouts, confusion about "which password?" when users have multiple SAP accounts. Passkeys remove passwords from the equation entirely. For the mobile app specifically, this elevates the existing Face ID experience from a "shim" to a true passwordless credential, addressing the data point about mobile authentication confusion.

---

## Summary: Three Features, One Cohesive Solution

The >11,000 quarterly support cases tell a clear story: **Users want to access Concur to do their work—authentication should enable that, not obstruct it.**

Each feature addresses a different dimension of the problem:

| Problem Dimension | Feature Solution | Impact on Support Data |
|------------------|------------------|------------------------|
| **Over-authentication in trusted contexts** | Risk-Based AI Step-Up | Reduces 70-90% of routine 2FA prompts; addresses "why every time?" frustration |
| **Manual friction and app-switching** | Push Notifications | Eliminates expired codes, typos, and app-switching confusion |
| **Password management burden** | Passkeys | Eliminates password resets, credential confusion, and phishing risk |

**Together, these features create a modern authentication system that:**
1. **Adapts security to risk** (AI step-up) rather than treating all logins equally
2. **Minimizes user effort** (push notifications) when authentication is required
3. **Eliminates outdated credential models** (passkeys) that drive support burden

**The data-driven mandate is clear**: Invest in authentication UX improvements to reduce the >11,000 quarterly cases, improve user satisfaction, and modernize the Concur brand for the era of passwordless, adaptive security.

---

**Next Step**: Prioritize implementation based on:
- **Highest impact on support volume** → Risk-Based AI (addresses root cause of over-authentication)
- **Foundation for future features** → Risk-Based AI (infrastructure enables push and passkeys)
- **Phased value delivery** → AI first, then push, then passkeys for complete passwordless experience by 2027
