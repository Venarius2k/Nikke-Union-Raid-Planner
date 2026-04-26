# Nikke Union Raid Planner

**Nikke Union Raid Planner** is a planning tool for NIKKE: Goddess of Victory union raids. It takes your union's mock damage data and automatically builds the best possible hit assignment plan across all bosses and levels. It decides which player attacks which boss, in what order, and with which team.

Instead of spending hours and manually figuring out who should hit what, the planner runs your roster's mock data through many optimisation checks and algorithms that account for unit clashes between teams, the hit limit and boss HP thresholds across multiple difficulty levels. It then picks the plan that gets the most out of your roster, measured by how much of your union's combined damage potential was actually used and the efficiency of those players and the entire Union combined.

<img width="2547" height="1259" alt="image" src="https://github.com/user-attachments/assets/408990f6-0d80-41e9-a401-fccb700f60b0" /> <br>
<img width="3786" height="1893" alt="image" src="https://github.com/user-attachments/assets/821a8a14-7717-49b0-9c53-367af3c45596" />

---

## Features

- Automatic hit assignment across all bosses and levels.
- An algorithm that was iterated on multiple times over the months of development using real training data from my own Union.
- Multi-step optimisation algorithm that tries to maximise the total damage of your entire union and minimise loss.
- Efficiency statistics and unit usage breakdowns, to help you diagnose problematic players that you might otherwise miss when manually planning, best used if you want to improve player mocks and deal more damage.
- Exporting functionality to CSV/TSV or Google Spreadsheet.
- Completed hits functionality support. Once your players confirm a hit, if in an event it's a big overshoot or undershoot, the planner can rerun and re-optimise to find a better plan alternative.

---

## Download

