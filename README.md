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
author: Your name
description: Short yet informative description
image: /assets/images/blog-image.jpg
---
```
Note that the layout should stay as "post", but all the other fields you need to update with the information for your particular blog post.  The blog image should be a .jpg or .png file that you should add to the folder "assets/images".  Don't make it too large or the page will take longer to load (500-800 KB is a good size).  The file path should be okay to leave as "/assets/images/" in the header area.  

3.  Write the body of the blog using markdown.  For more information about writing with markdown, see the following 
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
* [Markdown Guide](https://www.markdownguide.org/cheat-sheet/)
* [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)

4.  Images for the blog will generally but put into the 'assets/images' folder.  You can aslo create a subfolder for each blog post if you'd like to keep your figures organized.  I've found that in the body of the post, it works better to use a url pointing to the figure's location.  In order to find the appropriate url, navigate to the figure in the repository and find the "download" url.  The correct url will typically have the work "raw" either at the beginning or as `/raw/` in the middle somewhere. For example:

```
![Figure](https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg)

OR

![Figure](https://github.com/esnt/stat386-projects/raw/main/assets/images/image5.jpg)
```

![Figure](https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg)

There isn't a good way to resize images with markdown, but you can use `html` directly to resize an image:

`<img src="https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg", alt="", style=width:400px;"/>`

(Width is 400 pixels)
<img src="https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg" alt="" style="width:400px;"/>



`<img src="https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg", alt="", style=width:100px;"/>`

(Width is 100 pixels)
<img src="https://raw.githubusercontent.com/esnt/stat386-projects/main/assets/images/image5.jpg" alt="" style="width:100px;"/>

This repository is cloned from [github.com/esnt/stat386-projects](https://github.com/esnt/stat386-projects) which was originally built by following [these excellent youtube tutorials](https://www.youtube.com/playlist?list=PLWzwUIYZpnJuT0sH4BN56P5oWTdHJiTNq) by Bill Raymond.
