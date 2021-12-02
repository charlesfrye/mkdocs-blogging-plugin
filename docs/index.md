---
title: Setup
---

# Setup

## Installation

```shell
pip3 install mkdocs-blogging-plugin
```

## Prerequisites

- Only `material` theme is adapted by far (pull requests are welcome).
- `navigation.instant` feature cannot be enabled if blog paging is on.
- Windows is not supported currently (pull requests are welcome).

## Usage

Add `blogging` in `plugins` and specify the directories to be included:

```yml
plugins:
  - blogging:
      dirs: # The directories to be included
        - blog
```

In the page you want to insert the blog content, just add a line `{{ blog_content }}` into your desired place:

```markdown
# Blogs

{{ blog_content }}
```

Optionally, in your articles, add meta tags providing their titles and descriptions, which will be displayed on the blog page:

```markdown
---
title: Lorem ipsum dolor sit amet
description: Nullam urna elit, malesuada eget finibus ut, ac tortor.
---
```

To exclude certain pages from the blog collection, add a meta tag `exculde_from_blog` in the meta section of the markdown file:

```markdown
---
exculde_from_blog: true
---
```

And it's done! You can open the page where you insert `{{ blog_content }}` and see how it is working.

## Options

Configure the plugin via following options:

```yml
theme:             # Use a predefined theme
  name: card
size: 5            # Number of articles in one page, default: 10
locale: en         # The locale for time localizations, default: system's locale
sort: 
  from: new        # Sort from new to old, default
  # or old         # Sort from old to new
  by: creation     # Sort by the first commit time, default
  # or revision    # Sort by the latest commit time
paging: false      # Disable paging
show_total: false  # Remove 'total pages' label
template: blog-override.html # Path to customized template
```

For more about themes and custom templates, see [Themes](theme.md) and [Template](theme.md) respectively.

## Publish on Github Pages

A few more steps need to be taken for hosting with Github Pages:

**Set `fetch-depth` to `0` when checking out with `actions/checkout`**

```yml
- uses: actions/checkout@v2
  with:
    fetch-depth: 0
```

Creation and revision time for articles rely on git logs, so a complete respository is required.
If it is not set, the plugin will take the latest commit time as fallback.

**Configure your locale in the plugin's configuration**

```yml
locale: zh-CN
```

Otherwise, the plugin will use locale of the server, which might not be expected.