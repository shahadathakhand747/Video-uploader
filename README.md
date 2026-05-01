# Video Uploader — Auto-Sync Source for Telegram Mini App

  This repository is the **source of truth** for `videos.json` — the video data used by the [Censor Coin Telegram Mini App](https://github.com/shahadathakhand747/Censor-coin-telegram-app).

  Whenever this file is updated, the automation workflow will push it to the Telegram app's repository automatically every night at **midnight Bangladesh Standard Time (BST / UTC+6)**.

  ---

  ## How It Works

  ```
  You update videos.json here
          ↓
  GitHub Actions workflow runs at midnight (BD time)
          ↓
  Reads videos.json from this repo
          ↓
  Completely replaces videos.json in Censor-coin-telegram-app
  (at: artifacts/censor-coin/public/videos.json)
          ↓
  Telegram Mini App serves the latest video data
  ```

  ---

  ## Repository Contents

  | File | Description |
  |------|-------------|
  | `videos.json` | The video data file — update this to change what the Telegram app shows |
  | `.github/workflows/sync-videos.yml` | GitHub Actions workflow that syncs the file daily |

  ---

  ## Automatic Sync Schedule

  The workflow runs **automatically every day at midnight Bangladesh Standard Time** (00:00 BST = 18:00 UTC).

  - Previous data in the Telegram app's `videos.json` is **fully replaced** with the latest version from this repo
  - No manual action needed — just update `videos.json` and the sync happens that night

  ---

  ## Manual Trigger (Workflow Dispatch)

  You can also run the sync manually at any time without waiting for midnight:

  1. Go to the **Actions** tab in this repository
  2. Click **"Sync videos.json to Telegram Mini App"**
  3. Click **"Run workflow"** → **"Run workflow"**
  4. The sync will run immediately

  ---

  ## videos.json Format

  The file is a JSON array of video objects. Example:

  ```json
  [
    {
      "id": "1",
      "d": "https://example.com/video.mpd",
      "t": 13
    },
    {
      "id": "2",
      "d": "https://example.com/video2.mpd",
      "t": 14
    }
  ]
  ```

  | Field | Description |
  |-------|-------------|
  | `id` | Unique video ID (string) |
  | `d` | Video URL or streaming manifest URL |
  | `t` | Duration in seconds |

  ---

  ## Workflow Status

  [![Sync videos.json](https://github.com/shahadathakhand747/Video-uploader/actions/workflows/sync-videos.yml/badge.svg)](https://github.com/shahadathakhand747/Video-uploader/actions/workflows/sync-videos.yml)

  ---

  ## Setup (Already Done)

  The following was already configured:

  - [x] `TARGET_REPO_TOKEN` secret added to this repo's Actions secrets (has write access to the Telegram app repo)
  - [x] Workflow file created at `.github/workflows/sync-videos.yml`
  - [x] Cron schedule set to `0 18 * * *` (18:00 UTC = midnight Bangladesh time)

  ---

  ## Target Repository

  The `videos.json` is pushed to:

  **Repository:** `shahadathakhand747/Censor-coin-telegram-app`  
  **File path:** `artifacts/censor-coin/public/videos.json`
  