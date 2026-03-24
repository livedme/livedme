
# 🚀 .NET 10 + Blazor Server Migration Estimate

## 📌 Assumptions

* Full feature parity required
* Migrate to **.NET 10** and convert web UI to **Blazor Server**
* EF6 → EF Core migration required
* Third-party libraries must support .NET 10 or be replaced
* Hourly rate: **$15/hr** (adjustable)

---

# 📦 Per-Module Effort, Risk & Cost

## 1. `*.cshtml` (UI + All Areas)

**Areas:** Core, AssetManagement, Sales, EventManagement, ProductManagement, Config, Helpdesk,  Reporting

**Work:**

* Migrate OWIN/Auth → ASP.NET Core Identity
* Convert MVC/Razor → Blazor Server components
* Port routes & areas
* Migrate SignalR → ASP.NET Core SignalR
* Update JS integrations
* Rework auth flows (cookies, 2FA)
* Convert `web.config` → `appsettings.json`

**Complexity:** 🔴 Very High
**Time:** 700 – 800 hours
**Risks:**

* Full UI rewrite (views → components)
* SignalR client compatibility
* Third-party UI library support

---

## 2. `Flibble.CRM.Core.csproj`

**Work:**

* Retarget to .NET 10
* Fix API/compatibility issues
* Remove System.Web dependencies
* Integrate DI & logging

**Complexity:** 🟡 Medium
**Time:** 140 – 180 hours
**Risks:**

* Hidden System.Web dependencies

---

## 3. `Flibble.CRM.Integration.csproj`

**Integrations:** Google, Office365/Graph, Xero, SageOne

**Work:**

* Update SDKs to .NET 10
* Replace ADAL → MSAL (if required)
* Validate API changes
* Update token/auth handling

**Complexity:** 🔴 High
**Time:** 120 – 180 hours
**Risks:**

* Breaking API changes
* Unsupported SDKs

---

## 4. Import Tooling

**Projects:** MFA.Flibble.Import, Flibble.Import

**Work:**

* Migrate pipelines to .NET 10
* Update file handling (CSV, IO)
* Update scheduling/jobs

**Complexity:** 🟡 Medium
**Time:** 80 – 130 hours

---

## 5. Background Services

**Services:**

* TaskReminder
* TaskSync
* OutlookImport
* EmailImport
* TicketImport

**Work:**

* Convert to Worker Services (.NET 10)
* Update SMTP / Exchange / IMAP libraries
* Validate scheduling & concurrency

**Complexity:** 🟡 Medium
**Time:** 200 – 250 hours
**Risks:**

* Hosting model changes
* API compatibility

---

## 6. Console Apps & Tooling

**Projects:** PopulateIndex, ScratchPad

**Work:**

* Retarget to .NET 10
* Update dependencies
* Ensure search/index libraries compatibility

**Complexity:** 🟢 Low–Medium
**Time:** 50 – 80 hours

---

## 7. SageOne Authorization Client

**Work:**

* Port to .NET 10
* Update OAuth flow

**Complexity:** 🟢 Low
**Time:** 40 – 50 hours

---

## 8. Database Migration (EF6 → EF Core)

**Work:**

* Analyze existing EF usage
* Port models & mappings
* Update LINQ queries
* Migrate migrations
* Validate performance & data

**Complexity:** 🔴 High
**Time:** 100 – 130 hours
**Risks:**

* Behavioral differences
* Query regressions

---

## 9. Frontend Libraries & JS Integrations

**Libraries:**

* FullCalendar
* CKEditor
* jQuery plugins
* SignalR client

**Work:**

* Replace/update libraries
* Implement Blazor JS interop
* Rebuild client bundles

**Complexity:** 🟡 Medium
**Time:** 130 – 150 hours

---

## 10. Miscellaneous

**Work:**

* Logging (log4net → Serilog optional)
* Middleware (replace HttpModules)
* Error handling
* Performance tuning

**Time:** 50 – 70 hours

---

# 🧭 Recommended Phased Plan

## Phase 1: Discovery & Inventory

* Duration: **2–4 weeks**
* Effort: **40–160 hours**

**Goals:**

* Dependency compatibility matrix
* EF migration decision
* Identify blocking libraries
* Confirm Blazor approach

---

## Phase 2: Proof of Concept (POC)

* Duration: **1–2 months**
* Effort: **120–240 hours**

**Goals:**

* Auth migration
* One module conversion
* SignalR validation

---

## Phase 3: Incremental Migration

**Approach:** Strangler Pattern

* Gradually replace MVC areas with Blazor
* Keep legacy system running in parallel

---

# 💡 Cost Optimization Options

### Option 1: Delay EF Core Migration

* Keep EF6 temporarily
* ✅ Reduces short-term cost
* ⚠️ Adds long-term risk

---

### Option 2: Backend First Strategy

* Migrate backend to .NET 10 first
* Delay Blazor UI rewrite

**Benefit:**

* Faster delivery
* Lower initial cost

---
