# How to update and manage the KITAB website

In the following you find an explanation of the website set-up and some step-by-step guides for updating and adding content to the KITAB website. It is recommended that you consult this document before making any changes to file structures, adding new pages or making changes to existing pages. 

You will find here sections containing guides on the following:
- [The structure and format of the website](#about-the-structure-and-format-of-the-website).
- [Making changes to existing pages](#making-changes-to-existing-pages).
- [Adding new pages to the website](#adding-new-pages).
- [Style guides for particular website features](#specific-_pages-style-guides).
- [Using the automatic blog uploading procedure](#adding-blogs-automatically-from-docx-format).
- [Manually adding blogs to the website](#manually-adding-blogs-to-the-website). 

## Resources:
- Minimal mistakes [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).
- [Guide](https://github.github.com/gfm/) to GitHub flavoured markdown (GFM).
- [Guide](https://shopify.github.io/liquid/) to Liquid - the programming language used by Jekyll to produce html. You may need this to add theme-specific features or stable internal links.
- [Guide]() to running Jekyll commands
- [Guide]() to installing Jekyll through Windows Subsystem for Linux (WSL)

Note to Windows Ubuntu WSL users: When the guide below states 'cd into the directory' in you most remember to prefix the directory with '/mnt/' (the directory that specifies your Windows directories). For example:

```
cd /mnt/c/Users/mathe/Documents/
```

Would navigate to the Documents directory for the User 'mathe'.

You should also note that tab completion in Ubuntu is case sensitive ('U' + tab will autocomplete to 'Users', where 'u' + tab will not autocomplete and give an error sound).


## Dependencies

### GitHub
If you plan to run the blog post upload script or make any changes locally, then a familiarity with basic GitHub is essential. Windows users should use Git Bash, Linux or Mac users can use the git functionality in their command line.

To get the repository locally, run the following command:
- git clone https://github.com/kitab-project-org/kitab-project-org.github.io.git

Before making any updates, make sure to run:
- 'git pull origin master' 
This will fetch any changes that have been made by any users or on the remote before you make your own changes. This is essential for avoiding merge conflicts.

If you make any updates, take the following approach:
1. Run 
        ```
        git add .
        ```
1. Run 
        ```
        git commit -m "**easy to identify commit message**"
        ```
1. Run
        ```
        git push origin master
        ```
1. Wait a short while to allow GitPages to process your changes and then go to the website to see your changes take effect. 

*WARNING: once you push changes to the main repository they will be added to the website. Make sure that you are happy with your changes before committing them to the main repository (this also applies if you make changes online). Once a change has been pushed to the remote (or committed in the remote - i.e. committed on the GitHub website), you will need to change it back manually and create another commit, to revert (or you will need to reset to an earlier commit - this is not recommended).*

Given the above risks, it is recommended that you check big changes by running Jekyll locally before commiting your changes to the remote.


### Jekyll
Small changes to the website or blog uploads can be done without needed to install and run Jekyll locally. If you plan to make large changes to the website or add new pages, it is recommended that you install Jeykll on your local machine. This will allow you to test the website prior to uploading your changes to GitHub. The following steps. A good guide to Jekyll is [here](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages) (**Note:** This guide uses a different route to the WSL for installing Jekyll on Windows - we do not recommend Windows users follow the route specified in this guide - the blog post is intended as a guide to install and running Jekyll once WSL Ubuntu is installed).

#### Windows vs Mac and Linux
The recommended route is to run Jekyll throughout Windows Subsystem for Linux, using Ubuntu. You will need to Activate WSL and install Ubuntu, on this (check [this](https://ubuntu.com/wsl) guide). Mac and Linux users can use their usual command line.

#### Install Jekyll and get gems for our website
1. Open Ubuntu WSL in Windows or command line in Mac or Linux
1. run
        ```
        sudo gem install jekyll
        ```
1. run
        ```
        sudo gem install jekyll bundler
        ```
1. 'cd' into the KITAB website directory (the GitHub repository that you downloaded in in the step above)
1. run 
       ```
       bundle update
       ```
       - this uses the website's specs to get the appropriate gems and versions
1. At this stage (or the following stage) you may find that you get an error telling you that some of your gems are the wrong version. To fix this run gem install 'gem -v version' (where you give the name of the gem specified in the error and the version specified, e.g. 'gem install kramdown -v 1.1.0'). To troubleshoot these issues it is recommend you search for the error in google and follow a stack exchange thread - almost all of the errors you will encounter will be resolved there.
1. to check everything is installed correctly run 'bundle exec jekyll serve'. This will serve the website locally.
1. Navigate to the local server address given in the command line to see the local instance of the website.

#### Checking your changes by running Jekyll locally
Whenever you make any changes to the website, you can use the following steps to check how those updates look in your browser before pushing them to the main website.
1. Open WSL Ubuntu in Windows or command line in Mac or Ubuntu
1. 'cd' into the directory containing the website files
1. run
       ```
       bundle exec jekyll serve
       ```
1. Navigate to the local server in the browser to look at your changes.
1. Use 'ctrl' + 'c' to end the local server process (it is recommended that you do this before making further changes).

**A note on making updates while the server is running:** Jekyll allows you to make changes while the server is running and to see those changes locally. When you make a change, it will automatically re-run the build process and push the changes to the server. In some cases, it seems that this process errors and will hang (the command line will freeze up and you won't be able to end the local server process). If you find this happens, quit and reopen Ubuntu/the command line, and we recommend you use the command 'bundle exec jekyll serve --no-watch' to run the server in future. If you do this the website will not update as you make changes, but it will be more stable. In this case you will need to end the server and re-run 'bundle exec jekyll serve --no-watch' every time that you want to see changes.

#### Common Jekyll errors and solutions (to be updated as errors are reported)

1. **Issue:** Website fails to build or builds incorrectly (often styling disappears), console gives a failure to parse yml frontmatter error.
   
   **Solution:** Check the files specified in the console error. If they are pages, check the header front matter for errors (typically a failure to close quotation marks, or add quotation marks causes this error). If it is in navigation.yml or authors.yml, check the yml file for missing or unclosed quotation marks, look for missing indentation.

1. **Issue:** Console states that it failed to parse Liquid
   
   **Solution:** Go to the file(s) specified in the console error. Look for Liquid tags that are incorrectly formatted (for example missing '%' or '{' '}' marks), or for spelling errors in tags that mean that they cannot be recognised.

### Python
If you plan to run the blog docx conversion script on your local machine (for details on how to see below), you will need to install Python 3.6 or later on your local machine and pip to install the relevant packages. Use pip install to install any dependencies (open your Python-enabled command prompt, cd into the 'conversion_script' folder and use the command 'pip install -r requirements.txt'). For the exact dependencies see the requirements.txt file in the 'conversion_script' folder of the repository.

## About the structure and format of the website

The KITAB website is built from the Jekyll theme minimal-mistakes with some minimal added html for the home page. It is hosted using GitHub pages. Updates can be made directly to the markdown within this GitHub repository, or by cloning and editing the files locally.

For updating the website, there are four important folders:
1. _data
1. _pages
1. _posts
1. images

You may also need to make changes to the following files:
1. index.html
1. config.yml

You are unlikely to need to make any modifications to any other folders in the repository. Some of the folders contain files that are essential for Jekyll to build the website and changes are likely to cause **catastrophic** damage to the website. **Approach with caution.**

### _data

This folder contains three files, two of which are important for our use:
1. authors.yml
1. navigation.yml

authors.yml contains all of the data for the authors of blog posts. If there is a new author, they will need to be added to this yml. All fields for each author do not need to filled out. For best functionality, the minimum needed is: name, avatar, and bio. 

The contents of all fields should be given as quotation marks, bios should be around 30 words or less. The author id separated by the underscore (e.g. sarah_savant) needs to match the author given in the header matter of the blog post.

navigation.yml provides the structure of the website. The addresses used in this file should be match those in the header matter for relevant pages. The navigation is set up to provide sidebar navigation for all pages of the website. For guidance on how to use the navigation file, see the Minimal Mistakes [documentation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/).

Changes to this file should only be made if a new page is added, or if a title needs to be changed in the top navigation or any of the sidebar navigation. Never change the field id 'main', and try to avoid changing other field ids (e.g. about, corpus) or url fields. Changes to these will cause the website to break if corresponding changes are not made in the headers of relevant pages. 

### _pages

This folder contains all of the markdown files for the pages of the website. The folder structure is present to aid your navigation, but changes to this structure will not make any impact on the website itself. If you want to change the content of any pages of the website, you will be making the changes to the markdown pages in this folder. If you want to add a new page to the website, you will be adding that page to this folder (or potentially one of the subfolders).

### _posts

This is where all of the blog posts for the website are stored in markdown format. When Jekyll builds the website, it looks for new blogs in this folder and uploads them accordingly. If you use a script to convert and upload a blog, then it will automatically be added to this folder. Otherwise, you will be adding the markdown file for the blog post to this folder.

### images

Any images on the website are stored here. **The structure of this folder matters - any changes to organisation will lead to broken links and missing images. Only add images to this folder, do not change the structure.**

### index.html

This contains the content for the homepage of the website. Although it is an html file, Jekyll automatically converts the content of this file from markdown. You will find that this page contains markdown, Liquid and html. Specific guidance will be provided below on how to making changes to the content of this page.

### config.yml

The file detailing the settings for the website. You are unlikely to need to make changes to this file. It controls matters such as: the name of the website, the type of commenting API that it uses, and the main theme template to use.

### A note on the theme colour customisation

This KITAB website uses a modified version of the 'air' skin. The skin is specified in the config file under 'minimal_mistakes_skin'. To add KITAB colours to the website, small changes have been made to:

```
_sass/minimal-mistakes/skins/_air.scss
```


In this file one field has been changed:

```
$primary-color: #2862a5 !default; 
```

This sets the primary-color to the KITAB logo blue. If the theme were to be reset to default, make sure to update this field in _air.scss and specify the 'air' skin in config.yml.

## Making changes to existing pages

There is presently no procedure for converting website pages from docx to markdown using a python script. This is due to the increased level of customisation available in the pages part of the website (for example, for the insertion of text boxes). 

It is recommended that you modify the pages directly in the markdown file. This can be done through two approaches (use the second for any major changes, to avoid pushing potential errors to the main website):

### Making changes online

1. Navigate to the relevant page under _pages in the online repository
1. Click the edit button for that page
1. Make the changes to the text
1. Add a clear and identifiable commit message and press commit
1. Your changes will shortly appear on the website

### Making changes locally

1. Open git Bash (in Windows), or open command line in Mac or Linux.
1. cd into the GitHub repository for the website.
1. run 'git pull origin master' (in Bash in windows, in command line in Mac or Linux) - this will get any new changes from remote repository.
1. Navigate to the repository in your computer file system and navigate to the '_pages' folder, find the markdown file related to the page you want to edit.
1. Open the file in a text editor that supports markdown (such as EditPad Pro).
1. Make the relevant changes and save them.
1. Go to Ubuntu (in Windows) or the command line (in Mac or Linux).
1. cd into the GitHub repository for the website
1. run 'bundle exec jekyll serve'
1. Open the browser and enter the address of the local server
1. Check that your changes have had the desired effect.

If you are happy with your changes in the browser, do the following:
1. Go to git Bash (in Windows) or command line in Mac or Linux
1. Run 
        ```
        git add .
        ```
1. Run 
        ```
        git commit -m "*clear and identifiable commit message*"
        ```
1. Run 
        ```
        git push origin master
        ```
1. Your changes will shortly appear on the main website.

## Adding new pages

It is recommended that you add new pages locally, although it is possible to create a new markdown file using the 'Add file' function within GitHub. Your changes will, however, be added to the live website as you commit them and so it will not be possible to preview your changes before they go live.

Take the following steps to add a new page:

1. Open git Bash (in Windows), or open command line in Mac or Linux.
1. cd into the GitHub repository for the website.
1. run 'git pull origin master' (in Bash in windows, in command line in Mac or Linux) - this will get any new changes from remote repository.
1. Open a text editor that supports markdown (such as EditPad Pro).
1. Create a new file and save it in the '_pages' folder of the directory - give it a clear name that relates to the content of the page and ensure that it has the '.md' extension.
1. Paste the header matter into the new file, and fill out the fields that you need
1. Add the content to the file and save it.
1. Go to navigation.yml in the '_data' folder of the respository and open it in a text editor (such as EditPad Pro).
1. Add the permalink you specified in the header into navigation.yml along with the desired title (in the place in the navigation that you would like the link to appear) - see further the [_data section](#_data) above.
1. Go to Ubuntu (in Windows) or the command line (in Mac or Linux).
1. cd into the GitHub repository for the website.
1. run 
        ```
        bundle exec jekyll serve
        ```
1. Open the browser and enter the address of the local server.
1. Check that page appears in the expected place in the navigation and that you're happy with the content.

If you are happy with your changes in the browser, do the following:
1. Go to git Bash (in Windows) or command line in Mac or Linux
1. Run 
        ```
        git add .
        ```
1. Run 
        ```
        git commit -m "*clear and identifiable commit message*"
        ```
1. Run 
        ```
        git push origin master
        ```
1. Your new page will shortly appear on the main website.

### Header matter

All pages must have header matter to function correctly within the website. The header matter specifies matters such as: the banner image that will appear on the page, the title of the page, the relative url address of the page, and specific content features (for an advanced example of header-specified feature, see the [section on feature rows below](#feature-rows). Guidance on the kinds of fields used in headers can be found in the theme [documentation](https://mmistakes.github.io/minimal-mistakes/docs/layouts/). Here we will explore the fields currently used in headers of the KITAB website.

Headers given at the top of the markdown file for each page and are separated from the main text of the webpage using '---' above and below the header. For example the header for 'about-corpus.md' looks like this:

```
---
excerpt:	""
header:
  overlay_image: /images/covers/banner_corpus.png
  overlay_filter: rgba(40, 99, 165, 0.45)
  caption: "A snapshot of KITAB's [corpus metadata search application](https://kitab-corpus-metadata.azurewebsites.net/)"
title:		"About the corpus"
layout:		single
sidebar:
  nav: "corpus"
permalink: /corpus/about
---
```

This is a selection of the fields available for the KITAB website - the following is a guide to fields that can be used in the header matter:

```yml
---
excerpt:	# Appears under the title in the banner
header:
  overlay_image: # Address of image that appears in  the banner
  overlay_filter: rgba(40, 99, 165, 0.45) # A filter can be applied to the image - the first three numbers are RGB coordinates and the fourth is the level of transparency to apply to the colour overlay.
  caption: # The caption for the image in the banner - it will appear in the bottom right of the banner.
title:		# Title of the page that appears in the banner
layout:		single # The layout to use (specifications [here](https://mmistakes.github.io/minimal-mistakes/docs/layouts/)) - nearly all pages use 'single'. The homepage and applications portal use a 'splash' layout. If the page is going to be an archive of blog posts, it will be specified here.
sidebar: # Options for what appears in the sidebar
  nav: "corpus" # If you would like to apply a sidebar navigation menu it should be specified here - the name refers to name given to the sidebar Navigation in navigation.yml
permalink: /corpus/about # The relative url that will be used for this page in the website structure - this is the address you refer to in navigation.yml or 'relative_url' Liquid tags
toc: # If this is specified as 'true', a table of contents (using the markdown headings) will appear in the right side
toc_sticky: # If this is specified as 'true', the table of contents will move downwards as the user scrolls down 
---
```

Below is an empty header than can be copied and pasted into new webpages (it is ok if you leave fields that you don't need empty, it will not cause an error). When copying this text, make sure to keep the indentation the same. The layout has been specified as 'single', as this is most likely to be the kind of page you will be adding. If you need a different page type, do not forget to change this field:

```yml
---
excerpt:	
header:
  overlay_image: 
  overlay_filter: rgba(40, 99, 165, 0.45)
  caption: 
title:		
layout:		single 
sidebar: 
  nav: 
permalink: 
toc: 
toc_sticky:  
---
```

## Specific _pages style guides

### Liquid tags
In existing pages you will come across Liquid tags. This are characterised by curly braces '{' '}' and sometimes have '%'. If in doubt, do not remove these tags, as it will impact upon the styling or the hyperlinking within the webpage. To investigate the functionality of specific tags, look at the Liquid docs (see 'Resources' above) or google the relevant tag to find out more.

### Internal links
For stability we recommend specifying internal links (that is links to other pages in the KITAB website) using Liquid functionality. This will ensure that the links remain the same if changes are made elsewhere in the website. Take the following code as a guide:

```
specific [data]({{ '/data' | relative_url }})
```

Here the usual markdown is used to specify the link. The link text is given between square brackets '[ ]', but rather than specifying the link, we put Liquid between the parenthesis '( )'. '/data' specifies the internal link used in the website, as given in navigation.yml and in the header 'permalink' field of 'about-data.md'. This internal link must be given between quotation marks. ' | relative_url then tells Liquid to treat the text as a relative url. 

### Text boxes 

Text boxes are used on the website for emphasis. These use built-in theme functionality, detailed [here](). This webpage specifies the colour profiles and what you will need to write to insert a color.

Use the following code block (which utilises markdown, liquid and html) to insert good text boxes.

```html
{% capture except_notice %} 
*ADD TEXT IN MARKDOWN HERE (this can include anything, including images or tables)*
{% endcapture %}

<div class="notice--warning">
{{ except_notice | markdownify }}
</div> 
```

The code above will output the text in markdown with a warning coloured box.

For examples, look at existing pages of the website, such as 'corpus_use.md'. We recommend that you compare the code in the markdown file to the end result to see how this works.

An example from the (corpus_use.md) file is, the end result can be viewed [here](https://kitab-project.org/corpus/use):

```html
{% capture except_notice %} 
**Please note:** There are certain exceptional author IDs that we use in the corpus in specific cases where an author cannot be identified, where the author's death date is unknown or where the author is still alive. Please find these variants in the table below. They are constantly being reviewed by the team, so check back here for updates.

  ID | Meaning
  --- | ---
  0001Quran.Mushaf (previously 0001KitabAllah.QuranKarim) | The Quran
  MuallifMajhul | Unknown author (date in URI will correspond to the period when we think the author was alive)
  1450 | Date used for authors who are still alive
  Pseudo- | An indication that a work attributed to the author, but the attribution is uncertain or disputed



{% endcapture %}


<div class="notice--warning">
{{ except_notice | markdownify }}
</div> 
```

### The homepage

The file for the homepage is found in the main repository folder as 'index.html'. To edit this file, you will need to right click on it and open it into a text editor (it will by default open in a browser, where you cannot edit it).

index.html uses a splash layout that is built into the theme. This allows you to add 'feature rows' to the page with pictures and links. Two of the boxes on this page are produced using custom html, rather than in-built splash 'feature rows' they are: the latest blog posts, the box for twitter and getting involved. It is unlikely that you will need to change the custom html, but it is documented here for potential future modifications.

#### Feature rows
The more standardised content of the homepage is added using feature rows. For a guide to splash layouts and feature rows, see [here](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#splash-page-layout). It is recommended that you add or remove content on the homepage using built-in feature rows, rather than hardcoding html. The two cases of html below are used because they have a specialist usage. This documentation is not very clear and so below is a step-by-step guide to updating or adding a feature row.

The content of feature rows is specified in the header of index.html. For example, the feature row containing the message from the PI, is specified in the header, as follows:

```yml
pi_message:
  - image_path: /images/kitab/all_team2.jpg
    url: "/about/"
    btn_label: "Read more"
    btn_class: "btn--primary"
    title: "A message from the PI"
    excerpt: >
       KITAB provides a digital tool-box and a forum for discussions about Arabic texts. We wish to empower users to explore Arabic texts in completely new ways and to expand the frontiers of knowledge about one of the world's largest and most complex textual traditions.
```

Any change to content is therefore made in this header matter. For example, if you wanted to change the text of the feature row, you would change the text under 'excerpt'. If you wanted to add another feature row, then you would add more of the same fields to the header. For example, if you wanted to add another row about events, you might add to the header:

```yml
events:
  - image_path: /images/kitab/event_image.jpg
    url: "/events/"
    btn_label: "Events"
    btn_class: "btn--primary"
    title: "A message from the PI"
    excerpt: 'See about our latest events'
```

Once the feature row has been specified in the header, you can add it into the main body of the text in the position that you wanted to add the feature row. For example, if we wanted to add the features rows above one after the other, one with the image on the right and the other with the image on the left, we would add to the main body of the text:

```
{% include feature_row id="pi_message" type="right" %}
{% include feature_row id="events" type="left" %}
``` 

#### Our latest blogs - code block

The code block for our latest blogs is identified using the following comment in the code:

```html
<!Code block for the latest blogs - do not change!>
```


This code block uses liquid and html to fetch the latest blogs and thumbnails for them, all wrapped in a "feature__wrapper". 

##### The html code
The classes used in this code block are taken directly from the minimal mistakes theme. They are typically used for grid post archives on the website, and here the in-built classes have been repurposed to place a grid on the webpage

Within the "div" for the "feature__wrapper", each blog post appears as a "grid__item", as in the example below shows:

```html
<div class = "grid__item">
     <article class = "archive__item">
      
      {% assign latest_post = site.posts[0]%}
      <div class = "archive__item-teaser">
      {% if latest_post.image %}
      <img src = {{ latest_post.image }} </img>
      {% else %}
      <img src = "/images/kitab/mesa.jpg" > </img>
      {% endif %}
      </div>
      <h2 class = "archive__item-title no_toc">{{ latest_post.title | truncate: 50 }} </h2> <a href="{{ latest_post.url }}">read more</a></b>
      
      
      
      </article>
      
      
</div>
```

**Note:** This grid on the homepage contains 4 items. This is the maximum that the grid feature will hold on one row. If more grid items are added, a new row will be created. It is not recommended that you add more items to this, or change this code at all. You are most likely to change the default images (found in the Liquid, explained below, and in the 'Read more blogs' item (the final item in the grid).

##### The Liquid code explained
Each div is populated using liquid as follows:

First we set a variable for the most recent post (that is the post at index position 0):

```liquid
{% assign latest_post = site.posts[0]%}
```

The Liquid to set the variable for the second most-recent post would, therefore be:

```liquid
{% assign latest_post = site.posts[1]%}
```

Then we extract data about the blog post specified in the variable to populate the html. First we check if the blog post has a thumbnail image:

```liquid
{% if latest_post.image %}
```

If it does, we use that image as our thumbnail in the layout:

```html
<img src = {{ latest_post.image }} </img>
```

Otherwise we use a default image and then close the if statement:

```liquid
{% else %}
<img src = "/images/kitab/mesa.jpg" > </img>
{% endif %}
```

If you wanted to change the default thumbnail image, you would change the image address between the quotation marks.

Once we've got the image, we use Liquid to get the blog title, we then only take the first 50 characters of that title (using truncate), and use it as a hyperlink to link to the url of the blog:

```
<h2 class = "archive__item-title no_toc">{{ latest_post.title | truncate: 50 }} </h2> <a href="{{ latest_post.url }}">read more</a></b>
```

#### The twitter embed and sharing code block

The code block for the twitter embed and sharing links is indicated with the following comment:

```html
<!Code block for the twitter embed and sharing - do not change!>
```

As with the blog posts, all the items in this section are wrapped in a "feature__wrapper" div. However, in this case all the items are wrapped as a left-styled feature item "feature__item--left". Each item is then coded as an "archive__item", and its associated classes (as with the blog posts below).

The following is a guide for changing content:

The twitter embed is as follows: 
```html
<a class="twitter-timeline" data-width="600" data-height="500" data-theme="light" href="https://twitter.com/sarahsavant1?ref_src=twsrc%5Etfw">Tweets by sarahsavant1</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
```

To change out the twitter embed, swap out the entirety of the above code for the new embed code provided by twitter (do not change any of the html above or below this code!).

Titles for the items to the right of the twitter embed are indicated as in the following example:

```
<h2 class="archive__item-title">Follow us</h2>
```

In this case changing "Follow us" to "New text" would change the title of that item to "New text".

Excerpts for the item are indicated as in the following example:

```html
<div class="archive__item-excerpt">
   <p>Keep up to date with the KITABis. Follow us on twitter or subscribe to our mailing list.</p>

</div>
```

In this case changing "Keep up to date with the KITABis. Follow us on twitter or subscribe to our mailing list." to "New excerpt" would change the excerpt text to "New excerpt". Make sure not to change the surrounding code, including keeping \<p\> and \</p\> on either side of the excerpt text.

The button links for each item are indicated as in the following example:

```html
<p><a href="/subscribe" class="btn btn--primary">Subscribe!</a></p>
```

In this case changing "/subscribe" to "/blogs" would change the link to the blogs page on the website. Changing "Subscribe!" to "New link" would change the text of the button to "New link".

#### A warning on making changes to the homepage
As minimal mistakes is a responsive website theme (it adjusts the content according to the screen size), changes to the html on this page can significantly impact the look of the website, potentially making it unreadable on certain screens. If you are new to using responsive themes, or html in general, we recommend that you make changes gradually and continuously check their impact on the website (by running 'bundle exec jekyll serve' each time you make a small change). When checking your changes, make sure you account for different screen sizes (resize the browser box on your computer so that it's mobile sized and a small screen size). **Do not push your changes to the remote repository until you are sure your are happy with the aesthetics of your changes. Reversing changes once they are pushed to the remote is possible, but it is more difficult and in the meantime your changes could impact upon the experience of current users of the KITAB website.**

### Applications portal

The applications portal is found here: 

```
_pages/corpus_data/apps.md
```

This page uses a 'splash' layout with feature rows. For a guide to adding and editing feature rows, [see above](#feature-rows)

## Adding blogs automatically from docx format

There are two automatic approaches to adding blog posts:
1. Using the server-based procedure
1. Using the script within the respository

### Using the server-based procedure

This procedure will be the preferred option for all team members. It is still being implemented - check back here for the procedure.

### Using the script within the repository

Within the repository for there is the folder 'conversion_script'. This folder contains the python script and dependencies for adding a new blog to the website. The following steps assume that Python and Jekyll have already been installed, and that you have a local clone of the GitHub respostory (see [dependencies](#dependencies) above). The script cannot be run directly from GitHub. 

To use this script take the following steps:

1. run 
        ```
        git pull origin master
        ```
        - to ensure your local repository is up-to-date with the remote
1. add the .docx files for the new blogs to 'input/blogs' (only .docx is supported - multiple blogs can be uploaded at once) 
1. Blog post files should be named as follows: firstname_surname.blogtitle (e.g. 'mathew_barber.visualisations blog.docx'). The author code before the '.' will correspond to the author id in authors.yml (see the guide to the _data folder [above](#_data)). If there are multiple blogs by the same author, add a number to the surname (e.g. 'mathew_barber1.second visualisations blog.docx')
1. copy the sample 'header_plain' file from the 'resources' folder into the 'input/headers' folder. Copy as many header_plain files into this folder as you have blog posts.
1. Give each header file a name that matches its corresponding blog post, using the extension .yml (e.g. the header file for 'mathew_barber.visualisations blog.docx' would be 'mathew_barber.yml')
1. Open the header files in a text editor (e.g. EditPad Pro)
1. Fill out the following fields in each header file, for each blog post: 'title', 'author', 'tags'. The 'image' field will be populated automatically by the script using the first image in the blog. This is the image that appears as the thumb on the homepage. If the blog has no images, you might want to specify a thumbnail image here. The 'author' field should correspond to the author id in 'authors.yml' (see the guide to the _data folder [above](#_data))

  Example of filled-out header file:


         ---
         header:
           overlay_image: "/images/covers/banner_blog.jpg"
           overlay_filter: 0.1
           caption: "Gentile Bellini - Scribe, 1479-1481 (Image courtesy of [Isabella Stewart Gardner Museum](https://www.gardnermuseum.org/experience/collection/10755), Boston)" 
           show_overlay_excerpt: false 
         title: "A blog on visualisation"
         author:	mathew_barber
         layout:	single
         categories:
           - 
           - 
         tags:
           - viz
         image : 
         ---

Once the files have been added, do the following:

1. If the blog author has not authored for KITAB before, add the author to authors.yml. To do this, copy an existing author from this file and change the id, name and short bio. As noted above, the author id will match that given in the file name and author field in the header file.
1. Open a python-enabled console.
1. cd into the 'conversion_script' directory.
1. run 
         ```
         python docx_converter.py
         ```
1. The script will run and state if it has suceeded.
1. Navigate to the '_posts' directly to check the new blogs have been added.

If the blogs have been added, do the follow:
1. open Ubuntu (or terminal in Mac or Linux) and cd into the repository
1. run 
        ```
        bundle exec jekyll serve
        ```
1. navigate to the local server and check the new blogs appear on the website

If the new blogs appear as expected on the website:
1. open Git Bash (in Windows) or use the terminal in Mac or Linux
1. cd into the repository for the website
1. run 
        ```
        git add .
        ```
1. run 
        ```
        git commit -m "added new blogs"
        ```
1. run 
        ```
        git push origin master
        ```

**If the blog posts do not add to the folder, or they do not appear as expected on the local website, do not push the changes back to GitHub. Instead submit an issue report on the respository specifying the problem**

## Manually adding blogs to the website

If blog posts are in markdown format, they can be manually added to the website without the use of the conversion script. As this involves a good knowledge of markdown, and manually adding blog images to the website directory, this is not the recommended approach. Although it is possible to add the blog and images directly to GitHub, it is easier to add a blog post and its images locally.

To do this, follow these steps:
1. open git Bash and cd into the website directory
1. run
        ```
        git pull origin master
        ```
        - this will update the local files and avoid conflicts
1. Open a text editor that supports markdown (such as EditPad Pro)
1. Create a new file for the blog post
1. Save the file in the '_posts' directory of the website repository, using the following format (using the date that you intend to release the blog post): 'yyyy-mm-dd-title-of-post' (e.g. 2021-11-08-visualisations-blog)
1. Copy the contents of the header_plain file in 'conversion_script/resources' into the top of the new markdown file.
1. Fill out the relevant fields of the header (making sure that the 'author' field matches the author id in authors.yml - see [above](#_data)
1. Paste text of the blog in markdown format into the file
1. go to the directory /images/blogs/ and add a new folder with the format yyyy-mm-dd
1. paste the blog images into this folder
1. update the image addresses in the markdown blog post file (for example, if you had saved image 'viz1.jpg' for the above specified blog, you would give the image location as : '/images/blogs/2021-11-08/viz1.jpg'
1. Open Ubuntu (or a terminal in Mac or Linux)
1. cd to the website repository
1. run
        ```
        bundle exec jekyll serve
        ```
1. Navigate to the local server address in your browser and check the new blog post is present (note: if the blog is dated into the future, it will not appear on the website until the specified date)

If the blog has been sucessfully added to the website, do the following to add the blog to the main website:
1. Go to git Bash
1. cd into the website repository
1. run
         ```
         git add .
         ```
1. run
         ```
         git commit -m"added new blog manually"
         ```
1. run
         ```
         git push origin master
         ```
1. Your changes should now appear on the main website