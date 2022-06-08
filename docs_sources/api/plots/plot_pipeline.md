# plot_pipeline
---------------

<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">plot_pipeline</strong>(model=None,
show_params=True, title=None, figsize=None, filename=None, display=True)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/plots.py#L4197">[source]</a>
</span>
</div>

Plot a diagram of a model's pipeline.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>model: str or None, optional (default=None)</strong><br>
 Name of the model for which to draw the pipeline. If None,
it plots the current pipeline without any model.
</p>
<p>
<strong>show_params: bool, optional (default=True)</strong><br>
Whether to show the parameters used for every estimator.
</p>
<p>
<strong>title: str or None, optional (default=None)</strong><br>
Plot's title. If None, the title is left empty.
</p>
<p>
<strong>figsize: tuple or None, optional (default=None)</strong><br>
Figure's size, format as (x, y). If None, it adapts the size to the
length of the pipeline.
</p>
<p>
<strong>filename: str or None, optional (default=None)</strong><br>
Name of the file. Use "auto" for automatic naming.
If None, the figure is not saved.
</p>
<p>
<strong>display: bool or None, optional (default=True)</strong><br>
Whether to render the plot. If None, it returns the matplotlib figure.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>matplotlib.figure.Figure</strong><br>
Plot object. Only returned if <code>display=None</code>.
</td>
</tr>
</table>
<br />

!!! tip
    Print `atom.pipeline` in a notebook for [sklearn's interactive visualization](https://scikit-learn.org/stable/auto_examples/miscellaneous/plot_pipeline_display.html)
    of the pipeline.



## Example

```python
from atom import ATOMClassifier

atom = ATOMClassifier(X, y)
atom.impute(strat_num="median", strat_cat="drop", max_nan_rows=0.8)
atom.encode(strategy="LeaveOneOut", max_onehot=8, frac_to_other=0.02)
atom.balance(strategy="adasyn", sampling_strategy=1.0)
atom.feature_selection(strategy="univariate", n_features=20)
atom.run("Tree", metric="auc", n_calls=10)

atom.tree.plot_pipeline()
```

<div align="center">
    <img src="../../../img/plots/plot_pipeline.png" alt="plot_pipeline" width="700" height="400"/>
</div>
