# 🗺️ Seal Roadmap

This document outlines the project development roadmap for **Seal**, tracking release milestones from the v2.0.0 architectural overhaul to future releases.

---

## 🎯 Milestone 1: v2.0.0 Stabilization & V1 Downloader Retirement (In Progress)

**Target**: `v2.0.0-alpha.6` / `v2.0.0-beta.1`  
**Goal**: Complete the transition from the legacy single-job `Downloader` (V1) to the concurrent, queue-backed `DownloaderV2`, eliminate technical debt, and ensure core stability.

### Tasks:
* [x] **Formalize Project Roadmap**: Establish `ROADMAP.md` and organize milestone targets.
* [ ] **Retire Legacy V1 Downloader**:
  * [ ] Migrate [`TaskListPage.kt`](app/src/main/java/com/junkfood/seal/ui/page/command/TaskListPage.kt) to `DownloaderV2`.
  * [ ] Migrate [`TaskLogPage.kt`](app/src/main/java/com/junkfood/seal/ui/page/command/TaskLogPage.kt) to `DownloaderV2`.
  * [ ] Update [`YtdlpUpdater.kt`](app/src/main/java/com/junkfood/seal/ui/page/YtdlpUpdater.kt) to check `DownloaderV2` queue state rather than legacy `Downloader.downloaderState`.
  * [ ] Refactor [`NotificationActionReceiver.kt`](app/src/main/java/com/junkfood/seal/NotificationActionReceiver.kt) to use `DownloaderV2.cancel()`.
  * [ ] Safely remove `Downloader.kt`, `DownloadPage.kt`, and `HomePageViewModel.kt`.
* [ ] **DownloaderV2 Polish**:
  * [ ] Ensure custom command executions are fully managed within the `DownloaderV2` queue.
  * [ ] Multi-task notification action handling (cancel/restart).
* [ ] **Testing & Quality Assurance**:
  * [ ] Unit tests for `TaskFactory` and task queue state transitions.
  * [ ] Test task backup & restore serialization via MMKV.

---

## 🧪 Milestone 2: v2.0.0 Beta & Release Candidate (RC)

**Target**: `v2.0.0-rc.1`  
**Goal**: Polish UI/UX, verify compatibility across Android versions (API 24–35), and complete translation sync.

### Tasks:
* [ ] **Version Bump**: Transition `Version.kt` from `Version.Alpha` to `Version.Beta` and `Version.ReleaseCandidate`.
* [ ] **Adaptive UI & Motion Polish**:
  * [ ] Verify sheet insets, keyboard (IME) behavior, and predictive back gestures on Android 14+.
  * [ ] Optimize recomposition counts in `DownloadPageV2` grid items.
* [ ] **Foreground Service & Lifecycle Audit**:
  * [ ] Verify foreground service type permissions (`dataSync` / `mediaProcessing` vs `specialUse`) for Android 14/15 background download reliability.
* [ ] **Weblate Translation Freeze**:
  * [ ] Sync and merge pending community translations from Hosted Weblate.

---

## 🚀 Milestone 3: v2.0.0 Stable Release

**Target**: `v2.0.0`  
**Goal**: Official general availability release.

### Tasks:
* [ ] Finalize `CHANGELOG.md` with complete migration guide from v1.13.x.
* [ ] Update `README.md` screenshots showing the new Material 3 download queue and bottom sheets.
* [ ] Publish production binaries on GitHub Releases and submit metadata to F-Droid.

---

## 🔮 Milestone 4: v2.1+ Post-v2 Enhancements

**Target**: `v2.1.0` and beyond  
**Goal**: Next-generation features and power-user tools.

### Planned Features:
* **Scheduled Downloads**: Queue downloads to run during specified off-peak hours (e.g. overnight or unmetered Wi-Fi).
* **Smart Network Recovery**: Automatic queue pause when switching to metered data, and automatic resume on Wi-Fi reconnect.
* **Audio Tag Editor**: Quick in-app editing of audio metadata (Title, Artist, Album, Cover Art) prior to file write.
* **Plugin / Extractor Updates**: In-app management for yt-dlp extractor plugins.
