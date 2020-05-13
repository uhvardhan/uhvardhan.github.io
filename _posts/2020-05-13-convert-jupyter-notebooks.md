---
layout: post
title: How to post Jupyter Notebooks to your Jekyll site?
subtitle: Convert your jupyter notebooks into blog posts
categories: tutorials
---

## Instructions:

Step 1: Run the following command in terminal to convert a file named
`test.ipynb` from `.ipynb` to `.md` suitable for your Jekyll site. Remember to
`cd` to the directory that includes the file you intend to convert.

```bash
jupyter nbconvert --to markdown test.ipynb
```

This command will create two new items:
- `test.md` is a file containing the markdown for your blog post
- `test_files` is a folder containing all the images for your blog post

Step 2: Move the `test.md` file to your blog's `_posts` folder. Rename the
file to include the date and title for your post such as

```bash
2020-05-13-convert-jupyter-notebooks.md
```

Make sure the first few lines of `.md` contain the appropriate front matter
(YAML block in Jekyll parlance). Change any image links to point to your blog's
image folder.

Step 3: Move the `test_files` folder to your blog's `assests/img` folder.

Step 4: Add these files to the git repository and commit. Push the repo.

Congratulations! You have updated your site!

### References:

1. [Adam Blomberg Blog](https://blomadam.github.io/tutorials/2017/04/09/ipynb-to-Jekyll-Post-tools.html)
