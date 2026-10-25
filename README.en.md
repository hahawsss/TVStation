<div align="center">

# TVStation

**Turn your media library into TV channels that keep playing themselves.**

Programs are always on. Nothing to pick, nothing to queue — turn it on and watch, just like TV.

**[中文](README.md)** | English

</div>

---

## Why this project exists

I've been running a media library for a long time, but every time it was the same story: endless tinkering — categorizing, scraping, organizing — and after a while I didn't even feel like watching anymore.

So the idea came: what if the things I actually like in my library could **play like a TV station** — turn it on and watch, exactly the way TV works.

That's what TVStation does. It turns the movies and shows on your NAS into real TV channels: series play from episode one in order and continue across days, movies rotate by time slot, with your own ads or intros in between. Turn on the TV and there's already something on; change channels with the remote — except everything playing comes from your own library.

**It's not a player. It's a TV station.** No playlists, no "continue watching", no poster wall to browse. Just channels.

---

## Low barrier to entry — especially with hard drive prices what they are

- **Works directly with network drives**: keep your library on a mounted cloud drive and it still plays. With pre-download caching, upcoming programs are pulled to local storage ahead of time — you don't have to put everything on disk.
- **One 2TB (or smaller) mechanical hard drive is enough**: plenty of people have old drives lying around — put them to use. Nearly 50 channels is no problem.
- **Low-spec hardware is fine**: the default "Direct Stream" mode doesn't re-encode, so CPU usage is minimal. Reference setup: i3 8100 + 16GB RAM + two 2TB drives + one 1TB drive — 70+ channels running.
- **Automatically picks Mandarin audio and subtitles**: if your movie files have them, Mandarin audio and subtitles are prioritized automatically.
- **Basically free**: paid features are mainly about channel creation. New installs get unlimited channel creation for the first half month; after that it drops to 3 channels — usually enough for a "General", "Movies" and "Kids" channel at home.
- **Built-in user guide** in the app: very simple to operate, very powerful features.

---

## Screenshots

<p align="center"><b>Program Guide</b> — your library's EPG: schedule a month ahead, visible, editable, clearable</p>

<p align="center"><img src="docs/screenshots/epg.png" width="90%"></p>

<p align="center"><b>Monitoring Dashboard</b> — live previews of all channels, plus CPU / memory / disk / hardware acceleration status</p>

<p align="center"><img src="docs/screenshots/dashboard.png" width="90%"></p>

<p align="center"><b>Media Library</b> — separate management for movies / series / ads, with scanning, subtitle matching and transcoding in one place</p>

<p align="center"><img src="docs/screenshots/library.png" width="90%"></p>

<p align="center"><b>TV Player App</b> — for Android TVs and boxes, up to 8 channels on one screen</p>

<p align="center"><img src="docs/screenshots/app.png" width="90%"></p>

---

## What it can do

**Scheduling**
- Series are tracked episode by episode; when one ends the next begins, continuing across days. When a series finishes, the next one starts automatically.
- When there isn't time for a full episode, ads fill the gap to the next hour — no cliffhangers mid-episode.
- Movies rotate randomly by time slot; supports series ordering like "part one today, part two tomorrow".
- Three scheduling modes: time-slot programming / folder order / continuous play.
- Schedule a month ahead; the program guide is visible, editable and clearable. Auto-generate next month's schedule with one toggle.

**Playback**
- Three modes: Transcode / Smart / Direct Stream (default — almost no CPU usage on a NAS)
- Intel iGPU hardware transcoding (QSV)
- External and embedded text subtitles, HDR to SDR, loudness normalization
- When the schedule runs out, the screen doesn't go black — a built-in TV test card plays automatically
- Playback segments are written to a RAM disk (tmpfs) — no wear on your drives

**Sources**
- Local directories + mounted network drives + pre-download cache
- Recognizes show names and episode numbers from nfo metadata; works even without scraping
- Duplicate cleanup, broken-link repair, automatic subtitle matching

**Watching**
- Standard M3U + XMLTV EPG — works with TVs, Kodi, VLC, Infuse
- Built-in Android TV player (APK installable directly from the NAS), with multi-view mode showing up to 8 channels on one screen
- Web monitoring dashboard with live previews of all channels

---

## Download

Release packages are attached to this repo's **Releases** (right sidebar on the web page):

