# LimeSurvey OSD Importer Plugin

A [LimeSurvey](https://www.limesurvey.org) plugin that imports [OpenScales Definition (.osd)](https://openscales.net) files directly into LimeSurvey as surveys.

## Features

- Upload any `.osd` file from the LimeSurvey admin UI
- Supports all OSD item types:
  - `likert` → Array (F) grid, grouped by response scale
  - `multi` → List radio (L)
  - `multicheck` → Multiple choice (M)
  - `section` → New question group (page break)
  - `inst` → Text display (X)
  - `short` / `long` → Short/long free text (S/T)
  - `vas` → Multiple Numerical slider (K) with slider attributes set automatically
  - `grid` → Array (F) with custom rows and columns
- Multi-language surveys (specify primary + additional language codes at import)
- Parameter substitution: scales with a `parameters` block show input fields at import time
- Sections map to LimeSurvey question groups (one page per section)
- Compatible with LimeSurvey 6.x / PHP 8.x

## Installation

### Manual

1. Copy the `OSDImporter/` directory into your LimeSurvey `plugins/` folder
2. Go to **Admin → Configuration → Plugin Manager**
3. Find **OSDImporter** and click **Activate**

### Docker (development)

```bash
./install.sh [container_name]
# default container name: limesurvey
```

Or register directly in the database:

```sql
INSERT INTO lime_plugins (name, plugin_type, active, version, load_error, load_error_message)
VALUES ('OSDImporter', 'user', 1, '0.1.0', 0, '');
```

## Usage

Navigate to:
```
/index.php/admin/pluginhelper/sa/fullpagewrapper/plugin/OSDImporter/method/index
```

Or use the **Import OSD** link in the admin menu (if your theme supports `extraMenus`).

Upload a `.osd` file, set the primary language code (e.g. `en`), optionally add
comma-separated extra language codes, fill in any parameter values, and click **Import Survey**.

On success, a link to the new survey is returned. Warnings (unsupported item types,
VAS slider attribute reminders, etc.) are shown below.

## Notes

- Scoring, conditional visibility (Expression Manager), and branching are not
  automatically configured — these must be set up manually after import.
- VAS sliders: the plugin sets `slider_layout`, `slider_min`, `slider_max`,
  `slider_accuracy`, and `slider_orientation` automatically on the K-type question.

## License

Apache 2.0 — see [LICENSE](LICENSE).

Copyright 2025 Shane T. Mueller / [OpenScales Project](https://openscales.net)
Contact: shanem@mtu.edu
