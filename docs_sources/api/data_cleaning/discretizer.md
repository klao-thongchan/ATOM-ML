# Discretizer
-------------

<div style="font-size:20px">
<em>class</em> atom.data_cleaning.<strong style="color:#008AB8">Discretizer</strong>(strategy="quantile",
bins=5, labels=None, gpu=False, verbose=0, logger=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/data_cleaning.py#L1173">[source]</a>
</span>
</div>
Bin continuous data into intervals. For each feature, the bin edges
are computed during fit and, together with the number of bins, they
will define the intervals. Ignores numerical columns. It can be
accessed from atom through the [discretize](../../ATOM/atomclassifier/#discretize)
method. Read more in the [user guide](../../../user_guide/data_cleaning/#binning-numerical-features).

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>strategy: str, default="quantile"</strong><br>
Strategy used to define the widths of the bins. Choose from:
<ul style="line-height:1.2em;margin-top:5px">
<li>"uniform": All bins have identical widths.</li>
<li>"quantile": All bins have the same number of points.</li>
<li>"kmeans": Values in each bin have the same nearest center of a 1D k-means cluster.</li>
<li>"custom": Use custom bin edges provided through <code>bins</code>.</li>
</ul>
<strong>bins: int, sequence or dict, default=5</strong><br>
<ul style="line-height:1.2em;margin-top:5px">
<li>If int: Number of bins to produce for all columns. Not allowed if strategy="custom".</li>
<li>If sequence: Number of bins per column, where the n-th value
corresponds to the n-th column that is transformed. If strategy="custom",
it's the bin edges with length=n_bins + 1.</li>
<li>If dict: One of the aforementioned options per column, where the key is
the column's name.</li>
</ul>
<strong>labels: sequence, dict or None, default=None</strong><br>
Label names with which to replace the binned intervals.
<ul style="line-height:1.2em;margin-top:5px">
<li>If None: Use default labels of the form [min_edge]-[max_edge].</li>
<li>If sequence: Labels to use for all columns.</li>
<li>If dict: Labels per column, where the key is the column's name.</li>
</ul>
<strong>gpu: bool or str, default=False</strong><br>
Train estimator on GPU (instead of CPU). Not for strategy="custom".
<ul style="line-height:1.2em;margin-top:5px">
<li>If False: Always use CPU implementation.</li>
<li>If True: Use GPU implementation if possible.</li>
<li>If "force": Force GPU implementation.</li>
</ul>
<strong>verbose: int, default=0</strong><br>
Verbosity level of the class. Choose from:
<ul style="line-height:1.2em;margin-top:5px">
<li>0 to not print anything.</li>
<li>1 to print basic information.</li>
<li>2 to print detailed information.</li>
</ul>
<strong>logger: str, Logger or None, default=None</strong><br>
<ul style="line-height:1.2em;margin-top:5px">
<li>If None: Doesn't save a logging file.</li>
<li>If str: Name of the log file. Use "auto" for automatic naming.</li>
<li>Else: Python <code>logging.Logger</code> instance.</li>
</ul>
</td>
</tr>
</table>

!!! tip
    The transformation returns categorical columns. Use the [Encoder](../encoder)
    class to convert them back to numerical types.

!!! warning
    If strategy="custom", the columns returned can contain `NaN` if the values
    lie outside the specified bin edges.

<br>



## Attributes

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Attributes:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>feature_names_in_: np.array</strong><br>
Names of features seen during fit.
</p>
<p>
<strong>n_features_in_: int</strong><br>
Number of features seen during fit.
</p>
</td>
</tr>
</table>
<br>



## Methods

<table style="font-size:16px">
<tr>
<td><a href="#fit">fit</a></td>
<td>Fit to data.</td>
</tr>

<tr>
<td><a href="#fit-transform">fit_transform</a></td>
<td>Fit to data, then transform it.</td>
</tr>

<tr>
<td><a href="#get-params">get_params</a></td>
<td>Get parameters for this estimator.</td>
</tr>

<tr>
<td><a href="#log">log</a></td>
<td>Write information to the logger and print to stdout.</td>
</tr>

<tr>
<td><a href="#save">save</a></td>
<td>Save the instance to a pickle file.</td>
</tr>

<tr>
<td><a href="#set-params">set_params</a></td>
<td>Set the parameters of this estimator.</td>
</tr>

<tr>
<td><a href="#transform">transform</a></td>
<td>Transform the data.</td>
</tr>
</table>
<br>


<a name="fit"></a>
<div style="font-size:18px"><em>method</em> <strong style="color:#008AB8">fit</strong>(X, y=None)
<span style="float:right"><a href="https://github.com/tvdboom/ATOM/blob/master/atom/data_cleaning.py#L1236">[source]</a></span></div>
Fit to data.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: dataframe-like</strong><br>
Feature set with shape=(n_samples, n_features).
</p>
<p>
<strong>y: int, str, dict, sequence or None, default=None</strong><br>
Does nothing. Implemented for continuity of the API.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>Discretizer</strong><br>
Estimator instance.
</tr>
</table>
<br />


<a name="fit-transform"></a>
<div style="font-size:18px"><em>method</em> <strong style="color:#008AB8">fit_transform</strong>(X, y=None)
<span style="float:right"><a href="https://github.com/tvdboom/ATOM/blob/master/atom/data_cleaning.py#L109">[source]</a></span></div>
Fit to data, then transform it. Note that leaving y=None can lead
to errors if the `strategy` encoder requires target values.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: dataframe-like</strong><br>
Feature set with shape=(n_samples, n_features).
</p>
<p>
<strong>y: int, str, dict, sequence or None, default=None</strong><br>
Does nothing. Implemented for continuity of the API.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>pd.DataFrame</strong><br>
Transformed feature set.
</tr>
</table>
<br />


<a name="get-params"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">get_params</strong>(deep=True)
<span style="float:right">
<a href="https://github.com/scikit-learn/scikit-learn/blob/0fb307bf3/sklearn/base.py#L189">[source]</a>
</span>
</div>
Get parameters for this estimator.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>deep: bool, default=True</strong><br>
If True, will return the parameters for this estimator and contained
subobjects that are estimators.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>dict</strong><br>
Parameter names mapped to their values.
</td>
</tr>
</table>
<br />


<a name="log"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">log</strong>(msg, level=0)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basetransformer.py#L590">[source]</a>
</span>
</div>
Write a message to the logger and print it to stdout.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>msg: str</strong><br>
Message to write to the logger and print to stdout.
</p>
<p>
<strong>level: int, default=0</strong><br>
Minimum verbosity level to print the message.
</p>
</td>
</tr>
</table>
<br />


<a name="save"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">save</strong>(filename="auto")
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basetransformer.py#L611">[source]</a>
</span>
</div>
Save the instance to a pickle file.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>filename: str, default="auto"</strong><br>
Name of the file. Use "auto" for automatic naming.
</td>
</tr>
</table>
<br>


<a name="set-params"></a>
<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">set_params</strong>(**params)
<span style="float:right">
<a href="https://github.com/scikit-learn/scikit-learn/blob/0fb307bf3/sklearn/base.py#L221">[source]</a>
</span>
</div>
Set the parameters of this estimator.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<strong>**params: dict</strong><br>
Estimator parameters.
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>Discretizer</strong><br>
Estimator instance.
</td>
</tr>
</table>
<br />


<a name="transform"></a>
<div style="font-size:18px"><em>method</em> <strong style="color:#008AB8">transform</strong>(X, y=None) 
<span style="float:right"><a href="https://github.com/tvdboom/ATOM/blob/master/atom/data_cleaning.py#L1361">[source]</a></span></div>
Bin the data into intervals.
<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: dataframe-like</strong><br>
Feature set with shape=(n_samples, n_features).
</p>
<p>
<strong>y: int, str, dict, sequence or None, default=None</strong><br>
Does nothing. Implemented for continuity of the API.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>pd.DataFrame</strong><br>
Transformed feature set.
</tr>
</table>
<br />



## Example

=== "atom"
    ```python
    from atom import ATOMClassifier
    
    atom = ATOMClassifier(X, y)
    atom.discretize(strategy="custom", bins=[0, 18, 120], labels=["child", "adult"])
    ```

=== "stand-alone"
    ```python
    from atom.data_cleaning import Discretizer
    
    discretizer = Discretizer(
        strategy="custom",
        bins=[0, 18, 120],
        labels=["child", "adult"],
    )
    discretizer.fit(X_train)
    X = discretizer.transform(X)
    ```