Get the latest release from the [Releases](https://github.com/Venarius2k/Nikke-Union-Raid-Planner/releases) page.

> Download `Nikke Union Raid Planner(NURP).exe` and run it — no installation required.

---

## Requirements

- Windows 10 or later
- A Google account with access to Google Sheets (optional, see below)
- A Google Cloud service account JSON file (optional, see below)

---

## I don't want to set up Google Service Account, can I still use this?

You can upload .CSV files that contain mock/hit log data instead of needing to connect a Google Service Account. Assuming the .CSV file that is uploaded contains correct columns (See `Spreadsheet Setup` guide below), it will work out of the box.

This however, is not recommended as you will have to constantly export and upload the .CSV file during every hit log or mock, which can take time and allow you to make mistakes.

If you want to proceed in setting up a Google Service Account, see below.

## Google Service Account setup

### Step 1

The app connects to your Google Sheet using a service account. This is the only hard part besides setting up your Google Spreadsheet.

See below for written steps or click this [Youtube link](https://www.youtube.com/watch?v=iHIuJPqXeKw) for more visual guidance.

1. Go to [Google Cloud Console](https://console.cloud.google.com/welcome) and sign in to your Google account.
2. Create a new project by clicking **Select a project** in the top left → click **New Project** → name it → then click Create.
3. Select the project from the notification top right or click "Select a project" top left and choose your new project.
4. Click **"Google Cloud"** top left → **APIs & Services** and search for **Google Sheets API**, click it and click "enable".
5. Go to **APIs & Services → Credentials → Create Credentials → Service Account**
6. Fill in your Service Account name (eg, Nikke Raid Planner), go to permissions, click **"Basic"** and select **"Viewer"** access.
7. Click the service account you just created → **Keys** tab → **Add Key → Create new key → JSON**, once created, it will automatically be saved to your downloads folder.
8. Drag the newly created JSON file into your custom-made folder where you will keep your Nikke Union Raid Planner.exe file.

Please keep this JSON file secure and never share or distribute it.

### Step 2. Share your Google Sheet with the service account

1. Open your Google Sheet that the app will read data from.
2. Click **Share** top right
3. Paste the service account email (found inside the `.json` file under `"client_email"`) and give it **Viewer** access

### Step 3. Link the service account in the app

1. Launch the app via the .exe file provided and go to the **Config** tab
2. Under **Connection → Service Account JSON**, click **Browse** and select your `.json` file (or paste the full path manually)
3. A green tick confirms it loaded correctly

---

## Spreadsheets setup

The app reads from two worksheets in your Google Sheet, one for mocks and one for hit logs.

1. If you are new to raid planning and you don't use any Spreadsheets right now, go for Option A.
2. If you are actively managing spreadsheets and want to utilise this tool without using my templates, go for Option B.
3. Alternatively, if you want to combine the templates and your existing Spreadsheet, I would recommend a mix of Option A and B. Copy the entire spreadsheet (File > Make a Copy), and then migrating your existing Spreadsheet sheets to the new template. (This is only because it will keep the formula links unbroken when making a copy of the template instead of migrating each sheet to your existing Spreadsheet)

### Option A - I want to copy the templates to use for myself

I have created an extensive guide on how to get everything set up inside the [Google Spreadsheet](https://docs.google.com/spreadsheets/d/1g_0-pI8jw5akQhTRcA5RmBzqxpqofn-0LMMHypUDpTU/edit?gid=945543527#gid=945543527)

### Option B - I want to use my own spreadsheet

Your worksheets must have the following column names exactly (case-sensitive):

**Mocks worksheet**:

| Name | Boss | P1  | P2  | P3  | P4  | P5  | DMG | Available |
| ---- | ---- | --- | --- | --- | --- | --- | --- | --------- |

- `Name` - player name
- `Boss` - boss name (must match what you configure in Config → Bosses, eg, "Modernia" or "Crystal Armor")
- `P1`–`P5` - unit names used in the team
- `DMG`-— mock damage (accepts formats like `16.2b`, `16,200,000,000`, `16.200.000.000`)
- `Available`-— `Yes` or `No` if the player is available or not


<br><img width="1578" height="1348" alt="Screenshot 2026-04-26 220147" src="https://github.com/user-attachments/assets/20ac0994-8698-4e85-a3fe-1538d7848f07" /><br> 

**Hit Logs worksheet**:

| Name | Boss | Boss Level | P1  | P2  | P3  | P4  | P5  | DMG |
| ---- | ---- | ---------- | --- | --- | --- | --- | --- | --- |

- `Boss Level` - accepts `Level 1`, `Level 2`, `Level 3`, `Level 4` or plain integers `1`–`4`

<br><img width="1565" height="1352" alt="Screenshot 2026-04-26 220241" src="https://github.com/user-attachments/assets/f0ccb965-fae7-443c-aa1a-819a97e1fc02" /><br>

The above also assumes your spreadsheet supports flat data tables, and you have setup the functionality of automatically copying an entry made by a player (their mocks) into a flat data table that you would either export manually or load inside the Raid Planning app with a Google Service Account.

If you want to see how it works, click this [Google Spreadsheet](https://docs.google.com/spreadsheets/d/1g_0-pI8jw5akQhTRcA5RmBzqxpqofn-0LMMHypUDpTU/edit?gid=945543527#gid=945543527) link and take a look yourself.

### Linking your sheet in the app

1. Copy the full URL of your Google Sheet
2. In the app go to **Config → Connection → Google Sheet**
3. Paste the URL
4. Set the worksheet names to match your sheet

---

## Using the App

### Loading data

- **Load Mocks** - loads mock data from your Google Sheet.
- **Load Hit Logs** - loads confirmed hits from the hit log worksheet. These are locked in and cannot be changed by the planner. The planner builds a plan around the confirmed hits, if any. Click "Clear All Loaded Data" to remove them and load the Mocks again to regenerate the plan
- **Load from CSV** - alternative to Google Sheets. Export your mocks as a CSV and load them directly. Make sure the column names match the requirement (see Step 2)

### Generating a plan

The plan gets automatically generated when you press "Load Mocks". If you have Hit Logs, you need to press "Load Hit Logs" and then "Refresh Plan" for the new plan to be generated centred around the confirmed hits.
<br>When making any config changes, you'll be prompted to "Refresh Plan" to apply the new changes.

### Tabs

- **Level 1–4** - per-level assignment breakdown showing which player hits which boss, for how much damage and with which team.
- **Overview** - Assigned hits per player, player efficiency and meta unit usage to track who's using what. The "Issues" column also shows conflicting units that may appear if the player did not mock a good variety of teams.
- **Plan** - plan metrics (total damage, overshoot, damage lost, utilisation) and improvement tips.
- **Export** - download the full plan as CSV, TSV, or copy the ready-made text to paste into your Google Spreadsheet
- **Config** - changing boss names and weakness, overshot and safety buffers, meta units usage tracking and appearance settings.
- **Settings** - font size and display preferences.

---

## Settings & Config

Your configuration (sheet URL, boss names, buffer values, etc.) is saved automatically to `settings.json` in the same folder as the exe.

---

## License

Copyright (c) 2026 Venarius2k. All rights reserved.

This software may be downloaded and used free of charge. Redistribution of the original compiled application is permitted provided it is unmodified, and no fee is charged.

Decompiling, reverse engineering, disassembling, or otherwise attempting to derive the source code of this software is strictly prohibited. The source code may not be copied, modified, or distributed in any form.

---

## Support & Contact

- **Discord** — ven2k
- **Bug reports** — [GitHub Issues](https://github.com/Venarius2k/Nikke-Union-Raid-Planner/issues)
- **Support the project** — [Ko-fi](https://ko-fi.com/ven2k)

_All data loaded into this app stays on your machine and is never shared with anyone._
