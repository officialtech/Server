# Symlink


### Update a Symlink
1. Remove old symlink and create new one:

```bash
# Remove old symlink
rm /path/to/symlink

# Create new symlink
ln -s /path/to/actual/file /path/to/symlink

# Verify
ls -la /path/to/symlink
```

2. Or update it in one command:

```bash
ln -sfn /path/to/new/target /path/to/symlink
```

- |->| `ln`	Link command (creates links)
- |->| `-s`	Create a symbolic link (shortcut)
- |->| `-f`	Force — overwrite if symlink already exists
- |->| `-n`	No dereference — don't follow existing symlinks
- |->| `/path/to/new/target`	What the symlink should point to (actual file/folder)
- |->| `/path/to/symlink`	Where to create the symlink (the shortcut)


---

### Real-World Example

```bash
ln -sfn /usr/local/node-v16/bin/node /usr/bin/node

# This creates a symlink `/usr/bin/node` that points to the actual `Node.js` binary at `/usr/local/node-v16/bin/node`

# Now you can use:

node --version
# Instead of: `/usr/local/node-v16/bin/node --version`
```

---

### Breaking Down the Flags

1. `-s` (Symbolic Link)
- Creates a shortcut reference, not a copy.

```bash
# With -s (symlink)
ln -s /actual/file /shortcut
# /shortcut points TO /actual/file (doesn't copy it)

# Without -s (hard link)
ln /actual/file /copy
# /copy is a separate copy (takes up space)
```

2. `-f` (Force)
- If symlink already exists, overwrite it without asking.

```bash
# Without -f: Error if symlink already exists
ln -s /new/target /symlink
# ln: /symlink: File exists

# With -f: Overwrites silently
ln -sf /new/target /symlink
# (works fine, even if /symlink existed)
```

3. `-n` (No Dereference)
- Don't follow existing symlinks when creating a new one.

```bash
# Without -n: Might follow old symlink
ln -sf /new/target /symlink

# With -n: Definitely replaces the symlink itself
ln -sfn /new/target /symlink
```



