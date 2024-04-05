---
title: "Symlink in git"
author: "Jeffery Jiang"
tags: ["git"]
date: "2022-11-09"
---

## What is symlink

A symlink, also known as a symbolic link or soft link, is a special type of file that acts like a shortcut to another file or directory on your computer. It's similar to a shortcut you might create on your desktop.

Here's how it works:

- The symlink itself doesn't contain the actual data.
- Instead, it stores the location (path) of the target file or directory that it points to.
- When you try to access the symlink, your operating system follows the path stored in the - symlink and opens the target file or directory.

here is how symlink defined in bash

```bash
// creating
ln -s /path/to/documents/important important_docs
// using
ls important_docs
```

There are several benefits to using symlinks:

- **Organization**: You can organize your files and directories more logically by creating symlinks in convenient locations, even if the actual files are stored elsewhere.
- **Flexibility**: Symlinks can be easily recreated or pointed to different targets, providing flexibility in your file structure.
- **Saves space**: Since symlinks don't store the actual data, they don't take up additional storage space.

However, there are also some things to keep in mind about symlinks:

- **Broken symlinks**: If the target file or directory is moved or deleted, the symlink becomes broken and won't work properly.
- **Not all programs recognize symlinks**: Some programs might not interpret symlinks correctly and may try to access the symlink file itself instead of the target.


## Symlink in git

Imagine you have a project with a large image file named `banner.jpg` stored in a dedicated folder for assets,  `assets/images`. You also have a separate markdown file, `readme.md`, in the root directory of your project that needs to reference the banner image

### Using a symlink

1. **Create the Symlink**:
    - Navigate to the root directory of your Git repository using your terminal.
    - Run the following command to create a symlink named banner.jpg that points to the actual `assets/images/banner.jpg` file:
    
    ```bash
    ln -s assets/images/banner.jpg banner.jpg
    ```
    This creates a symlink named `banner.jpg` in your root directory, but it essentially acts as a shortcut to the original image file.

2. **Using the Symlink:**
    Edit your readme.md file and reference the image using the symlink:

    ```text
    # My Project
    [![Banner Image](banner.jpg)](path/to/website)
    ```
3. **Git Tracking:**

    Since the symlink `(banner.jpg)` stores the path to the target file `(assets/images/banner.jpg)`, Git will track the symlink itself as part of your repository.
    When you commit changes and push to remote repository (like GitHub), the symlink information will be included.

4. **git config core.symlink**
    Let's say you have a repository with a symbolic link named `my_link` pointing to `some_file.txt`:

    ```rust
    my_repository/
    ├── my_link -> some_file.txt
    └── some_file.txt
    ```
    - If `core.symlinks` is set to true, Git will preserve the symbolic link when checking out files. So, when you clone or checkout this repository, my_link will be created as a symbolic link pointing to `some_file.txt`.
    - If `core.symlinks` is set to false, Git will create plain text files with the link target path as content instead of symbolic links. So, in the same scenario as above, when you clone or checkout the repository with core.symlinks set to false, `my_link` will be created as a plain text file containing the path `some_file.txt`

