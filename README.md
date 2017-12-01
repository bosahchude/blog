# www.CodeLeg.com Blog Generator

Contains a Jekyll site for generating www.CodeLeg.com

This repo contains the files Jekyll needs to create the site.

This is a GitHub Specific version of Jekyll and can be run with

    bundle exec jekyll serve

## Creating Posts

Simply drop the markdown or html file into the _posts_ folder

Naming convention should be

    year-month-day-title.md

for markdown files, and

    year-month-day-title.html

for HTML files. HTML files should be contained within a _div_

Images and other static files should be stored in the _assets_ folder.

### Front Matter Format

The following front matter should be created for each posts:

    ---
    layout:   post
    title:    Your Post Title
    date:     yyyy-mm-dd
    Category: Data Science
    tags:     One, Two, Three, Four
    ---

To enable commenting, you have to explicitly set it with:

    comments: true

**Note:** You have to omit the line entirely to disable commenting, Simply
changing comments to false would still display comments. Okay?
