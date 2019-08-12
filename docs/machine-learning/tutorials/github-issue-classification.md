---
title: 'Tutorial: Categorize support issues - multiclass classification' 
description: Discover how to use ML.NET in a multiclass classification scenario to classify GitHub issues to assign them to a given area.
ms.date: 07/31/2019
ms.topic: tutorial
ms.custom: mvc, title-hack-0516
#Customer intent: As a developer, I want to use ML.NET to apply a multiclass classification learning algorithm so that I can understand how to categorize support issues to assign them to a given area.
---
# Tutorial: Categorize support issues using multiclass classification with ML .NET

This sample tutorial illustrates using ML.NET to create a GitHub issue classifier to train a model that classifies and predicts the Area label for a GitHub issue via a .NET Core console application using C# in Visual Studio.

In this tutorial, you learn how to:
> [!div class="checklist"]
> * Prepare your data
> * Transform the data
> * Train the model
> * Evaluate the model
> * Predict with the trained model
> * Deploy and Predict with a loaded model

You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/GitHubIssueClassification) repository.

## Prerequisites

* [Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.

* The [Github issues tab separated file (issues_train.tsv)](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv).
* The [Github issues test tab separated file (issues_test.tsv)](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv).

## Create a console application

### Create a project

1. Open Visual Studio 2017. Select **File** > **New** > **Project** from the menu bar. In the **New Project** dialog, select the **Visual C#** node followed by the **.NET Core** node. Then select the **Console App (.NET Core)** project template. In the **Name** text box, type "GitHubIssueClassification" and then select the **OK** button.

2. Create a directory named *Data* in your project to save your data set files:

    In **Solution Explorer**, right-click on your project and select **Add** > **New Folder**. Type "Data" and hit Enter.

3. Create a directory named *Models* in your project to save your model:

    In **Solution Explorer**, right-click on your project and select **Add** > **New Folder**. Type "Models" and hit Enter.

4. Install the **Microsoft.ML NuGet Package**:

    In Solution Explorer, right-click on your project and select **Manage NuGet Packages**. Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**, select the **v 1.0.0** package in the list, and select the **Install** button. Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.

### Prepare your data

1. Download the [issues_train.tsv](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv) and the [issues_test.tsv](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv) data sets and save them to the *Data* folder previously created. The first dataset trains the machine learning model and the second can be used to evaluate how accurate your model is.

2. In Solution Explorer, right-click each of the \*.tsv files and select **Properties**. Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.

### Create classes and define paths

Add the following additional `using` statements to the top of the *Program.cs* file:

[!code-csharp[AddUsings](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddUsings)]

Create three global fields to hold the paths to the recently downloaded files, and global variables for the `MLContext`,`DataView`, and `PredictionEngine`:

* `_trainDataPath` has the path to the dataset used to train the model.
* `_testDataPath` has the path to the dataset used to evaluate the model.
* `_modelPath` has the path where the trained model is saved.
* `_mlContext` is the <xref:Microsoft.ML.MLContext> that provides processing context.
* `_trainingDataView` is the <xref:Microsoft.ML.IDataView> used to process the training dataset.
* `_predEngine` is the <xref:Microsoft.ML.PredictionEngine%602> used for single predictions.

Add the following code to the line right above the `Main` method to specify those paths and the other variables:

[!code-csharp[DeclareGlobalVariables](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DeclareGlobalVariables)]

Create some classes for your input data and predictions. Add a new class to your project:

1. In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.

1. In the **Add New Item** dialog box, select **Class** and change the **Name** field to *GitHubIssueData.cs*. Then, select the **Add** button.

    The *GitHubIssueData.cs* file opens in the code editor. Add the following `using` statement to the top of *GitHubIssueData.cs*:

[!code-csharp[AddUsings](~/samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#AddUsings)]

Remove the existing class definition and add the following code, which has two classes `GitHubIssue` and `IssuePrediction`, to the *GitHubIssueData.cs* file:

[!code-csharp[DeclareGlobalVariables](~/samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#DeclareTypes)]

The `label` is the column you want to predict. The identified `Features` are the inputs you give the model to predict the Label.

Use the [LoadColumnAttribute](xref:Microsoft.ML.Data.LoadColumnAttribute) to specify the indices of the source columns in the data set.

`GitHubIssue` is the input dataset class and has the following <xref:System.String> fields:

* the first column `ID` (GitHub Issue ID)
* the second column `Area` (the prediction for training)
* the third column `Title` (GitHub issue title) is the first `feature` used for predicting the `Area`
* the fourth column  `Description` is the second `feature` used for predicting the `Area`

`IssuePrediction` is the class used for prediction after the model has been trained. It has a single `string` (`Area`) and a `PredictedLabel` `ColumnName` attribute.  The `PredictedLabel` is used during prediction and evaluation. For evaluation, an input with training data, the predicted values, and the model are used.

All ML.NET operations start in the [MLContext](xref:Microsoft.ML.MLContext) class. Initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects. It's similar, conceptually, to `DBContext` in `Entity Framework`.

### Initialize variables in Main

Initialize the `_mlContext` global variable  with a new instance of `MLContext` with a random seed (`seed: 0`) for repeatable/deterministic results across multiple trainings.  Replace the `Console.WriteLine("Hello World!")` line with the following code in the `Main` method:

[!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateMLContext)]

## Load the data

ML.NET uses the [IDataView class](xref:Microsoft.ML.IDataView) as a flexible, efficient way of describing numeric or text tabular data. `IDataView` can load either text files or in real time (for example, SQL database or log files).

To initialize and load the `_trainingDataView` global variable in order to use it for the pipeline, add the following code after the  `mlContext` initialization:

[!code-csharp[LoadTrainData](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTrainData)]

The [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) defines the data schema and reads in the file. It takes in the data path variables and returns an `IDataView`.

Add the following as the next line of code in the `Main` method:

[!code-csharp[CallProcessData](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallProcessData)]

The `ProcessData` method executes the following tasks:

* Extracts and transforms the data.
* Returns the processing pipeline.

Create the `ProcessData` method, just after the `Main` method, using the following code:

```csharp
public static IEstimator<ITransformer> ProcessData()
{

}
```

## Extract Features and transform the data

As you want to predict the Area GitHub label for a `GitHubIssue`, use the [MapValueToKey()](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A) method to transform the `Area` column into a numeric key type `Label` column (a format accepted by classification algorithms) and add it as a new dataset column:

[!code-csharp[MapValueToKey](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#MapValueToKey)]

Next, call `mlContext.Transforms.Text.FeaturizeText` which transforms the text (`Title` and `Description`) columns into a numeric vector for each called `TitleFeaturized` and `DescriptionFeaturized`. Append the featurization for both columns to the pipeline with the following code:

[!code-csharp[FeaturizeText](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#FeaturizeText)]

The last step in data preparation combines all of the feature columns into the **Features** column using the [Concatenate()](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate%2A) method. By default, a learning algorithm processes only features from the **Features** column. Append this transformation to the pipeline with the following code:

[!code-csharp[Concatenate](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Concatenate)]

 Next, append a <xref:Microsoft.ML.Data.EstimatorChain%601.AppendCacheCheckpoint%2A> to cache the DataView so when you iterate over the data multiple times using the cache might get better performance, as with the following code:

[!code-csharp[AppendCache](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AppendCache)]

> [!WARNING]
> Use AppendCacheCheckpoint for small/medium datasets to lower training time. Do NOT use it (remove .AppendCacheCheckpoint()) when handling very large datasets.

Return the pipeline at the end of the `ProcessData` method.

[!code-csharp[ReturnPipeline](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnPipeline)]

This step handles preprocessing/featurization. Using additional components available in ML.NET can enable better results with your model.

## Build and train the model

Add the following call to the `BuildAndTrainModel`method as the next line of code in the `Main` method:

[!code-csharp[CallBuildAndTrainModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallBuildAndTrainModel)]

The `BuildAndTrainModel` method executes the following tasks:

* Creates the training algorithm class.
* Trains the model.
* Predicts area based on training data.
* Returns the model.

Create the `BuildAndTrainModel` method, just after the `Main` method, using the following code:

```csharp
public static IEstimator<ITransformer> BuildAndTrainModel(IDataView trainingDataView, IEstimator<ITransformer> pipeline)
{

}
```

### About the classification task

Classification is a machine learning task that uses data to **determine** the category, type, or class of an item or row of data and is frequently one of the following types:

* Binary: either A or B.
* Multiclass: multiple categories that can be predicted by using a single model.

For this type of problem, use a Multiclass classification learning algorithm, since your issue category prediction can be one of multiple categories (multiclass) rather than just two (binary).

Append the machine learning algorithm to the data transformation definitions by adding the following as the first line of code in `BuildAndTrainModel()`:

[!code-csharp[AddTrainer](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTrainer)]

The [SdcaMaximumEntropy](xref:Microsoft.ML.Trainers.SdcaMaximumEntropyMulticlassTrainer) is your multiclass classification training algorithm. This is appended to the `pipeline` and accepts the featurized `Title` and `Description` (`Features`) and the `Label` input parameters to learn from the historic data.

### Train the model

Fit the model to the `splitTrainSet` data and return the trained model by adding the following as the next line of code in the `BuildAndTrainModel()` method:

[!code-csharp[TrainModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#TrainModel)]

The `Fit()`method trains your model by transforming the dataset and applying the training.

The [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) is a convenience API, which allows you to pass in and then perform a prediction on a single instance of data. Add this as the next line in the `BuildAndTrainModel()` method:

[!code-csharp[CreatePredictionEngine1](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine1)]

### Predict with the trained model

Add a GitHub issue to test the trained model's prediction in the `Predict` method by creating an instance of `GitHubIssue`:

[!code-csharp[CreateTestIssue1](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateTestIssue1)]

Use the [Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) function makes a prediction on a single row of data:

[!code-csharp[Predict](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Predict)]

### Using the model: prediction results

Display `GitHubIssue` and corresponding `Area` label prediction in order to share the results and act on them accordingly.  Create a display for the results using the following <xref:System.Console.WriteLine?displayProperty=nameWithType> code:

[!code-csharp[OutputPrediction](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#OutputPrediction)]

### Return the model trained to use for evaluation

Return the model at the end of the `BuildAndTrainModel` method.

[!code-csharp[ReturnModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnModel)]

## Evaluate the model

Now that you've created and trained the model, you need to evaluate it with a different dataset for quality assurance and validation. In the `Evaluate` method, the model created in `BuildAndTrainModel` is passed in to be evaluated. Create the `Evaluate` method, just after `BuildAndTrainModel`, as in the following code:

```csharp
public static void Evaluate(DataViewSchema trainingDataViewSchema)
{

}
```

The `Evaluate` method executes the following tasks:

* Loads the test dataset.
* Creates the multiclass evaluator.
* Evaluates the model and create metrics.
* Displays the metrics.

Add a call to the new method from the `Main` method, right under the `BuildAndTrainModel` method call, using the following code:

[!code-csharp[CallEvaluate](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallEvaluate)]

As you did previously with the training dataset, load the test dataset by adding the following code to the `Evaluate` method:

[!code-csharp[LoadTestDataset](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTestDataset)]

The [Evaluate()](xref:Microsoft.ML.MulticlassClassificationCatalog.Evaluate%2A) method computes the quality metrics for the model using the specified dataset. It returns a <xref:Microsoft.ML.Data.MulticlassClassificationMetrics> object that contains the overall metrics computed by multiclass classification evaluators.
To display the metrics to determine the quality of the model, you need to get them first.
Notice the use of the [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) method of the machine learning `_trainedModel` global variable (an [ITransformer](xref:Microsoft.ML.ITransformer)) to input the features and return predictions. Add the following code to the `Evaluate` method as the next line:

[!code-csharp[Evaluate](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Evaluate)]

The following metrics are evaluated for multiclass classification:

* Micro Accuracy - Every sample-class pair contributes equally to the accuracy metric.  You want Micro Accuracy to be as close to 1 as possible.

* Macro Accuracy - Every class contributes equally to the accuracy metric. Minority classes are given equal weight as the larger classes. You want Macro Accuracy to be as close to 1 as possible.

* Log-loss - see [Log Loss](../resources/glossary.md#log-loss). You want Log-loss to be as close to zero as possible.

* Log-loss reduction - Ranges from [-inf, 100], where 100 is perfect predictions and 0 indicates mean predictions. You want Log-loss reduction to be as close to zero as possible.

### Displaying the metrics for model validation

Use the following code to display the metrics, share the results, and then act on them:

[!code-csharp[DisplayMetrics](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayMetrics)]

### Save the model to a file

Once satisfied with your model, save it to a file to make predictions at a later time or in another application. Add the following code to the `Evaluate` method. 

[!code-csharp[SnippetCallSaveModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SnippetCallSaveModel)]

Create the `SaveModelAsFile` method below your `Evaluate` method.

```csharp
private static void SaveModelAsFile(MLContext mlContext,DataViewSchema trainingDataViewSchema, ITransformer model)
{

}
```

Add the following code to your `SaveModelAsFile` method. This code uses the [`Save`](xref:Microsoft.ML.ModelOperationsCatalog.Save*) method to serialize and store the trained model as a zip file.

[!code-csharp[SnippetSaveModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SnippetSaveModel)]

## Deploy and Predict with a model

Add a call to the new method from the `Main` method, right under the `Evaluate` method call, using the following code:

[!code-csharp[CallPredictIssue](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallPredictIssue)]

Create the `PredictIssue` method, just after the `Evaluate` method (and just before the `SaveModelAsFile` method), using the following code:

```csharp
private static void PredictIssue()
{

}
```

The `PredictIssue` method executes the following tasks:

* Loads the saved model
* Creates a single issue of test data.
* Predicts Area based on test data.
* Combines test data and predictions for reporting.
* Displays the predicted results.

Load the saved model into your application by adding the following code to the `PredictIssue` method:

[!code-csharp[SnippetLoadModel](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SnippetLoadModel)]

Add a GitHub issue to test the trained model's prediction in the `Predict` method by creating an instance of `GitHubIssue`:

[!code-csharp[AddTestIssue](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTestIssue)]

As you did previously, create a `PredictionEngine` instance with the following code:

[!code-csharp[CreatePredictionEngine](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine)]
  
Use the `PredictionEngine` to predict the Area GitHub label by adding the following code to the `PredictIssue` method for the prediction:

[!code-csharp[PredictIssue](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#PredictIssue)]

### Using the loaded model for prediction

Display `Area` in order to categorize the issue and act on it accordingly. Create a display for the results using the following <xref:System.Console.WriteLine?displayProperty=nameWithType> code:

[!code-csharp[DisplayResults](~/samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayResults)]

## Results

Your results should be similar to the following. As the pipeline processes, it displays messages. You may see warnings, or processing messages. These messages have been removed from the following results for clarity.

```console
=============== Single Prediction just-trained-model - Result: area-System.Net ===============
*************************************************************************************************************
*       Metrics for Multi-class Classification model - Test Data
*------------------------------------------------------------------------------------------------------------
*       MicroAccuracy:    0.738
*       MacroAccuracy:    0.668
*       LogLoss:          .919
*       LogLossReduction: .643
*************************************************************************************************************
=============== Single Prediction - Result: area-System.Data ===============
```

Congratulations! You've now successfully built a machine learning model for classifying and predicting an Area label for a GitHub issue. You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/GitHubIssueClassification) repository.

## Next steps

In this tutorial, you learned how to:
> [!div class="checklist"]
> * Prepare your data
> * Transform the data
> * Train the model
> * Evaluate the model
> * Predict with the trained model
> * Deploy and Predict with a loaded model

Advance to the next tutorial to learn more
> [!div class="nextstepaction"]
> [Taxi Fare Predictor](taxi-fare.md)
