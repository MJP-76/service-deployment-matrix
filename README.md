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

## Data

Each customer account and deployment is encrypted (AES-GCM; keys derived from passwords with PBKDF2) and stored per path in this browser's localStorage, which doubles as the offline cache. Add a fine-grained personal access token in **Setup → Shared store** (scoped to this repository, Contents: read/write) to sync the same encrypted files through GitHub — customers on other machines then see each other's updates. Without a token everything stays in this browser; nothing readable leaves it either way.

Use **Setup → Save into file…** to bake the current deployment into the file itself for offline handover — the recipient opens it with the team password.

### Previous version

Data saved by earlier single-user copies stays available: the sign-in page offers **Open saved data from the previous version**, which keeps the familiar Customer Engineer / Deployment Engineer sections and their passwords.

## Sharing with a customer

Give the customer this file (Teams/SharePoint folder, download link or USB) plus their sign-in ID and password. Folder permissions control who can obtain the file; their credentials control what they see once it is open.

> Note: browsers won't run HTML from the SharePoint/Teams web preview — the file must be opened from the synced desktop copy.
