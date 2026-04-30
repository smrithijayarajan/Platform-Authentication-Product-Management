# Customer Interview Analysis - Top 5 Pain Points

**Data Sources Analyzed:**
- CitiBank - Discovery Interview (June 25, 2025)
- Inigo Insurance - Discovery Interview & AI Meeting Notes (July 2025)
- L'Oreal - AI Meeting Notes
- Hitachi Energy - Interview Prep & Login Data
- Sekisui House - Customer Responses

---

## Top 5 Pain Points from Customer Interviews

### 1. **Mobile App Sign-In Complexity & Multiple Steps**
**Affected Customers: CitiBank, Inigo Insurance**

**CitiBank Feedback:**
- Users must enter email address on first screen
- Then select from 3 confusing SSO options ("mobile SSO", "GBT portal", "Salesforce Prod 2", "sapcon password") - **redundant page**
- Quote: "For all CD users, it's just a mobile SSO. So this is basically a redundant page for us."
- Users don't understand which option to select
- "Not many are aware that they have to input their email address at the first page. There's no easy prompt there."
- **Impact**: This multi-step confusion hinders mobile app adoption (only 1-15% adoption at CitiBank)

**Inigo Insurance Feedback:**
- Mobile app directs users to Edge for SSO/MFA but **often fails to complete the authentication loop**
- Error when returning to the app after Azure SSO
- Some users see the Azure/SSO button, others don't
- **Root cause**: Conditional access/app protection policies interfering with in-app browser or authentication redirect

**Why This Is #1**: Blocks users at the entry point; creates immediate friction; directly cited as barrier to mobile adoption

---

### 2. **Mobile App Low Adoption Due to Login Barriers**
**Affected Customers: CitiBank, L'Oreal**

**CitiBank:**
- Only **1% of users use mobile app** (initially reported), though analytics show 15%
- Primary reason: Historical login pain + lack of features (now improving)
- Requires training videos/documentation just to explain how to log in
- Quote: "Onboarding takes about a day because the user tries it, doesn't understand how to do it, raises a query, service desk shares guide"
- Manoj (CitiBank): "If I have to give feedback, I might say that you can make it a bit more customized. For example, we know that for city we use **only SSO**. So those additional options that we show up once we know that it's a city customer, if we don't show those, it would be better. It reduces confusion."

**L'Oreal:**
- **External users (beauty advisors) cannot access Concur mobile** due to MFA requirement
- They don't have company devices and won't use personal devices for enterprise apps
- L'Oreal had to hire **temporary workers** to process expenses on behalf of external users
- Quote: "External users, like beauty advisors, face challenges accessing Concur due to the MFA requirement. These users often do not have company-provided devices and are reluctant to use personal devices for enterprise applications."

**Why This Is #2**: Sign-in complexity directly suppresses feature adoption; creates workarounds; generates support burden

---

### 3. **MFA/Authentication Loop Failures on Mobile**
**Affected Customers: Inigo Insurance, CitiBank**

**Inigo Insurance (Major Issue):**
- **Authentication redirect fails** - app sends user to Edge for SSO/MFA, but doesn't complete the loop back to the app
- Errors when returning from Azure SSO
- Suspected causes:
  - Conditional access policies blocking redirect
  - App protection/lockdown settings interfering with in-app browser
  - Edge browser restrictions on managed devices
  - New corporate device policy (recently rolled out) may be breaking it
- Quote from meeting notes: "The Concur mobile app directs users to Edge for SSO/MFA but often fails to complete the authentication loop (error when returning to the app). Some users see the Azure/SSO button, others do not."

**CitiBank:**
- MFA process works but adds friction
- Users must authenticate with Microsoft Authenticator on every mobile login (not seamless like web)
- Quote: "The mobile app also is for SSO. The only difference is in mobile app it's not the automated because it's not within the city network, so it has to do the username password entry."

