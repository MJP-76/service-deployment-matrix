# SimpliVity Deploy Kit

A single self-contained HTML workbook for HPE SimpliVity deployments, delivered by TD SYNNEX Advanced Solutions.

Open `simplivity-deploy-kit.html` in any modern browser — no server, no build, no install.

## What it does

- **Two sections, two passwords** — *Customer Engineer* (project details, pre-flight checklist, NTP/DNS, vCenter passwords) and *Deployment Engineer* (network plans, per-node Sections 1–6, vCenter & Arbiter, XML, documents). Both are asked for on every load.
- **DeploymentConfiguration XML** — import an existing SimpliVity Deployment Manager saved configuration XML to pre-fill everything, or export the file Deployment Manager consumes.
- **Reference documents** — print / export / email a branded deployment reference (TD SYNNEX palette, versioned, optional credentials).
- **Shortcuts** — one-click iLO (https), ESXi/OVC (PuTTY), vCenter (https/SSH/WinSCP/VAMI), plus Deploy/Upgrade Manager launchers via the portable Windows launcher kit (Setup tab).
- **Node quick-fill** — *Add nodes…* asks how many; fill in the first node's addresses and save to pre-fill the rest (IPs step by last octet, netmask & gateway copied).

## Data

Everything stays in the browser's localStorage — nothing is uploaded. The deployment section is encrypted under its password; the customer section is stored as-is.

Use **Setup → Save into file** to bake the current data into the file itself for handover to the next engineer.

## Sharing with a customer

Put a copy of the file in the customer's permissioned Teams/SharePoint folder — folder permissions are the access control. The customer opens it, fills their section, and the deployment engineer picks it up from the same file.

> Note: browsers won't run HTML from the SharePoint/Teams web preview — the file must be opened from the synced desktop copy.
