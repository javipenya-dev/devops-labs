# Lab 04: Links and Permissions

## 🔗 Links (Enlaces)
- **Soft Link (`ln -s`):** A shortcut. Used in DevOps for versioning (e.g., `current` pointing to `app_v1` or `app_v2`). If the original is deleted, the link breaks.
- **Hard Link (`ln`):** A second name for the same physical file (same inode). Used for space-efficient backups. If the original is deleted, the data remains accessible via the hard link.

## 🔐 Permissions (`chmod`)
Numeric system: Read (4) + Write (2) + Execute (1). Order: Owner, Group, Others.
- `chmod 755`: Standard for scripts and directories (Everyone can execute/read, only owner can write).
- `chmod 700`: Private (Only owner has total control).
- `chmod 644`: Standard for regular files (Owner writes, everyone reads).
- `chmod 444`: Read-only for everyone (Even the owner cannot modify it without changing permissions back).