**Device Management Context (Inigo Insurance):**
- Company size ~250 employees; ~150 corporate devices
- Intune shows 137 devices have Concur app installed
- New corporate mobile device policy rolled out to new/replacement devices
- Older devices still on old policy - **the new policy may be the source of the problem**
- BYOD allowed but Intune MDM not pushed to BYOD

**Why This Is #3**: Complete authentication failure = no access; affects managed devices; requires IT investigation/support tickets

---

### 4. **Lack of Persistent Sessions / Forced Re-Authentication**
**Affected Customers: CitiBank, L'Oreal**

**CitiBank:**
- Web has seamless automated SSO (dsso) - users just click link, auto-authenticated within network
- **Mobile requires username + password entry every time** (not automated like web)
- Users accustomed to web's ease find mobile cumbersome
- Quote: "The web application is available only within city network and it's an automated authentication... All they have to do is click on a link and it basically lands them in the homepage."
- Quote: "With respect to the web, we don't have an issue as such. It's just the way users are used to."

**L'Oreal:**
- Users typically don't need to enter credentials if Face ID is authorized
- **But**: Process still requires entering UPN → redirect to L'Oreal IT page → authenticate → redirect back
- If not on VPN, must use Microsoft Authenticator
- Quote from meeting notes: "The login process on the Concur mobile application is smooth, with users typically not needing to enter credentials if face ID login functionality is authorized. The process involves entering the UPN, being redirected to a L'Oreal IT page for authentication, and then gaining access to the Concur application."

**Hitachi Energy Data:**
- Last 30 days: 116,311 web logins (98.9% SSO SAML)
- **Mobile re-authentication: 231,009 records** - showing high frequency of re-auth on mobile
- 50.9% of records are "mobi" type re-authentications

**Why This Is #4**: Creates unnecessary friction for repeat logins; makes mobile feel inferior to web experience; users avoid mobile as a result

---

### 5. **Inconsistent Sign-In Options & Configuration Confusion**
**Affected Customers: CitiBank, Inigo Insurance**

**CitiBank:**
- Quote: "If I have to give feedback, I might say that you can make it a bit more customized. For example, we know that for city we use **only SSO**. So those additional options that we show up once we know that it's a city customer, if we don't show those, it would be better. It reduces confusion."
- Showing 3 SSO options when only 1 is valid confuses users
- After entering email, users see: "Give me 3 buttons saying sign in with and says mobile SSO, GBT portal, Salesforce Prod 2 and then sapcon password."
- Quote: "So this is basically a redundant page... When those additional buttons it, it can cause a bit of a confusion. What should I click so ends up being... that kind of hinders the adoption rate."

**Inigo Insurance:**
- **User entry errors** (incorrect username formatting) can hide the SSO option entirely
- Inconsistent experience: some users see Azure/SSO button, others don't
- Depends on device policy (old vs. new corporate policy)
- Quote from notes: "User entry errors (incorrect username formatting) can hide SSO option."

**Why This Is #5**: Company-specific auth setup doesn't adapt to user; shows irrelevant options; creates unnecessary decision points

---

## Additional Insights from Customer Interviews

### **CitiBank - Enterprise Scale Context**
- **Deployment**: SAP Concur in 90 of 95 countries where Citi operates
- **Team Structure**: Global team manages expense administration; regional teams for travel
- **Device Policy**: Primarily BYOD (Bring Your Own Device)
- **SSO Setup**: Automated SSO (dsso) within network - seamless web experience
- **User Base**: Many senior travelers with executive assistants who handle expense reports
- **Delegate Usage**: Assistants scan receipts in bulk → upload to web (delegates on mobile only recently added)

### **L'Oreal - Mobile Usage Patterns**
- **Primary Mobile Use Cases**:
  - Expense management: photo receipts (recognized as legal documents)
  - Approval process via mobile
  - **Hybrid workflow**: Create expense reports on mobile during trips → finalize on computer in office
