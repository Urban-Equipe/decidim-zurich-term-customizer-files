## Decidim Zürich – Term Customizer Files

This repository contains the **Term Customizer CSV files** used on the City of Zürich’s Decidim platform **«Mitwirken an Zürichs Zukunft»**.  
They define project‑specific and environment‑specific wording that overrides the standard Decidim translations (e.g. labels, button texts, help texts) without forking Decidim itself.

All process details and conventions are documented in the Decidim Zürich wiki under **A. Prozessdokumentation**, especially **A.3 Sprachfiles & Term-Customizer-Konventionen**:  
[A. Prozessdokumentation – decidim-zuerich Wiki](https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation)

---

### Role of the Term Customizer

- **Three translation layers**
  - **Top-level (Crowdin language files)**: Upstream Decidim translations maintained in Crowdin. Changes here affect all Decidim installations.
  - **Second-level (Decidim locale files)**: Rails `config/locales` YAML files shipped with the Decidim Zurich codebase. Used for Zürich‑specific defaults that should apply platform‑wide.
  - **Third-level (Term Customizer sets, this repo)**: Fine-grained overrides that apply to specific tenants, environments, organizations, or processes and take precedence over the other layers.

- **When to use Term Customizer (summary of wiki conventions)**
  - Prefer to change wording in **Crowdin** or **Decidim locale files** when the change is **generic** and reusable.
  - Use **Term Customizer** when a change is:
    - **Tenant-specific** (e.g. only for «Mitwirken an Zürichs Zukunft»),
    - **Environment-specific** (e.g. only on integration or only on production),
    - **Process- or organization-specific** (e.g. only for a particular participation process or organizational unit),
    - Or when **rapid wording changes** are needed without a code deployment.

For the full, authoritative description of these rules, see the wiki section **“A.3 Sprachfiles & Term-Customizer-Konventionen”** in  
[`https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation`](https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation).

---

### Repository contents and naming conventions

All files in this repository are **CSV exports of Term Customizer sets** from Decidim Awesome.

Each file name usually encodes:

- **Context / area** (`admin`, `mitwirken`, etc.).
- **Feature or section** (e.g. `news`, `organizations`, `MeinKonto`, `processMitwirken`).
- **Sometimes environment or status** (e.g. sets for archived or test processes, as described in the wiki).

These CSVs can be **re-imported into the Term Customizer** to restore or update a set. The set names and constraints (tenant, environment, process, organization) are managed in the Decidim backend UI, not in this repository.

---

### Working with the Term Customizer (summary of process)

The detailed process for editing wording is maintained in the wiki under **“A.3 Sprachfiles & Term-Customizer-Konventionen”** and **“D. Funktionsweise Term Customizer”** (see  
[`https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation`](https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation)).
The following is a condensed summary tailored to this repository:

1. **Decide the correct translation layer**
   - If the wording change should apply to **all Decidim instances** → propose a change to the **Crowdin** translation.
   - If it should apply to **all Zürich tenants** (Mitwirken, MeinQuartier, etc.) → adjust the **Rails locale (YAML) files** in the Decidim Zürich codebase.
   - If it is **specific to a tenant / environment / process / organization** → use or create a **Term Customizer set** and manage it via CSV.

2. **Edit a term via Term Customizer**
   - In the Decidim admin backend, open **Decidim Awesome → Term Customizer**.
   - Locate the relevant **set** (e.g. for a specific process or tenant), making sure its **constraints** (tenant, environment, process, organization) are correctly defined.
   - Adjust the terms via the UI or by **importing an updated CSV** derived from this repository.

3. **Export and version the changes**
   - After changes have been approved and deployed, **export the updated Term Customizer set** as CSV from the Decidim backend.
   - Save the CSV to this repository, following the existing naming pattern.
   - Commit and push the change so that the current platform wording is always reproducible from version control.

4. **Cleaning up unused sets**
   - The wiki defines the category **“Nicht (mehr) verwendete Translation Sets”**. If a set is no longer used (e.g. for a retired process), either:
     - Remove or disable it in the Decidim backend, and/or
     - Move or clearly mark the corresponding CSV file in this repository according to the locally agreed convention.

---

### Relation to process and environment management

The A. Prozessdokumentation also describes how Term Customizer is used in broader workflows, e.g.:

- **Process closure & archiving**  
  For completed processes, the Term Customizer is used to restrict or adapt terms for archived processes.  
  Example from the wiki: in the set `Mitwirken_prod_abgeschlosseneProzesse`, constraints ensure styling/wording only applies to archived processes. See section **“A.7 Prozessabschluss & -archivierung”** in  
  [`https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation`](https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation).

- **CSS & visual adjustments via Decidim Awesome**  
  While CSS overrides are managed separately under **Decidim Awesome → Eigene Styles**, both features use a similar **constraint** concept (tenant, process, organization) and are described together in the wiki. Term Customizer focuses on **text/labels**, while “Eigene Styles” focuses on **layout and design**.

---

### How to contribute / update files

1. **Make changes in the Decidim backend**
   - Coordinate wording changes according to the **GitHub project workflow** documented in section **A.1 Github-Workflow** of the wiki (ticket creation, review, testing on integration, deployment on production).  
     See: [A. Prozessdokumentation – decidim-zuerich Wiki](https://github.com/puzzle/decidim-zuerich/wiki/A.-Prozessdokumentation)
   - Update the appropriate Term Customizer set in the admin UI.

2. **Export the updated Term Customizer set**
   - Export the set as CSV from Decidim Awesome → Term Customizer.
   - Replace the corresponding CSV file in this repository (keep the established naming).

3. **Commit and push**
   - Commit the changed CSV (and any documentation updates in `README.md`).
   - Push to the central repository so that the exported wording stays in sync with the live platform.


