# Getting started with ML.NET

This section of the tutorial covers how to get started with ML.NET. We'll cover
the following topics:

* What we'll be working on during this tutorial
* Creating a new project
* Installing ML.NET in your project

## What we'll be working on during this tutorial

This tutorial is focused primarily on learning how to use ML.NET in your
project. In this tutorial, we're working on a multi-class classifier for
labeling Github issues.

In this section of the tutorial, we're creating a new ASP.NET Core web
application and installing the ML.NET package.

Let's start by creating an empty web project for the project.

## Creating a new project

[![](http://img.youtube.com/vi/NWQF11Fc9_s/0.jpg)](http://www.youtube.com/watch?v=NWQF11Fc9_s "Creating a new project")

Open a terminal (Powershell on Windows, Mac Terminal or your Linux terminal) and execute 
the following commands to create a new project:

* `mkdir github-issue-classifier`
* `cd github-issue-classifier`
* `dotnet new sln -n GithubIssueClassifier`
* `dotnet new web -n Website`
* `dotnet new classlib -n Model`
* `dotnet new console -n Trainer`
* `dotnet sln add Website`
* `dotnet sln add Model`
* `dotnet sln add Trainer`

These commands perform the following steps:

1. First, we create a new project directory. 
2. Then, we add a new solution file to the project folder. 
3. Next, create a new empty web project. 
4. Finally, we're adding the project to the solution file.

After you've executed these commands, you can open the solution file in Visual
Studio 2019 or execute `code .` from the project folder to open up Visual Studio
Code.

**Note**: You can also use the files from the [starter folder](../../src/starter/) to get started.
In case you're using the starter files, skip over the rest of the steps in this section.

Now that you have an empty web project, let's add the ML.NET package to it.

## Installing ML.NET in your project

[![](http://img.youtube.com/vi/ufPhvsKEYAM/0.jpg)](http://www.youtube.com/watch?v=ufPhvsKEYAM "Adding a reference to the ML.NET package")

Execute the following command in each of the project directories that you 
just created.

```
dotnet add package Microsoft.ML --version 1.4
```

By executing this command you'll add a reference to the `Microsoft.ML` package.
After adding the reference to the ML.NET package, let's finalize the project
layout.

## Finalizing the project layout

[![](http://img.youtube.com/vi/6WZi6UIgwfE/0.jpg)](http://www.youtube.com/watch?v=6WZi6UIgwfE "Adding references the projects")

We now have a solution that has three projects:

* Website - The client that is going to use the model
* Trainer - The console application that is going to train the model
* Model - The components related to the model itself

We haven't set up any references between the projects. We'll do that next.

First, there's the model project that contains the classes that define 
the input, and output of the model and any other code that relates to the model.

The website project provides a user interface to use the model. It needs a
reference to the model project to use it.

Finally, we have a trainer project that is used to train the machine learning
model. The trainer project also needs a reference to the model project.

To set up the references, use the following commands:

* `cd Website`
* `dotnet add reference ../Model`
* `cd ../Trainer`
* `dotnet add reference ../Model`

And that's it, we're good to continue with the next step.

## Summary

In this section, we've created a new project for the Github issue classifier and
added the ML.NET package to it. In the next section, we'll load the dataset to
prepare the model.

[Next section](../loading-data/README.md)

