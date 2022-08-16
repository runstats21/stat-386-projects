# Stat386 Projects Blog

This the repo for the Stat386 blog projects.

## Steps for creating a new post.  

1. Create a new file in the "_posts" folder called 'YYYY-MM-DD-post-name.md', where YYYY is the year (2022), MM numeric month (01-12), and DD is the numeric day of the month (01-31).  The "post-name" is a short name for the new post with - between words.  You must use this name convention for all new posts.  

2.  Make the YML heading.  All pages in the site need to start with a YML heading.  For posts you should use
```
---
layout: post
title:  "Post Name"
date:   YYYY-MM-DD
description: Short yet informative description
image: /assets/images/blog-image.jpg
---
```
Note that the layout should stay as "post", but all the other fields you need to update with the information for your particular blog post.  The blog image should be a .jpg or .png file that you should add to the folder "assets/images".  Don't make it too large or the page will take longer to load (500-800 KB is a good size)

3.  Write the body of the blog using markdown.  

* Use `#` for section headings 
```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
```

* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
* [Markdown Guide](https://www.markdownguide.org/cheat-sheet/)
* [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)