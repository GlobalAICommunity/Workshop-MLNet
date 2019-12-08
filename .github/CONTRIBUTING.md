# Contributing guideline

Thank you for helping us improve this tutorial! We kindly ask you to follow
the guidelines in this document to help us approve your changes as fast 
as possible.

## How you can contribute

### Submitting a pull request 
To create a new pull request, make sure to follow these steps:

* Fork this repository if you haven't done so
* Create a new branch with a descriptive name using 
  `git checkout -b <branch-name>`.
* Commit your changes
* Push your changes using `git push origin -u <branch-name>`
* Create a new pull request on github

### General tips

* Only touch the files you want to change, please make sure not to reformat 
  files. It makes reviewing your changes a lot harder than necessary.
* Please, follow the checklist in this guide. It will help you get your changes
  approved a lot faster.
* There's a set of powerpoint slides in this repository. You are free to change
  those to your personal taste. But please, don't submit changes for them. The 
  slides are only there for reference.

## Service Level Agreement

We're doing our utmost best to review your pull request as soon as possible.
This is work we do during the evenings outside of work, so you may not get a 
response the minute you submit a pull request.

Usually, you'll get a response within 2 days.

## Checklist

### Spelling and grammar check

We ask you to check your documentation for spelling and grammar.
You can use the free online tool grammarly or something like office spelling.

### Check your documentation changes in the browser

The documentation is rendered using docsify. You can download and install it
using npm: `npm install -g docsify`. Then run the following command
to render the website:

```
docsify serve docs/
```

Now, open your browser and navigate to `http://localhost:3000/` to view the 
docs and verify that they render correctly.

### Test the tutorial steps

It's really easy to mess up the steps in the tutorial. Please make sure you
run through the tutorial on a clean copy of the sources.

We understand that you're not going to install a clean VM for your changes,
but working off a clean copy will greatly reduce the risk of errors 
in the tutorial.

### Test your code changes

There's a completed and starter version of the tutorial in the `src` folder.
Please make sure that you test any SDK/library changes against both versions.
They should compile and run without errors.

