<div align="center">

  # Hash Silo

</div>

Hash Silo is a local password-hash utility for testing candidate passwords & generating compatible targets. It supports 515 Hashcat-compatible modes across common operating-system credentials, archives, encrypted volumes, password managers, databases, wallets, network authentication formats, and more.

All hashing and verification runs on the local machine. Hash Silo does not access the network or send usage data anywhere off of the local machine.

## Highlights

- 515 registered Hashcat-compatible modes
- Password verification & target generation where supported by the selected format
- Hash-type detection with all structurally compatible matches shown when a target is ambiguous
- Text and file-backed targets
- Username-aware formats when the selected mode requires one
- Reusable profiles with isolated targets & password-attempt history
- Export of failed password attempts for continued work elsewhere
- On-screen password-history masking to reduce shoulder surfing
- Optional SQLCipher database encryption/password locking
- Installed & portable data-storage modes
- Light & dark desktop themes with optional notification-area support

![screenshot](https://github.com/leftstack/hash_silo/blob/main/hash_silo_ui.png)

## How It Works

```text
Target hash or file + candidate password
                  |
                  v
        Selected Hashcat mode
                  |
                  v
       Local verification engine
                  |
                  v
       Match result + profile history
```

Hash Silo parses the selected target format, applies that mode's password transformations & cryptographic operations, and compares the result locally. For supported modes it can also generate a fresh, correctly formatted target from a password.

## Get Hash Silo

Download the latest package for your platform from the repository's Releases page, extract it, and launch Hash Silo.

Packages are available for:

- Windows 64-bit
- Linux 64-bit

SQLCipher and its cryptographic dependencies are bundled with release builds, so end users do not need to install a separate database or crypto library.

## Verify a Password

1. Select the expected hash type, or paste a target and use **Detect** to find compatible types.
2. Paste the target hash or select a target file when the mode uses one.
3. Enter a username when the selected format requires it.
4. Enter a candidate password and select **Try Password**.
5. Review the result and password-attempt history.

Hash-type detection is structural. Some target shapes are shared by multiple modes, so Hash Silo reports every compatible candidate rather than guessing when a result is ambiguous.

## Generate a Target

1. Select a hash type that supports generation.
2. Enter the password and any required username.
3. Select **Generate Hash**.
4. Copy the generated Hashcat-compatible target.

Fresh salts, initialization vectors, and other required material are generated automatically for formats that use them.

## Profiles and Data

Profiles keep separate hash types, targets, & attempted-password history. A default profile is created on first launch, and additional profiles can be created, renamed, selected, and deleted from the profile manager.

Without Portable Mode, the database is stored in the normal per-user application-data location:

- Windows: `%LOCALAPPDATA%\LeftStack\Hash Silo\hash_silo.sqlite3`
- Linux: `$XDG_DATA_HOME/LeftStack/Hash Silo/hash_silo.sqlite3`, or `~/.local/share/LeftStack/Hash Silo/hash_silo.sqlite3`
- macOS: `~/Library/Application Support/LeftStack/Hash Silo/hash_silo.sqlite3` (when & frankly if a native MacOS build becomes available)

History contains the actual attempted passwords. Treat the database & exported history files as sensitive data. Clearing history & deleting profiles are permanent operations.

## Portable Mode

Create an empty file named `.portable` beside the Hash Silo executable before launching it. Hash Silo will store `hash_silo.sqlite3` in that same directory and show `[Portable Mode]` in the window title.

Portable Mode changes where data is stored; it does not encrypt the database by itself.

## Database Security

Database Security in Settings can convert the local database to an encrypted SQLCipher database. Once protected, the password is required when Hash Silo starts or after the database is locked.

The database password is never stored & cannot be recovered. Database encryption protects closed database files at rest, but it does not protect information displayed by an unlocked session, copied to the clipboard, exported to a file, or observed by software running as the same user.

## Security Notes

- Hash Silo performs its work locally and does not access networks.
- The **Hide passwords** option masks history on screen only; the original values remain in the active profile and are still used by copy actions.
- Protect the database if attempted passwords or targets must be encrypted while Hash Silo is not running.
- Store exported password lists carefully & remove them when they are no longer needed.
- Use Hash Silo only with your own items/systems or those you are authorized to test.

## Notice

Hash Silo is an independent project and is not affiliated with or endorsed by the Hashcat project. 

---

*Note: This repository contains binary releases only.*
