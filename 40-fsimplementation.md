# File system implementation

Simplified version of unix fs

1. On-disk structure
2. Access methods
3. Policies

- How to build? 
- What structures needed?
- What do they need to track?
- How are they accessed?

Two aspects:
1. Data structures
2. Access methods

## Organization

Disk into blocks 4KB size

- Superblock
- Data bitmap
- Inode bitmap
- Array of inodes
- Array of data

Inode - structure that holds metadata

When inodes are fetched, the whole 512 bytes is fetched. Disk consist of sectors.

How inodes refer to where data blocks are?

- Direct pointers
- Indirect pointers
- Extents: pointer + length (contiguous?)


## Directory organization

list of (entryname, inode) pairs

## Free space management

FS must track free and not free data blocks and inodes
The bitmaps 

preallocation, performance

## Access paths: reading and writing

### Reading a file from disk

Traverse to look for inodes
Root inode is 2
bitmaps are not accessed on reads: inode whether points or not.
closing = deallocating file descriptor

### Writing a file to disk

Allocate a block unless overwritten.
Which block to allocate to the file? update bitmap, inode

I/O:
1. read the data bitmap
2. write the bitmap
3. read the inode
4. write the inode
5. write the block itself

Creating a file causes more I/Os
Directory has to allocate space

### How to reduce file system I/O costs?

## Caching and buffering

System memory DRAM to cache important blocks

Fixed size cache allocated at boot time 10%

Dynamic partitioning
Unified page cache
Subsequent file opens of the same file/dir hit in the cache and thus no I/O is needed.

Write buffering, delayed write to disk, cache

Trade offs

