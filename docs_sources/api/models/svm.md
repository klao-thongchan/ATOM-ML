# Kernel SVM (kSVM)
-------------------

<a href="../../../user_guide/training/#automated-feature-scaling" class="md-tag" draggable=False>needs scaling</a>
<a href="../../../user_guide/data_management/#sparse-datasets" class="md-tag" draggable=False>accept sparse</a>
<a href="../../../user_guide/gpu" class="md-tag" draggable=False>supports_gpu</a>

The implementation of the Kernel (non-linear) Support Vector Machine is
based on libsvm. The fit time scales at least quadratically with the
number of samples and may be impractical beyond tens of thousands of
samples. For large datasets consider using a [Linear Support Vector Machine](../lsvm)
or a [Stochastic Gradient descent](../sgd) model instead.

The multiclass support is handled according to a one-vs-one scheme.

Corresponding estimators are:

* [SVC](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html)
  for classification tasks.
* [SVR](https://scikit-learn.org/stable/modules/generated/sklearn.svm.LinearSVR.html)
  for regression tasks.

Read more in sklearn's [documentation](https://scikit-learn.org/stable/modules/svm.html).


<br><br>
## Hyperparameters

* By default, the estimator adopts the default parameters provided by
  its package. See the [user guide](../../../user_guide/training/#parameter-customization)
  on how to customize them.
* The `degree` parameter is only used when kernel="poly".
* The `gamma` parameter is always set to "scale" when kernel="poly".
* The `coef0` parameter is only used when kernel="rbf".
* The `random_state` parameter is set equal to that of the parent.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Dimensions:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>C: float, default=1.0</strong><br>
Real(1e-3, 100, "log-uniform", name="C")
</p>
<p>
<strong>kernel: str, default="rbf"</strong><br>
Categorical(["linear", "poly", "rbf", "sigmoid"], name="kernel")
</p>
<p>
<strong>degree: int, default=3</strong><br>
Integer(2, 5, name="degree")
</p>
<p>
<strong>gamma: str, default="scale"</strong><br>
Categorical(["scale", "auto"], name="gamma")
</p>
<p>
<strong>coef0: float, default=0</strong><br>
Real(-1.0, 1.0, name="coef0")
</p>
<p>
<strong>epsilon: float, default=0.1</strong><br>
Real(1e-3, 100, "log-uniform", name="epsilon")
</p>
<p>
<strong>shrinking: bool, default=True</strong><br>
Categorical([True, False], name="shrinking")
</p>
</td>
</tr>
</table>



<br><br>
## Attributes

### Data attributes

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Attributes:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>dataset: pd.DataFrame</strong><br>
Complete dataset in the pipeline.
</p>
<p>
<strong>train: pd.DataFrame</strong><br>
Training set.
</p>
<p>
<strong>test: pd.DataFrame</strong><br>
Test set.
</p>
<p>
<strong>X: pd.DataFrame</strong><br>
Feature set.
</p>
<p>
<strong>y: pd.Series</strong><br>
Target column.
</p>
<p>
<strong>X_train: pd.DataFrame</strong><br>
Training features.
</p>
<p>
<strong>y_train: pd.Series</strong><br>
Training target.
</p>
<p>
<strong>X_test: pd.DataFrame</strong><br>
Test features.
</p>
<p>
<strong>y_test: pd.Series</strong><br>
Test target.
</p>
<p>
<strong>shape: tuple</strong><br>
Dataset's shape: (n_rows x n_columns).
</p>
<p>
<strong>columns: pd.Index</strong><br>
Names of the columns in the dataset.
</p>
<p>
<strong>n_columns: int</strong><br>
Number of columns in the dataset.
</p>
<p>
<strong>features: pd.Index</strong><br>
Names of the features in the dataset.
</p>
<p>
<strong>n_features: int</strong><br>
Number of features in the dataset.
</p>
<p>
<strong>target: str</strong><br>
Name of the target column.
</p>
</td>
</tr>
</table>
<br>


### Utility attributes

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Attributes:</strong></td>
<td width="80%" class="td_params">
<strong>bo: pd.DataFrame</strong><br>
Information of every step taken by the BO. Columns include:
<ul style="line-height:1.2em;margin-top:5px">
<li><b>call</b>: Name of the call.</li>
<li><b>params</b>: Parameters used in the model.</li>
<li><b>estimator</b>: Estimator used for this iteration (fitted on last cross-validation).</li>
<li><b>score</b>: Score of the chosen metric. List of scores for multi-metric.</li>
<li><b>time</b>: Time spent on this iteration.</li>
<li><b>total_time</b>: Total time spent since the start of the BO.</li>
</ul>
<p>
<strong>best_call: str</strong><br>
Name of the best call in the BO.
</p>
<p>
<strong>best_params: dict</strong><br>
Dictionary of the best combination of hyperparameters found by the BO.
</p>
<p>
<strong>estimator: class</strong><br>
Estimator instance with the best combination of hyperparameters fitted
on the complete training set.
</p>
<p>
<strong>time_bo: str</strong><br>
Time it took to run the bayesian optimization algorithm.
</p>
<p>
<strong>metric_bo: float or list</strong><br>
Best metric score(s) on the BO.
</p>
<p>
<strong>time_fit: str</strong><br>
Time it took to train the model on the complete training set and
calculate the metric(s) on the test set.
</p>
<p>
<strong>score_train: float or list</strong><br>
Metric score(s) on the training set.
</p>
<p>
<strong>score_test: float or list</strong><br>
Metric score(s) on the test set.
</p>
<p>
<strong>score_bootstrap: np.array</strong><br>
Bootstrap results with shape=(n_bootstrap,) for single-metric runs and
shape=(metric, n_bootstrap) for multi-metric runs.
</p>
<p>
<strong>mean_bootstrap: float or list</strong><br>
Mean of the bootstrap results. List of values for multi-metric runs.
</p>
<p>
<strong>std_bootstrap: float or list</strong><br>
Standard deviation of the bootstrap results. List of values for multi-metric runs.
</p>
<strong>results: pd.Series</strong><br>
Training results. Columns include:
<ul style="line-height:1.2em;margin-top:5px">
<li><b>metric_bo:</b> Best score achieved during the BO.</li>
<li><b>time_bo:</b> Time spent on the BO.</li>
<li><b>score_train:</b> Metric score on the training set.</li>
<li><b>score_test:</b> Metric score on the test set.</li>
<li><b>time_fit:</b> Time spent fitting and evaluating.</li>
<li><b>mean_bootstrap:</b> Mean score of the bootstrap results.</li>
<li><b>std_bootstrap:</b> Standard deviation score of the bootstrap results.</li>
<li><b>time_bootstrap:</b> Time spent on the bootstrap algorithm.</li>
<li><b>time:</b> Total time spent on the whole run.</li>
</ul>
</td>
</tr>
</table>
<br>


### Prediction attributes

The prediction attributes are not calculated until the attribute is
called for the first time. This mechanism avoids having to calculate
attributes that are never used, saving time and memory.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Prediction attributes:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>predict_train: pd.Series</strong><br>
Class predictions on the training set.
</p>
<p>
<strong> predict_test: pd.Series</strong><br>
Class predictions on the test set.
</p>
<p>
<strong>decision_function_train: pd.Series or pd.DataFrame</strong><br>
Predicted confidence scores on the training set (only if classifier).
</p>
<p>
<strong>decision_function_test: pd.Series or pd.DataFrame</strong><br>
Predicted confidence scores on the test set (only if classifier).
</p>
<p>
<strong>score_train: float</strong><br>
Model's score on the training set.
</p>
<p>
<strong>score_test: float</strong><br>
Model's score on the test set.
</p>
</td>
</tr>
</table>



<br><br>
## Methods

The majority of the [plots](../../../user_guide/plots) and [prediction methods](../../../user_guide/predicting)
can be called directly from the models, e.g. `atom.ksvm.plot_permutation_importance()` or `atom.ksvm.predict(X)`.
The remaining utility methods can be found hereunder.

<table style="font-size:16px">
<tr>
<td><a href="#calibrate">calibrate</a></td>
<td>Calibrate the model.</td>
</tr>

<tr>
<td><a href="#clear">clear</a></td>
<td>Clear attributes from the model.</td>
</tr>

<tr>
<td><a href="#cross-validate">cross_validate</a></td>
<td>Evaluate the model using cross-validation.</td>
</tr>

<tr>
<td><a href="#delete">delete</a></td>
<td>Delete the model.</td>
</tr>

<tr>
<td><a href="#dashboard">dashboard</a></td>
<td>Create an interactive dashboard to analyze the model.</td>
</tr>

<tr>
<td><a href="#evaluate">evaluate</a></td>
<td>Get the model's scores for the provided metrics.</td>
</tr>

<tr>
<td><a href="#export-pipeline">export_pipeline</a></td>
<td>Export the model's pipeline to a sklearn-like Pipeline object.</td>
</tr>

<tr>
<td><a href="#full-train">full_train</a></td>
<td>Train the estimator on the complete dataset.</td>
</tr>

<tr>
<td><a href="#inverse-transform">inverse_transform</a></td>
<td>Inversely transform new data through the pipeline.</td>
</tr>

<tr>
<td><a href="#rename">rename</a></td>
<td>Change the model's tag.</td>
</tr>

<tr>
<td><a href="#save-estimator">save_estimator</a></td>
<td>Save the estimator to a pickle file.</td>
</tr>

<tr>
<td><a href="#transform">transform</a></td>
<td>Transform new data through the pipeline.</td>
</tr>
</table>
<br>


<a name="calibrate"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">calibrate</strong>(**kwargs)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L651">[source]</a>
</span>
</div>
Applies probability calibration on the model. The estimator
is trained via cross-validation on a subset of the training
data, using the rest to fit the calibrator. The new classifier
will replace the `estimator` attribute. If there is an active
mlflow experiment, a new run is started using the name
`[model_name]_calibrate`. Since the estimator changed, the
model is [cleared](#clear). Only if classifier.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>**kwargs</strong><br>
Additional keyword arguments for sklearn's <a href="https://scikit-learn.org/stable/modules/generated/sklearn.calibration.CalibratedClassifierCV.html">CalibratedClassifierCV</a>.
Using cv="prefit" will use the trained model and fit the calibrator
on the test set. Use this only if you have another, independent set
for testing.
</td>
</tr>
</table>
<br />


<a name="clear"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">clear</strong>()
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L1060">[source]</a>
</span>
</div>
Reset attributes to their initial state, deleting potentially
large data arrays. Use this method to free some memory before
saving the class. The cleared attributes per model are:

* [Prediction attributes](../../../user_guide/predicting).
* [Metrics scores](../../../user_guide/training/#metric).
* [Shap values](../../../user_guide/plots/#shap).
* [Dashboard instance](../../../user_guide/data_management/#dashboard).

<br /><br /><br />


<a name="cross-validate"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">cross_validate</strong>(**kwargs)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L692">[source]</a>
</span>
</div>
Evaluate the model using cross-validation. This method cross-validates the
whole pipeline on the complete dataset. Use it to assess the robustness of
the solution's performance. The return of sklearn's <a href="https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_validate.html">cross_validate</a>
function is stored under the `cv` attribute.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>**kwargs</strong><br>
Additional keyword arguments for sklearn's cross_validate
function. If the scoring method is not specified, it uses
atom's metric.
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>pd.DataFrame</strong><br>
Overview of the results.
</td>
</tr>
</table>
<br />


<a name="delete"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">delete</strong>()
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L317">[source]</a>
</span>
</div>
If it's the last model in atom, the metric is reset. Use this
method to drop unwanted models from the pipeline or to free
some memory before saving. The model is not removed from any
active mlflow experiment.
<br /><br /><br />


<a name="dashboard"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">dashboard</strong>(dataset="test", filename=None, **kwargs)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L1205">[source]</a>
</span>
</div>
Create an interactive dashboard to analyze the model. The dashboard
allows you to investigate SHAP values, permutation importances,
interaction effects, partial dependence plots, all kinds of
performance plots, and even individual decision trees. By default,
the dashboard opens in an external dash app. The created dashboard
instance can be accessed through the `explainer_dashboard` attribute.
Read more in the [user guide](../../../user_guide/data_management/#dashboard).
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>dataset: str, default="test"</strong><br>
Data set to get the report from. Choose from: "train", "test",
"both" (train and test) or "holdout".
</p>
<p>
<strong>filename: str or None, default=None</strong><br>
Name to save the file with (as .html). None to not save anything.
</p>
<p>
<strong>**kwargs</strong><br>
Additional keyword arguments for the ExplainerDashboard instance.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong><a href="https://explainerdashboard.readthedocs.io/en/latest/dashboards.html">ExplainerDashboard</a></strong><br>
Created dashboard object.
</td>
</tr>
</table>
<br />


<a name="evaluate"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">evaluate</strong>(metric=None,
dataset="test", threshold=0.5, sample_weight=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L1120">[source]</a>
</span>
</div>
Get the model's scores for the provided metrics.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>metric: str, func, scorer, sequence or None, default=None</strong><br>
Metrics to calculate. If None, a selection of the most common
metrics per task are used.
</p>
<p>
<strong>dataset: str, default="test"</strong><br>
Data set on which to calculate the metric. Choose from: "train",
"test" or "holdout".
</p>
<strong>threshold: float, default=0.5</strong><br>
Threshold between 0 and 1 to convert predicted probabilities
to class labels. Only used when:
<ul style="line-height:1.2em;margin-top:5px">
<li>The task is binary classification.</li>
<li>The model has a <code>predict_proba</code> method.</li>
<li>The metric evaluates predicted target values.</li>
</ul>
<p>
<strong>sample_weight: sequence or None, default=None</strong><br>
Sample weights corresponding to y in <code>dataset</code>.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>pd.Series</strong><br>
Scores of the model.
</td>
</tr>
</table>
<br />


<a name="export-pipeline"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">export_pipeline</strong>(verbose=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L756">[source]</a>
</span>
</div>
Export the model's pipeline to a sklearn-like Pipeline object. If the
model used [automated feature scaling](../../../user_guide/training/#automated-feature-scaling),
the `scaler` is added to the pipeline. The returned pipeline is already
fitted on the training set.

!!! info
    ATOM's Pipeline class behaves the same as a sklearn <a href="https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html">Pipeline</a>,
    and additionally:
    <ul style="line-height:1.2em;margin-top:5px">
    <li>Accepts transformers that change the target column.</li>
    <li>Accepts transformers that drop rows.</li>
    <li>Accepts transformers that only are fitted on a subset of the
        provided dataset.</li>
    <li>Always outputs pandas objects.</li>
    <li>Uses transformers that are only applied on the training set (see the
        <a href="../../ATOM/atomclassifier/#balance">balance</a> or
        <a href="../../ATOM/atomclassifier/#prune">prune</a> methods)
        to fit the pipeline, not to make predictions on new data.</li>
    </ul>

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>memory: bool, str, Memory or None, default=None</strong><br>
Used to cache the fitted transformers of the pipeline.
<ul style="line-height:1.2em;margin-top:5px">
<li>If None or False: No caching is performed.</li>
<li>If True: A default temp directory is used.</li>
<li>If str: Path to the caching directory.</li>
<li>If Memory: Object with the <a href="https://joblib.readthedocs.io/en/latest/generated/joblib.Memory.html">joblib.Memory</a> interface.</li>
</ul>
<p>
<strong>verbose: int or None, default=None</strong><br>
Verbosity level of the transformers in the pipeline. If None, it leaves
them to their original verbosity. Note that this is not the pipeline's
own verbose parameter. To change that, use the <code>set_params</code>
method.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong><a href="https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html">Pipeline</a></strong><br>
Current branch as a sklearn-like Pipeline object.
</td>
</tr>
</table>
<br />


<a name="full-train"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">full_train</strong>(include_holdout=False)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L789">[source]</a>
</span>
</div>
In some cases it might be desirable to use all available data to train
a final model. Note that doing this means that the estimator can no
longer be evaluated on the test set. The newly retrained estimator will
replace the `estimator` attribute. If there is an active mlflow
experiment, a new run is started with the name `[model_name]_full_train`.
Since the estimator changed, the model is [cleared](#clear).

!!! warning
    Although the model is trained on the complete dataset, the pipeline
    is not! To also get the fully trained pipeline, use: `pipeline = atom
    .export_pipeline().fit(X, y)`.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>include_holdout: bool, default=False</strong><br>
Whether to include the holdout data set (if available) in the
training of the estimator. Note that if True, it means the model
can't be evaluated.
</td>
</tr>
</table>
<br />


<a name="inverse-transform"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">inverse_transform</strong>(X=None, y=None, verbose=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L1679">[source]</a>
</span>
</div>
Inversely transform new data through the pipeline. Transformers that
are only applied on the training set are skipped. The rest should all
implement a `inverse_transform` method. If only `X` or only `y` is
provided, it ignores transformers that require the other parameter.
This can be of use to, for example, inversely transform only the target
column. If called from a model that used automated feature scaling,
the scaling is inversed as well.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: dataframe-like or None, default=None</strong><br>
Transformed feature set with shape=(n_samples, n_features).
If None, X is ignored in the transformers.
</p>
<strong>y: int, str, dict, sequence or None, default=None</strong><br>
<ul style="line-height:1.2em;margin-top:5px">
<li>If None: y is ignored in the transformers.</li>
<li>If int: Position of the target column in X.</li>
<li>If str: Name of the target column in X.</li>
<li>Else: Array with shape=(n_samples,) to use as target.</li>
</ul>
<p>
<strong>verbose: int or None, default=None</strong><br>
Verbosity level of the output. If None, it uses the transformer's
own verbosity.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>pd.DataFrame</strong><br>
Original feature set. Only returned if provided.
</p>
<p>
<strong>pd.Series</strong><br>
Original target column. Only returned if provided.
</p>
</td>
</tr>
</table>
<br /><br />


<a name="rename"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">rename</strong>(name=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L817">[source]</a>
</span>
</div>
Change the model's tag. The acronym always stays at the beginning
of the model's name. If the model is being tracked by mlflow, the
name of the corresponding run is also changed.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>name: str or None, default=None</strong><br>
New tag for the model. If None, the tag is removed.
</table>
<br />


<a name="save-estimator"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">save_estimator</strong>(filename="auto")
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L854">[source]</a>
</span>
</div>
Save the estimator to a pickle file.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>filename: str, default="auto"</strong><br>
Name of the file. Use "auto" for automatic naming.
</td>
</tr>
</table>
<br />


<a name="transform"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">transform</strong>(X, y=None, verbose=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basemodel.py#L895">[source]</a>
</span>
</div>
Transform new data through the pipeline. Transformers that are only
applied on the training set are skipped. If only `X` or only `y` is
provided, it ignores transformers that require the other parameter.
This can be of use to, for example, transform only the target column.
If called from a model that used automated feature scaling, the data
is scaled as well.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: dataframe-like</strong><br>
Feature set with shape=(n_samples, n_features). If None, X is ignored
in the transformers.
</p>
<strong>y: int, str, dict, sequence or None, default=None</strong><br>
<ul style="line-height:1.2em;margin-top:5px">
<li>If None: y is ignored in the transformers.</li>
<li>If int: Position of the target column in X.</li>
<li>If str: Name of the target column in X.</li>
<li>Else: Array with shape=(n_samples,) to use as target.</li>
</ul>
<p>
<strong>verbose: int or None, default=None</strong><br>
Verbosity level of the output. If None, it uses the transformer's own verbosity.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>pd.DataFrame</strong><br>
Transformed feature set. Only returned if provided.
</p>
<p>
<strong>pd.Series</strong><br>
Transformed target column. Only returned if provided.
</p>
</td>
</tr>
</table>
<br />



## Example

```python
from atom import ATOMRegressor

atom = ATOMRegressor(X, y)
atom.run(models="kSVM", metric="r2", est_params={"kernel": "rbf"})
```
