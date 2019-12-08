# Using models

In the previous section, we've tested the model that we trained. In this section
we'll take a look at how to use ML.NET models in ASP.NET Core.

We'll cover the following topics:

* Preparing the solution
* Building prediction logic
* Making a prediction

Let's get started.

## Preparing the solution

To make a prediction, we'll need a page in the web application that allows the
user to enter some test data. Since this is no an ASP.NET tutorial, we've gone
ahead and prebuilt the page for you.

Copy the contents from the [src/starter/Website](../../src/starter/Website) folder into the
Website project. Make sure to build and run the project to make sure that the
code works as expected.

You can run the website by using the following command from the `Website`
folder:

``` shell
dotnet run
```

When the website works, let's move on to loading the model that we trained in
the previous section.

## Building prediction logic

Before we can make a prediction, we need to load up the model. For this, we're
going to wire up a prediction engine from ML.NET into our website.

Let's get started.

## Prepare the startup logic

The prediction engine that we're going to wire up needs access to the 
hosting environment of the website to locate the model file.

First, we need to import a few namespaces. Add the following lines
below the existing `using` statements in `Startup.cs` in the `Website` project:

``` csharp
using Microsoft.Extensions.ML;
```

Next, add the following code to the top of the `Startup` class in `Startup.cs`
in the `Website` project:

``` csharp
private IHostEnvironment Environment { get; }

public Startup(IHostEnvironment environment)
{
    Environment = environment;
}
```

This code performs the following steps:

1. First, we add a new property called `Environment`. This will give access
   to the content path of the application and other important information.
2. Next, we add a new constructor that takes a parameter `environment` and 
   stores its value into the `Environment` property.

After we've prepared the startup class, let's take a look at wiring up the
prediction egine.

## Adding a prediction engine to the website

Before we can make any prediction we need to wire up the prediction engine in
the website project. Add the following code to the `ConfigureServices` method in
the `Startup.cs` file in the `Website` project:

``` csharp
var modelFilePath = Path.Combine(
    Environment.ContentRootPath, 
    "GithubClassifier.zip");

services
    .AddPredictionEnginePool<GithubIssue, GithubIssuePrediction>()
    .FromFile(modelName: "GithubIssueClassifier", filePath: modelFilePath);
```

This code performs the following steps:

1. First, we find the filename for the model to load.
2. Next, we add a new prediction engine pool for our model. The prediction
   engine pool is configured to use a `GithubIssue` as input and
   `GithubIssuePrediction` as output.
3. Finally, we load the model for the prediction pool from disk and give it a
   name.

Now that we have the prediction engine pool ready, let's take a look at the
homepage and use the prediction engine pool to make a prediction.

## Making a prediction
In this final step of the tutorial, we're going to wire up the 
`GithubIssueLabeler` to the page model of the homepage.

Open up the `Index.cshtml.cs` file in the `Pages` folder of the `Website`
project. Add the following code to the top of the class:

``` csharp
private readonly PredictionEnginePool<GithubIssue, GithubIssuePrediction> _predictionEnginePool;

public IndexModel(PredictionEnginePool<GithubIssue, GithubIssuePrediction> predictionEnginePool)
{
    _predictionEnginePool = predictionEnginePool;
}
```

This code performs the following steps:

1. First, we define a field to store the instance of the prediction engine pool
   component.
1. Next, we define a new constructor that accepts a prediction engine pool
   instance.
2. Finally, we assign the prediction engine pool instance to the private field.

The next step is to wire up the prediction method of the labeler to the page.
Add the following code to the `OnPost` method of the `IndexModel` class
in `Website/Pages/Index.cshtml.cs`:

``` csharp
var issue = new GithubIssue
{
    Title = Input.Title,
    Description = Input.Description
};

var prediction = _predictionEnginePool.Predict(
    modelName: "GithubIssueClassifier", 
    example: issue);
    
PredictedArea = prediction.Area;

return Page();
```

This code performs the following steps:

1. First, we create a new issue from the input that we received from the user.
2. Next, we call the labeler to predict a label for the issue
3. Finally, we assign the result to the `PredictedArea` property.

Once you've got the code in place, run the website from the `Website` folder
using the following command:

```
dotnet run
```

Open up your browser to `https://localhost:5001/` and try it out!

## Summary

In this tutorial, we've explored how to use ML.NET for a multi-class
classification problem. You've learned how to load data, train a model, test it,
and finally use it in your application.

Thank you for your time and hope you enjoyed it!

Feel free to post an issue on this repository if you've found something wrong in
the text. Otherwise, have a great day!

If you're up for it, you can also try the automated ML tool. 
[Here's a video to demonstrate how it works.](https://youtu.be/6udPLZR0vvQ)