- **Smooth Login Experience**: Face ID works well for employees with corporate devices
- **MFA Process**: Microsoft Authenticator consistent across all L'Oreal apps
- **Future Needs**:
  - Push notifications for updates
  - Better in-app documentation
  - Microsoft Teams integration for approvals

### **Inigo Insurance - Technical Issues**
- **Authentication Stack**: SSO via Azure (SAML), MFA enforced
- **Device Management**: Intune MDM for corporate devices
- **Usage Metrics**: 137 devices with Concur app installed; ~26 users signed in (June)
- **Action Items from Meeting**:
  - Log support ticket for authentication redirect investigation
  - Test login flows on old vs. new device policy to isolate the issue
  - Review conditional access & app protection settings

### **Hitachi Energy - Login Data (Last 30 Days)**
- **Web Login Stats**:
  - Total: 116,311 logins
  - SSO SAML: 98.9% (115,032)
  - Password: 0.7% (814)
  - Email link: 0.4% (465)
- **Mobile Re-Authentication**:
  - Total: 231,009 records
  - "mobi" type: 50.9% (117,584)
- **Configuration**: MFA required, email link login enabled, session timeout 120 minutes

---

## Summary: Customer Pain Point Patterns

| Pain Point | Impact | Frequency Across Customers | Severity |
|------------|--------|----------------------------|----------|
| **Multi-step mobile login** | Adoption barrier, confusion, support burden | 2/5 customers (CitiBank, Inigo) | High |
| **Low mobile adoption** | Feature underutilization, workarounds | 2/5 customers (CitiBank, L'Oreal) | High |
| **MFA/redirect failures** | Complete access failure, IT escalation | 2/5 customers (Inigo major, CitiBank minor) | Critical |
| **Forced re-authentication** | Daily friction, mobile avoidance | 3/5 customers (CitiBank, L'Oreal, Hitachi) | Medium-High |
| **Irrelevant auth options** | Confusion, cognitive load | 2/5 customers (CitiBank, Inigo) | Medium |

---

## Key Quotes from Customers

### CitiBank (Manoj S.)
> "For all CD users, it's just a mobile SSO. So this is basically a redundant page for us... When those additional buttons, it can cause a bit of a confusion. What should I click so ends up being... that kind of hinders the adoption rate."

> "With respect to the web, we don't have an issue as such. It's just the way users are used to... All they have to do is click on a link and it basically lands them in the homepage."

> "Onboarding takes about a day because the user tries it, doesn't understand how to do it, raises a query, service desk shares guide."

> "If we could just [make] the number of screens lesser then it would be better."

### L'Oreal (BAUDEQUIN)
> "External users, like beauty advisors, face challenges accessing Concur due to the MFA requirement. These users often do not have company-provided devices and are reluctant to use personal devices for enterprise applications."

> "The login process on the Concur mobile application is smooth, with users typically not needing to enter credentials if face ID login functionality is authorized."

### Inigo Insurance (Ken Coleman, Kieran Shah, Ajay Bagdia)
> "The Concur mobile app directs users to Edge for SSO/MFA but often fails to complete the authentication loop (error when returning to the app)."

> "New corporate mobile device policy was rolled out to new/replacement devices. Older devices still on the old policy. The new policy may be the source of the problem."

---

## Customer Needs Summary

**What Customers Want:**
1. **Fewer login steps on mobile** - eliminate redundant screens
2. **Company-specific configuration** - hide irrelevant SSO options
3. **Reliable authentication redirects** - complete the SSO/MFA loop successfully
4. **Persistent sessions** - reduce frequency of re-authentication
5. **Better onboarding** - reduce need for training videos/documentation
6. **Cross-platform consistency** - mobile should be as easy as web

**Key Insight**: Mobile sign-in is the primary barrier to mobile app adoption for large enterprises. Web experience is seamless (automated SSO within network), while mobile requires multiple manual steps, causing users to avoid the mobile app entirely.
