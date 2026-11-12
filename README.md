# SimpliVity Deploy Kit

A single self-contained HTML workbook for HPE SimpliVity deployments, delivered by TD SYNNEX Advanced Solutions. It is the first vendor implementation of the [service-deployment-matrix](https://github.com/MJP-76/service-deployment-matrix) framework: every deployment is **vendor + one service** — deployment, upgrade or expansion — and the same three services apply to every vendor.

Open `simplivity-deploy-kit.html` in any modern browser — no server, no build, no install.

## Signing in

- **Customer** — sign in with the customer ID and password issued by TD SYNNEX. You see only the deployments created for your company; pick one to open its scoped workbook (site details, pre-flight checklist, NTP/DNS, vCenter passwords) and email them back to TD SYNNEX when complete.
- **Deployment Engineer** — unlock with the team password. The **Customers** tab manages everything: add a customer (name, sign-in ID, password), create / rename / delete their deployments, and reset a customer password. Opening a customer loads their full workbook — network plans, credentials, Sections 1–6 per node, vCenter & Arbiter, XML and the reference documents.

## What it does

- **DeploymentConfiguration XML** — import an existing SimpliVity Deployment Manager saved configuration XML to pre-fill everything, or export the file Deployment Manager consumes.
- **Reference documents** — print / export / email a branded deployment reference (TD SYNNEX palette, versioned, optional credentials).
- **Shortcuts** — one-click iLO (https), ESXi/OVC (PuTTY), vCenter (https/SSH/WinSCP/VAMI), plus Deploy/Upgrade Manager launchers via the portable Windows launcher kit (Setup tab).
- **Node quick-fill** — *Add nodes…* asks how many; fill in the first node's addresses and save to pre-fill the rest (IPs step by last octet, netmask & gateway copied).
- **Vendor × service** — the New deployment dialog asks for vendor and service, and names auto-generate as `<vendor> <Service> - <date>`.
- **Update check** — on load the kit compares itself with the repository's `version.json` and offers the newer download when one exists.

## Data

Each customer account and deployment is encrypted (AES-GCM; keys derived from passwords with PBKDF2) and stored per path in this browser's localStorage, which doubles as the offline cache. A fine-grained personal access token (**Contents: read and write**, this repository only) ships baked into the file, so encrypted files sync through GitHub out of the box and customers on other machines see updates. If the token is missing or expired, the kit warns and keeps everything in this browser instead; a replacement can be pasted in **Setup → Shared store** (saved in this browser's localStorage as an override) and the baked token can be restored with **Clear override**. Nothing readable leaves the browser either way.

Storage keys are namespaced by the product ID (`KIT_NS = 'svt'`) at the top of the script, so future kits from the framework can share a machine without colliding — **never change that constant for a shipped kit, or its users' saved data is orphaned.**

**Rotating the baked token:** create a new fine-grained PAT (repository `MJP-76/service-deployment-matrix`, Contents: read and write, ~90 days), replace `KIT_GH_TOKEN` in the script, bump `KIT_VERSION` and `version.json` together, then redistribute the file so copies pick up the new token (and the update banner prompts older copies).

Use **Setup → Save into file…** to bake the current deployment into the file itself for offline handover — the recipient opens it with the team password.

### Previous version

Data saved by earlier single-user copies stays available: the sign-in page offers **Open saved data from the previous version**, which keeps the familiar Customer Engineer / Deployment Engineer sections and their passwords.

## Sharing with a customer

Give the customer this file (download link or USB) plus their sign-in ID and password. The repository is public, so anyone with the link can download the file — but without valid sign-in credentials there is nothing to open, and every account and deployment in it is encrypted.

> Note: browsers won't run HTML from the SharePoint/Teams web preview — the file must be opened from the synced desktop copy or a direct download.
