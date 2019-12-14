# Testing models
In the previous section, we've looked at training models in ML.NET. In this
section, we'll expand the training pipeline with some testing logic.

We'll cover the following topics:

* Using cross-validation for testing
* Using other methods for testing

Let's expand the pipeline with cross-validation logic to test the model.

## Using cross-validation for testing

[![](http://img.youtube.com/vi/IamXQZQyWBg/0.jpg)](http://www.youtube.com/watch?v=IamXQZQyWBg "Validating the model")

The data for this tutorial doesn't include a test set. We could introduce one by
splitting the input file into a training and test set. However, we're not going
to do that for now. Instead, we're going to explore using cross-validation.

Open up `Program.cs` in the `Trainer` project and add the following code to the
end of the `Main` method:

``` csharp
var results = mlContext.MulticlassClassification.CrossValidate(
    data: dataView, estimator: trainingPipeline, numberOfFolds: 5
);

foreach (var entry in results)
{
    Console.WriteLine(entry.Metrics.ConfusionMatrix.GetFormattedConfusionTable());
}
```

The code performs the following steps:

1. First, we call the CrossValidate method with the dataset, the training
   pipeline, and the number of validation cycles to use.
2. Next, we print the validation results of each cross-validation cycle to the
   terminal.

You can run the application now. You should see a bunch of tables getting
printed to the terminal. Check the output on the terminal, notice any areas that
are hard to predict?

Cross-validation is a useful technique if you haven't got a separate test set.
Should you have a separate test set than using other validation techniques is a
better option.

## Using other methods for testing

You can add other validation methods instead of cross-validation if you have the
data for it. In this paragraph, we'll explore how to use other validation
methods. We're not adding them to the code since we don't have the dataset for
them.

To validate a model using a test set, you can use the following code:

``` csharp
var scoredData = trainedModel.Transform(testData);

var evaluationResults = mlContext.MulticlassClassification.Evaluate(
    data: scoredData, labelColumnName: "Label", scoreColumnName: "Score",
    predictedLabelColumnName: "PredictedLabel");
```

This code performs the following steps:

1. First, we use the trained model to make predictions on the test data.
2. Next, we use the `Evaluate` method to score the predictions.

The output of the `Evaluate` method is a set of metrics. It contains, among
other properties, the following properties:

* LogLoss
* Accuracy


Using this method you can quickly evaluate how the model is doing.

## Summary

In this section, we've explored how to use cross-validation and regular
validation method to test your model.

In the next section, we'll look at how to use the model in a ASP.NET core web
application.

[Next section](using-models/README.md)