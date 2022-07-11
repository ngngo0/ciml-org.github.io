# CIML Web

> CIML Web is a CIML website built using hexo. You can view the site @ https://ciml.sdsc.edu/.

## Install

1. Clone The Project

   ```
   cd your-hexo-folder

   git clone https://github.com/ciml-org/ciml-org.github.io.git
   ```

2. Install hexo

   ```
   npm i
   ```

3. Now you can run all the necessary hexo commands to start / modify the project, such as:

   ```
   // Start a local server
   npx hexo server

   // Generate static files for the website
   npx hexo generate

   // Deploy the static files onto the gh-pages branch of the repo
   npx hexo deploy
   ```

4. Usually, you shouldn't need to run `npx hexo deploy` since the Github Actions script will automatically detect
   changes made on `main` and automatically update the `gh-pages` branch

## Posts
All posts are saved in the `source/_posts` directory.
Posts in hexo have **front-matter** which determines how the post is organized, and where it can be found on the site.

The **front-matter** of a blog post looks vary depending on the type of content delivered.
Add this to the top of your blog markdown file. 

### Blog Post

```
---
title: "Hello World"
type: Blog
banner: your-banner-link.jpg
date: 2016-06-10 23:00
tags:
 - Movies
 - Life
---
```

### Summer Institute Post

```
---
title: Summer Institute
type: Event
event: Summer Institute
tags:
    - CIML
date: 2022-06-22
---
```

### Workshop Post

```
---
title: Workshop
type: Event
event: Workshop
tags:
    - CIML
---
```

### Tutorial Post

```
---
title: Tutorial
type: Event
event: Tutorial
tags:
    - CIML
---
```

### Webinar Post

```
---
title: Webinar
type: Event
event: Webinar
tags:
    - CIML
---
```

### Software Post

```
---
title: Software
type: Training
material: Software
tags:
    - CIML
---
```

### Interactive Video Post

```
---
title: Video
type: Training
material: Video
tags:
    - CIML
---
```

### Github Repo Post

```
---
title: Github
type: Training
material: Github
tags:
    - CIML
---
```

## Organization & Directories
Content in CIML web hexo are organized via the `source` directory within the repo.
On the website, content will be served via a url representing the file path from `source`.

For example, to find the page `summer_institutes`, it is located under the directory `source/events/summer_institutes`
This means, after hosting CIML web, this page can be found under `https://ciml.sdsc.edu/events/summer_institutes`

Any additional content added under this format will be served to the website under the specified path.

## Custom Layouts
Content added to our website can often contain a layout (or other parameters) in the **front-matter**.
For example, this **front-matter** from Summer Institutes contains both a layout and a sidebar:

```
---
title: Summer Institutes
layout: list-institutes
sidebar: 
  - {name: "Summer Institutes", link: "summer_institutes"}
  - {name: "Workshops & Tutorials", link: "workshops_and_tutorials"}
  - {name: "Webinars", link: "webinars"}
---
```

These layouts specifiy the `.ejs` template that will be used to load up this content.

In this section, we will go over the various custom ejs templates (and partials) created for the sake of CIML web.

These layouts and partials can be found under the path `themes/vexo/layout`

### Lists
In CIML web, I created a few layouts such as `list-blog.ejs, list-institutes.ejs, list-software.ejs, list-videos.ejs, ...`.

These layouts are designed to serve content in a blog style format, while paying close attention to filtering the type of content relevant. There is a layout specific for each kind of filter.

This layout requires no content in the `.md` file to be used

### Tags
Additonally there are layouts designed to filter tags as well. 
Such as `tags-blog.ejs, tags-institutes.ejs, tags-software.ejs, tags-videos.ejs`

This layout requires no content in the `.md` file to be used

### Cards
A specific layout for user cards has also been created to address the possibility of adding dynamic visual buttons for the user. This layout is unique as it requires content in the `.md` file to generate cards. 

```
// H1 represents the title for the section of cards
# Our Team

// Name of our card, and the link
[Mary Thomas (PI)](mary_thomas)

// Image for our card
![](images/MaryThomas.jpeg)

// A set of descriptors to be listed on our card
- Ph.D.
- Computational Data Scientist, HPC Trainer
- SDSC

[Marty Kandes (Co-PI)](marty_kandes)
![](images/MartyKandes.jpeg)
- Ph.D.
- Computational and Data Science Research Specialist
- SDSC

// A new block of cards
# Our Interns

...
```

### Sidebar
A unique sidebar element was created in order to support a more options in our user interface. 
It can be added in the **front-matter** like this:

```
---
title: Summer Institutes
layout: list-institutes
sidebar: 
  - {name: "Summer Institutes", link: "summer_institutes"}
  - {name: "Workshops & Tutorials", link: "workshops_and_tutorials"}
  - {name: "Webinars", link: "webinars"}
---
```

We style the parameters in the form of a JavaScript Object, each entry in the sidebar must have a `name` and a `link` attribute. 

- name: The name that will appear on the sidebar
- link: The href that we will redirect the user to, upon clicking on the sidebar button

```
  - {name: "Summer Institutes", link: "summer_institutes"}
```

### Contact
The contact form can be found in `themes/vexo/layout/contact.ejs`. This assuming the URL for the Google Contact Form Spreadsheet script has been changed, you must update the url in this file.

This file submits a `POST` request via RESTful API format to the app deployed by apps script on Google to store responses from users.

This layout requires no content in the `.md` file to be used


### Editing CSS For Style
In order to modify the CSS of our site, we need to modify the css in our hexo theme.

You can find the theme's css via going to `themes/vexo/source/css/`

### Modifying The Header Menu Links
These can be found in the overall config file, at `themes/vexo/source/_config.yml`