**[→ Go to the Releases download page](https://github.com/hahawsss/TVStation/releases)**

| Package | Purpose |
|---|---|
| `TVStation-2.2.48.fpk` | fnOS native version: manual install via App Center — no Docker, no configuration |
| `tvstation-2.2.48-compiled-amd64.tar.gz` | Docker image package: Synology / QNAP / Unraid / Portainer / command line |

Then follow the "Install" section below.

---

## Install

| Your platform | How to install |
|---|---|
| **fnOS** | Easiest: App Center → Manual Install → pick the `.fpk` from the release package. No Docker, no configuration. |
| fnOS / Synology / QNAP / Unraid / Portainer / CLI (Docker) | Follow [`tvstation-2.2.48-docker/安装说明.md`](tvstation-2.2.48-docker/安装说明.md) (in Chinese); `docker-compose.yml` is ready to use. |

After install, open `http://NAS_IP:8890` in a browser, set up the admin account on first launch, then follow the five steps in the in-app **User Guide**: add media library → create channels → configure time slots → generate program guide → start broadcasting.

> One thing to watch with the Docker version: playback segments must be written to a **RAM disk** (already configured in the compose file).
> Many NAS "Container" UIs don't recognize this setting and will silently drop it when you edit the container there —
> if that happens, the app shows a red banner at the top of every page; click "Open Fix Wizard" and follow the steps for your platform.

---

## Free / Personal editions

**The free edition is not a trial — it's the complete software, usable forever.** Broadcasting, transcoding, subtitles, M3U/EPG, monitoring dashboard, network-drive sources and pre-download cache all work — the difference is **scale** and **convenience**.

| | Free | Personal |
|---|:---:|:---:|
| Channels | 3 | Unlimited |
| Broadcasting / transcoding / subtitles / M3U + EPG / dashboard | ✓ | ✓ |
| Network-drive sources + pre-download cache | ✓ | ✓ |
| Automatic schedule renewal | — | ✓ |
| Adjustable concurrency limit | — | ✓ |
| Loudness normalization | — | ✓ |
| Subtitle mismatch protection, subtitle/audio language priority | — | ✓ |
| Duplicate cleanup, automatic backup | — | ✓ |
| Custom media categories | — | ✓ |
| Multiple cache drives, multiple scan roots, scheduled scans | — | ✓ |
| Media source mount switching, media path migration | — | ✓ |

> New installs get unlimited channel creation for the first half month; after that the free-edition limit of 3 channels applies.
> The free edition's schedule doesn't renew automatically, but channels **never go black** — next month is automatically filled with the built-in TV test card, and you can always schedule real programs manually.

**Expiration never stops playback.** When a Personal license expires it automatically falls back to the free edition and keeps broadcasting — your channel configuration and schedules **won't lose a single entry**; renew and install the new certificate to restore everything immediately.

---

## Purchase

**Personal edition: ¥60 / year.**

1. Open the **License** page in the app, enter the email to receive the certificate, click **Generate Request Code**
2. Click **Open Purchase Page** — the request code is carried over automatically
3. Check the email, place the order, pay with **Alipay**
4. A minute or two after payment, the certificate appears on the order page and is sent to your email
5. Paste the certificate back into the **License** page and click **Install Certificate**

The certificate is **bound to your device**. Renewal follows the same steps and extends from the original expiration date — renewing early costs you nothing.

---

## FAQ

**Q: Is the free edition enough?**
Three channels at home (e.g. "General", "Movies", "Kids") is usually enough. Consider the Personal edition when you want more channels or conveniences like automatic schedule renewal.

**Q: Will it eat a lot of CPU?**
The default is "Direct Stream" — no re-encoding, just a few percent per channel. Transcoding only kicks in when the source codec isn't supported by your TV.

**Q: Why do some files never play?**
In "Direct Stream" mode, codecs unsupported by mpegts (RV40/VP9/AV1/WMV, etc.) are excluded. Check them in the channel's "Force-transcode codecs", or switch to "Smart" mode.

**Q: Will my data be locked in?**
No. License expiration only affects the channel count and paid features. Your library, channel configuration and schedules all live in a local database and can be backed up and exported at any time.

**Q: Does it need an internet connection?**
No — the software runs fully offline. For purchase, open the purchase page on any internet-connected device; the certificate is just a piece of text to paste into the app.

---

## License & Legal

**Scope of use**: This software is for **personal, non-commercial use only** and may not be used for public playback at business premises. See the in-app terms of use for details.

**Software license**: This software is distributed in binary form and is not open source. A purchased license is for **your own use only** and may not be resold or redistributed.

**Content responsibility**: This software only provides a broadcasting tool. It **does not provide, index, or recommend any film or TV content**. All sources you broadcast are provided by you, and you bear the corresponding responsibility.

**Open-source components**: This software includes the following free software components, each under its own license, independent of this software:

| Component | License | Source |
|---|---|---|
| FFmpeg | GPL-3.0 | https://sources.debian.org/src/ffmpeg/ |
| MKVToolNix | GPL-2.0 | https://sources.debian.org/src/mkvtoolnix/ |
| WenQuanYi Micro Hei | GPL-2.0 with font exception | https://sources.debian.org/src/wqy-microhei/ |
| Python and its standard library | PSF License | https://www.python.org/downloads/ |

The above components are taken **unmodified** from official Debian packages. For the complete source code of the corresponding versions, use the links above or contact us by email.

---

## Feedback

- Email: asdf269611012@163.com (please prefix the subject with "TVStation feedback")
- Purchase page: https://tvmssq.online/

<div align="center">
<br>
<sub>TVStation · Always something on</sub>
</div>
