# TD SYNNEX Deployment Kit

A single self-contained HTML workbook for HPE and Nutanix deployments, delivered by TD SYNNEX Advanced Solutions. It is the reference implementation of the [service-deployment-matrix](https://github.com/MJP-76/service-deployment-matrix) framework: every deployment is **vendor + product + one service** — deployment, upgrade or expansion — and the same three services apply to every vendor.

Current version: **1.8.1** (see `version.json`).

| Vendor | Products |
|---|---|
| HPE | SimpliVity, Hardware |
| Nutanix | Nutanix Cloud Infrastructure |

Open `index.html` in any modern browser — no server, no build, no install.

## Signing in

- **Customer** — sign in with the customer ID and password issued by TD SYNNEX. You see only the deployments created for your company; pick one to open its scoped workbook (site details, pre-flight checklist, NTP/DNS, vCenter passwords) and email them back to TD SYNNEX when complete.
- **Deployment Engineer** — unlock with the team password. The **Customers** tab manages everything as **Partner › Customer › Year › Deployment**: add a customer (name, sign-in ID, password), create / rename / delete their deployments, and reset a customer password. A partner must be chosen explicitly before a customer can be added. New work is always a new deployment — a deployment never moves between customers or partners.

## What it does

- **HPE SimpliVity workbook** — per-node Sections 1–8 (iLO, ESXi, OVC, storage VMkernel, OVC storage, federation, vCenter, arbiter), the network plan, credentials, and the DeploymentConfiguration XML that SimpliVity Deployment Manager imports. An existing saved XML can also be imported to pre-fill everything.
- **Nutanix workbook** — repeatable clusters, each with Prism Element, hosts & CVMs, containers, VLANs, switch ports, credentials, authentication, DNS/NTP and SSL, plus one Prism Central per cluster. Separate **Migration** and **Nutanix Central** tabs cover Nutanix Move and the multi-cluster endpoints/certificates.
- **Pre-flight workbook import** — read a completed vendor questionnaire and create the deployment, with a preview before anything is written (see below).
- **Reference documents** — print / export / email a branded deployment reference (TD SYNNEX palette, versioned, optional credentials).
- **Shortcuts** — one-click iLO (https), ESXi/OVC (PuTTY), vCenter (https/SSH/WinSCP/VAMI) through the portable Windows launcher kit.
- **Node quick-fill** — *Add nodes…* asks how many; fill in the first node's addresses and save to pre-fill the rest (IPs step by last octet, netmask & gateway copied).
- **Update check** — on load the kit compares itself with the repository's `version.json` and offers the newer download when one exists.

## Importing a vendor workbook

**Import pre-flight…** accepts an `.xlsx` from either vendor and says which one it found.

| Vendor | What it reads | Notes |
|---|---|---|
| HPE SimpliVity | Every template generation from 08-2019 to 11-2023: the sectionless layouts, the C-column sections (02-2020 → 11-2021), the D-column sections (11-2023 onwards) and the revision that adds a vMotion section | Fields are matched by **section and label**, so field-key changes, a shifted or inserted column and blank serial numbers do not break it. One deployment per datacenter sheet, because each has its own vCenter, arbiter and network plan. |
| Nutanix | TD SYNNEX Nutanix Installation Workbook — `Cluster - NN`, `Prism Central - NN`, `Migration`, `Nutanix Central` | One deployment per workbook. Each `Cluster - NN` becomes a cluster and its `Prism Central - NN` attaches by number; containers, VLANs, switch ports, credentials, authentication and Prism Central settings are carried across. |

**Not read:** the 2019–2022 Nutanix questionnaires and the 2025 site-per-sheet workbooks (`Brownhills - Production` style). They are recognised as Nutanix and refused with an explanation rather than misread.

**Credentials** are never taken from the workbook unless *Import passwords found in the document* is ticked — everything defaults to `TBA` / `TBA Onsite`. `As per OEM` is kept either way, because it is an instruction rather than a secret. Serial numbers, IPMI addresses and similar identifiers are always imported.

## Data

Each customer account and deployment is encrypted (AES-GCM; keys derived from passwords with PBKDF2) and stored per path in this browser's localStorage, which doubles as the offline cache. A fine-grained personal access token (**Contents: read and write**, this repository only) is pasted once per browser in **Setup → Shared store**, so encrypted files sync through GitHub and customers on other machines see updates. No token ships in the page. If the token is missing or expired, the kit says so and keeps everything in this browser instead. Nothing readable leaves the browser either way.

Customer folders in the repository are opaque hashes (`customers/c-…`), never customer names; `registry.enc` is the encrypted index. Sign-in lasts 60 minutes of inactivity and survives a refresh; **Sign out** clears it, and any open dialog closes when the session locks.

Storage keys are namespaced by the product ID (`KIT_NS = 'deploy-kit'`) at the top of the script, and the customer-folder salt uses the same prefix. **Never change either for a shipped kit, or its users' saved data is orphaned.** Older `svt` keys are migrated once on first load.

**Rotating the token:** create a new fine-grained PAT (repository `MJP-76/service-deployment-matrix`, Contents: read and write, ~90 days) and paste it in **Setup → Shared store** on each machine. Bump `KIT_VERSION` and `version.json` together when shipping other changes so the update banner prompts older copies.

## Launcher kit (Windows)

Setup → Launcher kit produces three files — `svt-launcher.vbs`, `svt-launcher.ini` and `register-protocols.reg` — which let the SSH and WinSCP shortcuts hand a session to the portable tools.

- **PuTTY** — direct `putty.exe` download.
- **WinSCP** — WinSCP ships only a **portable ZIP** (there is no single portable `.exe`); unzip `WinSCP.exe` next to the launcher. The link is version-pinned and needs an occasional bump.
- **Kit folder** — defaults to `~/Downloads`, which is where the three files land. The `.reg` needs a full Windows path (e.g. `C:\Users\you\Downloads`), and the kit warns if it is still `~`.
- **Deployment / Upgrade Manager links were removed** — their installed path and version vary, so the kit exports the XML for you to import manually instead.

## Sharing with a customer

Give the customer this file (download link or USB) plus their sign-in ID and password. The repository is public, so anyone with the link can download the file — but without valid sign-in credentials there is nothing to open, and every account and deployment in it is encrypted.

> Note: browsers won't run HTML from the SharePoint/Teams web preview — the file must be opened from the synced desktop copy or a direct download.
