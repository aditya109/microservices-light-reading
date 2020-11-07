<main>Git Architecture</main>

# Introduction

The regular cycle of Git : `checkout > modify > commit`.

## Git as a Folder

When you run  `git init` in a folder, Git creates the `.git` directory. 

```powershell
mkdir git-playground && cd git-playground
git init
ls .git
```

The output is the following:

```
    Directory: D:\Projects\git-playground\.git


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        02-11-2020  10:21 AM                hooks
d-----        02-11-2020  10:21 AM                info
d-----        02-11-2020  10:21 AM                objects
d-----        02-11-2020  10:21 AM                refs
-a----        02-11-2020  10:21 AM            130 config
-a----        02-11-2020  10:21 AM             73 description
-a----        02-11-2020  10:21 AM             23 HEAD
```

This is where Git stores all your commits and other relevant information to manipulate these commits.

When you clone a repository:

- Git clones this single directory into your folder
- Creates remote-tracking branches for each branch in the cloned repository
- Creates and checks out an initial branch that is specified by the HEAD file.

> Take-a-way:
>
> "cloning a repository is essentially just copying `.git` directory from the other location."

## Git as a Database

Git is a simple key-value data store, where a value is put into the repository and a key is retrieved by which the corresponding value can be accessed.

### Writing to the database: hash-object, Variables

The command that puts values into the database is `hash-object` and it returns a 40-character checksum hash that will be used as a key. 

The command creates a plain object in Git repository that is called a `blob`. 

Let's create a simple string `f1 content` into the database. Open the `.git` directory using **Git Bash** and type the following

```bash
$ F1CONTENT_BLOB_HASH=$(echo 'f1 content' | git hash-object -w --stdin )
$ echo $F1CONTENT_BLOB_HASH
a1deaae8f9ac984a5bfd0e8eecfbafaf4a90a3d0
```

Explanation:

1. The `echo` command outputs the `f1 content` string.
2. By using the pipe operator `|` we redirect, or "pipe", the output to the `git hash-object` command.
3. The parameter `-w` passed to the `hash-object` command tells it to store the object; otherwise, the command simply tells you what the key would be.
4. The parameter `--stdin` tells the command to read the content from `stdin`.
5. If you don’t specify this, `hash-object` expects a file path at the end. As mentioned earlier, the `git hash-object` command returns a hash that I then save into the `F1CONTENT_BLOB_HASH` variable.

### Reading from the database: cat-file

To read a value by key from the database we can use the `cat-file` command with the `-p` option. 

```bash
$ git cat-file -p $F1CONTENT_BLOB_HASH
f1 content
```



We can go into `.git/objects` and you will see the folder created by Git with the name `a1` which is the first two letters of the hash key:

```bash
$ ls -1 objects
4b/
a1/
info/
pack/
```

This is the way Git usually stores objects — one folder per one blob.

However, Git can also merge multiple blobs into one file to generate pack files and the `pack` directory you see above is where these files are stored.

Git keeps information related to these pack objects in the `info` directory.

Git generates hashes for blobs based on the blob contents. So objects in Git are immutable because changing the contents would change the hash.

Let’s write another string `f2 content` into the repository:

```bash
$ F2CONTENT_BLOB_HASH=$( \
     echo 'f2 content' | git hash-object -w --stdin )
$ ls -1 .git/objects/
4b/
9b/ 
a1/ 
info/ 
pack/     
```

As expected you can see that the `\.git\objects` folder now contains two records `9b/` and `a1/`.

### Tree as an integral part

Currently we have two blobs in our repository:

```
F1CONTENT_BLOB_HASH -> 'f1 content'
F2CONTENT_BLOB_HASH -> 'f2 content'
```

We need a way to somehow group them together and also associate each blob with a filename. And this where a tree comes into play.

A tree can be created using `git mktree` command with the following syntax for each file/blob association:

```bash
[file-mode object-type object-hash file-name]
```

We will use the mode `100644` that defines a blob as a regular file which can be read and written by the user. 

Those permissions are used when checking out files to a working directory to set permissions on files\directories corresponding to the trees entries.

So to associate two blobs with two files we'll do the following:

```bash
INITIAL_TREE_HASH=$( \
    printf '%s %s %s\t%s\n' \
      100644 blob $F1CONTENT_BLOB_HASH f1.txt \
      100644 blob $F2CONTENT_BLOB_HASH f2.txt |
    git mktree )
```

Just as with `hash-object`, the `mktree` command returns a hash key for the created tree object:

```bash
echo $INITIAL_TREE_HASH
e05d9daa03229f7a7f6456d3d091d0e685e6a9db
```

So here is what we have now:

$INITIAL_TREE_HASH

- **f1 content** $F1CONTENT_BLOB_HASH
- **f2 content** $F2CONTENT_BLOB_HASH

```
Folder PATH listing
Volume serial number is C849-E654
D:.
├───4b
├───9b
├───a1
├───e0
├───info
└───pack
```

When using `mktree` we can specify another tree object as a parameter instead of a blob. That tree will be associated with the directory instead of a regular file. 

###  Index is a place where trees are assembled





