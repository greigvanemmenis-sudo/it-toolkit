# IT Tech Toolkit

A single self-contained HTML page of PowerShell and macOS scripts, plus step-by-step fix-it guides, for first and second line IT support.

**Live page: https://toolkit.vantagecybersolutions.com/**

No install, no build step, no internet connection needed once you have the file. Open it in any browser, from a desktop, a USB stick or a shared drive (`\\server\it\toolkit.html`). The live link above is the same file, hosted, so it works from any machine with a browser.

## What's in it

**157 scripts** across 14 categories:

| Windows | macOS |
| --- | --- |
| System info, Network, Security & triage | macOS (general triage, network, apps, printing) |
| Performance & disk, Printing | macOS accounts & domain (AD bind, mobile accounts, SecureToken, FileVault) |
| Accounts & AD, Windows Update | |
| Office / Teams / OneDrive, Remote admin | |
| Hardware & drivers, Event logs | |

Plus an **AWS VPN Client** section covering both platforms: version checks, log readers, endpoint and adapter checks, SAML callback port, profile backup, and a one-shot clean wipe and reinstall for each platform.

**26 fix-it guides** for the usual tickets: slow PC, no internet, printing, Teams, Outlook, account lockouts, domain trust failures, suspicious processes, blue screens, disk full, Windows Update, mapped drives, OneDrive, AWS VPN connection and update problems, and nine macOS guides including the "red dot at login" domain walkthrough. Each step links straight to the script that does the job.

**36 Run-box shortcuts** (Windows + R) and a **ticket notes** scratchpad.

## How it works

**Fill-in boxes** at the top take a computer name, IP, username, process, app, domain or file path. Every script on the page updates live, and Copy gives you the filled-in version. The values are remembered between visits, so you type your own domain once and it sticks.

**Badges** on each script say what it needs before you run it:

`Run as admin` / `Needs sudo` — elevation required.

`Makes changes` — it changes the machine; read it first. Anything without this badge only reads information.

`macOS` — Terminal command for a Mac, downloads as `.sh`. Everything else is PowerShell and downloads as `.ps1`.

`Remote`, `Needs RSAT`, `Internet` — other prerequisites.

**Search** with `/` from anywhere. It covers titles, descriptions and the script bodies.

**Favourites and notes** are stored in each person's own browser (`localStorage`), so a shared copy on a network drive gives every tech their own set without anyone overwriting anyone. They are per-browser and per-address, so the hosted copy and a local copy keep separate lists.

## Adding your own scripts

Open the file in a text editor and find a line beginning `S('`. Each script is one call:

```javascript
S('unique-id','category','Title',['admin','changes'],
'What it does and when to use it.',
String.raw`
Your script here
`);
```

Categories are listed in the `CATS` array near the top. Fill-ins are `{{COMPUTER}}`, `{{IP}}`, `{{USER}}`, `{{PROCESS}}`, `{{APP}}`, `{{DOMAIN}}` and `{{FILE}}`.

Two things to avoid inside `String.raw` blocks, because they break the page: backticks (use `Write-Host ""` instead of `` `n `` in PowerShell) and `${...}`.

Guides live in the `GUIDES` array. `[[script-id]]` in a step becomes a clickable chip that jumps to that script.

## Notes

Placeholder values are used throughout — `corp.example.com` for the domain, `localadmin` for a local admin account, `domainadmin` for an AD account with rights to remove computer objects. Replace them with your own. Nothing in this repo is specific to any organisation, and nothing organisation-specific should be added to it, because the page is public.

Scripts marked `Makes changes` do what they say. Read before running, especially the clean reinstall and printing system reset, and check with whoever owns the endpoint before touching security or management agents.

Provided as-is, with no warranty. You are responsible for what you run on someone else's machine.
