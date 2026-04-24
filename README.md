# StravaAutoUploader

A Windows desktop app that logs a **manual Run** to your Strava account
with randomized distance, duration, and start time. Use it after each run
when you didn't have a watch or phone tracking.

| Field      | Range                            |
| ---------- | -------------------------------- |
| Sport      | Run                              |
| Distance   | 4.50 – 4.70 km (random)          |
| Duration   | 1h 02m – 1h 08m (random)         |
| Start time | 07:00 – 08:35 local time, today  |

> Use this only for runs you actually did. Strava's TOS prohibits posting
> activities you didn't perform.

---

## How to run

Just double-click **`StravaAutoUploader.exe`**.

Windows SmartScreen may say "Unknown publisher" the first time — click
**More info** → **Run anyway**. (The exe isn't code-signed because that
costs money for a personal-use app.)

The GUI opens with three cards:

1. **Connect your Strava app** — paste Client ID + Secret from
   <https://www.strava.com/settings/api> (Authorization Callback Domain
   must be `localhost`). *Skip this if your `.env` is already next to the
   exe — the GUI auto-loads it.*
2. **Authorize Strava access** — click **Get authorization link**, then
   **Copy** the URL into any browser. Click *Authorize* on Strava and the
   app detects it automatically (it listens on `localhost:8721` for the
   redirect).
3. **Log a run** — click **Preview**, then **Upload to Strava**.

You can move `StravaAutoUploader.exe` anywhere you like (Desktop, Start
Menu folder, pinned to taskbar). The `.env` next to it will travel with it
if you keep them together.

---

## Where your data lives

| File                                            | Purpose                                |
| ----------------------------------------------- | -------------------------------------- |
| `%APPDATA%\StravaAutoUploader\.env`             | Strava Client ID + Secret              |
| `%APPDATA%\StravaAutoUploader\tokens.json`      | OAuth refresh + access tokens          |

The exe also auto-detects a `.env` sitting next to it (or in its parent
folder) and copies it into `%APPDATA%` on first run.

---

## Troubleshooting

| Problem                            | Fix                                                               |
| ---------------------------------- | ----------------------------------------------------------------- |
| Windows SmartScreen blocks the exe | Click **More info** → **Run anyway**                              |
| GUI says "Not connected"           | Click **Get authorization link** in the Authorize card            |
| `Token refresh failed` / `401`     | Click **Reset authorization**, then **Get authorization link**    |
| Browser callback fails             | Callback domain in your Strava app must be `localhost`            |
| Port `8721` in use                 | Close anything listening on it before clicking authorize          |
| Need to wipe credentials           | Delete `%APPDATA%\StravaAutoUploader\.env` and reopen the app     |

---

## Files in this folder

```
StravaAutoUploader/
├── StravaAutoUploader.exe   The app (74 MB, fully self-contained)
├── .env                     Your Strava credentials (auto-loaded)
└── README.md                This file
```

That's it. Everything else (Electron runtime, source code, dependencies)
is bundled inside the exe.
