# Interlude: Files and Directories

Persistent storage

OS must take extra care with storage device

###### Crux: How to manage a persistent device?


## Files and directories

Key abstractions:
1. file - linear array of bytes (r/w)
2. directory - list of pair(name, inode)

("foo", 10)

Directory within directory -> dir. tree

## Unlink()

## Creating files

```c

int fd = open("foo", O_CREAT|O_WRONLY|O_TRUNC, S_IRUSR|S_IWUSR);

```
open() - returns file descriptor - private per process
capability
strace

## Reading and writing files

Three files open:
1. STDIN - 0
2. STDOUT - 1
3. STDERR - 2


## Writing immediately with fsync()

File system buffers data for later writing (5 - 30 sec)

Directory should also be fsynced


## Renaming files

mv
rename()
mmap - access persistent data in files (alternative way)


## Getting information about files

Metadata

stat(), fstat()

## Removing files

rm
unlink()

## Making directories

mkdir()

.
..

ls -a

rm -rf * - dangerous

## Reading directories

opendir()
readdir()
closedir()

```c
int main(int argc, char **argv) {
	DIR *dp = opendir(".");
	assert(dp != NULL);
	struct dirent *d;
	while((d = readdir(dp)) != NULL) {

		printf("%lu %s\n", (unsigned long) d->d_ino, d->d_name);
	}
	closedir(dp);
	return 0;
}
```

## Deleting directories

rmdir: directory must be empty

## Hard links

ln file file2

ls -i file file2

When reference count == 0, inode is freed, data blocks freed, the file 
is therefore deleted legitimately.

## Symbolic links

ln -s file file2 
not regular file, but symbolic link

lrwxrwxr-x

the 'l' indicates it is a soft link

dangling reference possible

## Permission bits and access control lists

- regular file
d directory
l symbolic link

Owner Group User/other
 rwx   r-x    r-x

chmod - change file mode

access control list


## Making and mounting a file system

mkfs

file system type ext3

mount() - make fs accessible


- A file is an array of bytes which can be created, read, written, and
deleted. It has a low-level name (i.e., a number) that refers to it
uniquely. The low-level name is often called an i-number.

- A directory is a collection of tuples, each of which contains a
human-readable name and low-level name to which it maps. Each
entry refers either to another directory or to a file. Each directory
also has a low-level name (i-number) itself. A directory always has
two special entries: the . entry, which refers to itself, and the ..
entry, which refers to its parent.

- A directory tree or directory hierarchy organizes all files and direc-
tories into a large tree, starting at the root.

- To access a file, a process must use a system call (usually, open())
to request permission from the operating system. If permission is
granted, the OS returns a file descriptor, which can then be used
for read or write access, as permissions and intent allow.

- Each file descriptor is a private, per-process entity, which refers to
an entry in the open file table. The entry therein tracks which file
this access refers to, the current offset of the file (i.e., which part
of the file the next read or write will access), and other relevant
information.

- Calls to read() and write() naturally update the current offset;
otherwise, processes can use lseek() to change its value, enabling
random access to different parts of the file.

- To force updates to persistent media, a process must use fsync()
or related calls. However, doing so correctly while maintaining
high performance is challenging [P+14], so think carefully when
doing so.

- To have multiple human-readable names in the file system refer to
the same underlying file, use hard links or symbolic links. Each
is useful in different circumstances, so consider their strengths and
weaknesses before usage. And remember, deleting a file is just per-
forming that one last unlink() of it from the directory hierarchy.

- Most file systems have mechanisms to enable and disable sharing.
A rudimentary form of such controls are provided by permissions
bits; more sophisticated access control lists allow for more precise
control over exactly who can access and manipulate information.


