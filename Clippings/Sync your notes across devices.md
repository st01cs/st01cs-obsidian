---
title: "Sync your notes across devices"
source: "https://help.obsidian.md/sync-notes#Git"
author:
  - "[[Obsidian Help]]"
published:
created: 2025-10-01
description: "Sync your notes across devices - Obsidian Help"
tags:
  - "clippings"
---
Obsidian stores notes locally on your device so you always have access to them, even offline. To access your notes on multiple devices you need to set up a sync method.

This guide covers common sync methods, including tips to avoid data loss and ensure a smooth experience.

We also recommend reading our [backup guide](https://help.obsidian.md/backup) to protect your data.

## Syncing methods

With Obsidian your data is simply stored as files in a folder called a [vault](https://help.obsidian.md/sync/vault-types). This means there are many ways to sync your data.

These are a few commonly used sync methods reported by members of the [Obsidian Community](https://obsidian.md/community):

## Obsidian Sync

The most straightforward and officially supported sync method is our first party solution: [Obsidian Sync](https://help.obsidian.md/sync).

Follow the [setup guide](https://help.obsidian.md/sync/setup) to configure Obsidian Sync.

Avoid using Obsidian Sync alongside other cloud services like Dropbox or OneDrive **for the same vault**, as this can cause data conflicts and file corruption.

## iCloud

iCloud can be used to sync vaults between iOS and macOS. However, **iCloud Drive on Windows** may lead to file duplication or corruption.

**How to create and store your vault in iCloud Drive**:

- **Enable iCloud Drive**:
	- On macOS: Go to **System Preferences → Apple ID → iCloud → iCloud Drive**.
	- On iOS: Go to **Settings → \[Your Name\] → iCloud → iCloud Drive**.
- **Create a new vault in iCloud**:
	- On macOS:
		1. Open **Obsidian** and select **Create new vault**.
		2. In the file picker, navigate to **iCloud Drive → Obsidian**.
		3. Create a folder for your vault and name it.
		4. Select **Create** to finish.
	- On iOS:
		1. Open **Obsidian** and tap **Create new vault**.
		2. Enter a name for your vault.
		3. Toggle on **Store in iCloud**.
		4. Tap **Create**.
- **Open the vault on another Apple device**:
	- On another macOS or iOS device, open **Obsidian**, go to the [Vault switcher](https://help.obsidian.md/manage-vaults), and select **Open folder as vault**. Navigate to **iCloud Drive → Obsidian**.

Best Practices

- For **macOS 14 (Sonoma) and earlier**: Disable **Optimize Mac Storage** in iCloud settings to prevent files from being offloaded. This setting affects all iCloud storage on the device, not just Obsidian.
- For **macOS 15 (Sequoia)**: Right-click the **Obsidian** folder in iCloud Drive and select **Keep Downloaded**.

## OneDrive

Before using OneDrive for syncing, ensure that your vault folder is marked as **Always keep on this device**. This prevents OneDrive from offloading files and causing Obsidian to think they are missing.

**How to create and store your vault in OneDrive**:

OneDrive may not function well for Android syncing. Consider using apps like [Dropsync](https://play.google.com/store/apps/details?id=com.ttxapps.dropsync) or [FolderSync](https://play.google.com/store/apps/details?id=dk.tacit.android.foldersync.lite).

Best Practices:

- Always keep your vault files **Available Offline** by right-clicking the folder and selecting **Always keep on this device**.
- Avoid using OneDrive's **Files On-Demand** feature for vaults to prevent syncing issues.

## Google Drive

Google Drive is not officially supported for syncing Obsidian vaults on iOS. Consider using a third-party solution or plugin to sync on iOS.

**How to create and store your vault in Google Drive**:

Best Practices:

- Set vault files to **Available Offline** in Google Drive to avoid syncing issues due to offloading.
- For iOS, consider alternative methods like [Obsidian Sync](https://help.obsidian.md/sync), [iCloud](https://help.obsidian.md/sync-notes#iCloud), or use the **Remotely Save** plugin.

## Syncthing

Syncthing is a decentralized file synchronization tool that doesn't rely on cloud storage. It syncs your vault directly between devices over the network or internet.

**How to create and store your vault using Syncthing**:

Syncthing works best when at least one device is always on to ensure continuous syncing.

Best Practices:

- For local syncing, ensure all devices are connected to the same network.
- Exclude `.obsidian` from syncing if you want separate settings on each device.
- Use ignore patterns to avoid syncing temporary or backup files.

## Git

**Git** is a version control system that allows you to track changes, collaborate with others, and sync your vaults through repositories like GitHub, GitLab, or a self-hosted server.

**How to sync your vault using Git**:

1. **Set up a remote repository**:
	- Create a repository on a Git hosting platform (e.g., GitHub, GitLab, or a self-hosted server).
2. **Sync your vault**:
	1. Open a terminal or Git GUI (e.g., GitKraken, Sourcetree).
	2. Initialize a Git repository in your vault folder using `git init`.
	3. Add the remote repository: `git remote add origin [URL]`.
	4. Commit your changes: `git add .` and `git commit -m "Your message"`.
	5. Push the changes: `git push origin main`.
3. **Pull changes on other devices**:
	- Clone the repository on another device and pull changes using `git pull origin main`.

Git provides strong version control, but syncing isn't automatic. You must manually push and pull changes.

## iPhone and iPad syncing

**Recommended options**:

- [Obsidian Sync](https://help.obsidian.md/sync)
- [iCloud](https://help.obsidian.md/sync-notes#iCloud)

Avoid syncing the same vault across multiple services (e.g., using both Obsidian Sync and iCloud simultaneously) to prevent data conflicts or corruption.

**Unsupported options**:  
The following services aren't officially supported on iOS, but users have found workarounds using third-party tools or plugins:

- Dropbox
- Google Drive
- OneDrive
- Syncthing

Some users have successfully used plugins like **Remotely Save** or **LiveSync** to sync vaults on iOS. However, these methods aren't officially supported, and results may vary.

### Working Copy

**Working Copy** is a Git client for iOS that allows you to clone, commit, and push changes to a Git repository. It works well for syncing Obsidian vaults via Git, though some features require a paid in-app purchase.

**How to sync your vault using Working Copy**:

1. **Install Working Copy**:
	- Download the **[Working Copy](https://apps.apple.com/us/app/working-copy-git-client/id896694807)** app on your iPhone or iPad.
2. **Clone your Git repository**:
	- Open Working Copy, tap **Add Repository**, and enter your repository URL (e.g., GitHub, GitLab).
3. **Link repository to Obsidian**:
	- Link the cloned repository folder to an empty vault in **Obsidian**.
4. **Commit and push changes**:
	- After editing notes in Obsidian, use Working Copy to **Commit** and **Push** changes to the remote repository.
	- On other devices, pull changes using Git to sync the vault.

While Working Copy isn't officially supported, many users have successfully used it to sync vaults with Git.

## Comparison

|  | End-to-end   encryption | Version   history |
| --- | --- | --- |
| [Obsidian Sync](https://help.obsidian.md/sync) | ✅ | ✅ |
| iCloud | Optional | ❌ |
| OneDrive | ❌ | ❌ |
| Google Drive | ❌ | ❌ |
| Syncthing | Optional | ✅ |
| Git | ❌ | ✅ |

## Frequently asked questions

**Why is my preferred syncing service not officially supported?**

Unlike some note-taking apps that access one file at a time, Obsidian requires access to the entire vault for its features (e.g., updating links when renaming a file). This makes it difficult for some services to function reliably with Obsidian.

**Why do I need to keep files "Available Offline"?**

If services like OneDrive or iCloud offload files (e.g., using **Files On-Demand** or **Optimize Mac Storage**), Obsidian can't access them, causing sync issues. Mark your vault folder as **Always keep on this device** (OneDrive) or ensure **Keep Downloaded** is enabled (iCloud).

**How do I manage different configurations for my vaults?**

Obsidian allows you to customize the configuration folder per device using the [Config folders](https://help.obsidian.md/configuration-folder) feature.