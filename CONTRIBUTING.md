# Contributing To These Guides
You'd like to help us improve these guides? Great! We're always looking for new contributors to help us improve our documentation. There are many ways you can contribute, from writing new guides, improving existing guides, or even just fixing typos.


## What Can I Contribute?
There are many ways you can contribute to this project. Here are some examples:

- Writing new guides
- Improving existing guides
- Fixing typos
- Expanding explanations


## How Do I Contribute?
Contributing to this project is easy. Just follow these steps:

1. Fork this repository
2. Create a new branch for your changes
3. Make your changes
4. Commit your changes
5. Push your changes to your fork
6. Create a pull request
7. Wait for your changes to be reviewed and merged
8. Celebrate!
9. Repeat steps 2-8 as often as you like


## How Should I Write My Guide?


### Basics
We have a few guidelines for writing guides. Please follow these guidelines when writing your guide:

- Guides should be written in markdown format
- Guides should be written in a way that is easy to understand
- Guides should be written in a way that is easy to read
- Guides should be written in a way that is easy to follow
- Guides should be written in a way that is easy to translate
- Guides should be written in a way that is easy to maintain
- Guides should be written in a way that is easy to update
- Guides should be written in a way that is easy to expand
- Guides should be written in a way that is easy to improve
- That should cover it..


### File Location
The markdown files for guides need to be placed in the `/guides/` directory. The file name should be the same as the guide title, with all spaces replaced with hyphens. For example, a guide titled "How To Install rAthena" would be saved as `how-to-install-rathena.md`.

We have created some directories to help organize the guides. Please place your guide in the appropriate directory. If you are unsure where to place your guide, please ask in our [Discord server](https://discord.gg/kMeMXWEvSV).


### Markdown Guidelines
You can structure your guide any way you see fit, but we do have a few guidelines for writing markdown files to keep everything looks reasonably consistent.


#### Headings
Headings should be used to break up your guide into sections. When you use hashes `#` to create headings, you should use the following number of hashes for each heading:

- `#` - Top level heading (autogen - do not use in your guide)
- `##` - Second level heading
- `###` - Third level heading
- `####` - Fourth level heading

These headings are automatically turned into a table of contents on the guide page. This allows users to quickly jump to the section they are interested in.


#### Code Blocks
Code blocks should be used to display code. You can use code blocks to display commands, code snippets, or even entire files. To create a code block, you can use the following syntax:

	```
	# This is a code block
	```


#### Inline Code
Inline code should be used to display code that is part of a sentence. To create inline code, you can use the following syntax:

	`This is inline code`


#### Links
Links should be used to link to other pages. To create a link, you can use the following syntax:

	[Link Text](https://example.com)


#### Images
Images can be used, but we recommend using them sparingly. They should be linked from a permenant hosting solution (not somewhere that deletes images after x days) and should not be pushed to this repository unless absolutely necessary. To display an image, you can use the following syntax:

	![Image Alt Text](https://example.com/image.png)


#### Tables
Tables can be used to display data in a tabular format. To create a table, you can use the following syntax:

	| Column 1 | Column 2 | Column 3 |
	| -------- | -------- | -------- |
	| Row 1    | Row 1    | Row 1    |
	| Row 2    | Row 2    | Row 2    |
	| Row 3    | Row 3    | Row 3    |


#### Lists
Lists can be used to display data in a list format. To create a list, you can use the following syntax:

	- List Item 1
	- List Item 2
	- List Item 3


### Testing Your Guide
If you have MkDocs installed, you can test your guide locally by running the following command:

	mkdocs serve

This starts a local web server that you can use to view your guide. You can then visit `http://localhost:8000` in your web browser to view your guide. This is useful for testing links, images, and other formatting.


### What Happens Next?
Once you have created your pull request, it will be reviewed by a member of the documentation team or an rA Repository Maintaner. If your pull request is approved, it will be merged into the default (`master`) branch and after a few moments will be pushed automatically as a HTML file to the [Guides](https://rathena.github.io/user-guies/) website.

If your pull request is not approved, you will be given feedback on what needs to be changed before it can be merged.
