# Crash consistency: FSCK & Journalling

File system data structures must persist.

### How to update disk despite crashes

File system checker

Journalling

inode, bitmap, data write

## File system checker fsck

- Superblock
- Free blocks
- Inode state
- Inode links
- Dublicates
- Bad blocks
- Directory checks

slow

## Journalling

write-ahead logging