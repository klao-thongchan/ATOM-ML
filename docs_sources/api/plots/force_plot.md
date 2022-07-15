# force_plot
------------

<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">force_plot</strong>(models=None,
index=None, show=None, target=1, title=None, figsize=(14, 6),
filename=None, display=True, **kwargs)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/plots.py#L3461">[source]</a>
</span>
</div>

Plot SHAP's force plot. Visualize the given SHAP values with an additive
force layout. Note that by default this plot will render using javascript.
For a regular figure use `matplotlib=True` (this option is only available
when only a single sample is plotted). Read more about SHAP plots in the
[user guide](../../../user_guide/plots/#shap).

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>models: str, sequence or None, optional (default=None)</strong><br>
Name of the model to plot. If None, all models in the pipeline are
selected. Note that leaving the default option could raise an
exception if there are multiple models in the pipeline. To avoid
this, call the plot from a model, e.g. <code>atom.xgb.force_plot()</code>.
</p>
<p>
<strong>index: int, str, sequence or None, optional (default=None)</strong><br>
Index names or positions of the rows in the dataset to plot.
If None, it selects all rows in the test set.
</p>
<p>
<strong>target: int or str, optional (default=1)</strong><br>
Index or name of the class in the target column to look at. Only for
multi-class classification tasks.
</p>
<p>
<strong>title: str or None, optional (default=None)</strong><br>
Plot's title. If None, the title is left empty.
</p>
<p>
<strong>figsize: tuple, optional (default=(14, 6))</strong><br>
Figure's size, format as (x, y).
</p>
<p>
<strong>filename: str or None, optional (default=None)</strong><br>
Name of the file. If matplotlib=False, the figure is saved as a html
 file. If None, the figure is not saved.
</p>
<p>
<strong>display: bool or None, optional (default=True)</strong><br>
Whether to render the plot. If None, it returns the matplotlib figure.
</p>
<p>
<strong>**kwargs</strong><br>
Additional keyword arguments for SHAP's <a href="https://shap.readthedocs.io/en/latest/generated/shap.plots.force.html">force plot</a>.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>matplotlib.figure.Figure</strong><br>
Plot object. Only returned if <code>display=None</code> and <code>matplotlib=True</code>.
</td>
</tr>
</table>

!!! warning
    This plot can not be called from a canvas because of incompatibility
    between the ATOM and shap API.

<br>



## Example

```python
from atom import ATOMClassifier

atom = ATOMClassifier(X, y)
atom.run("lr")
atom.force_plot(index=120, matplotlib=True, filename="force_plot")
```

<div align="center">
    <img src="../../../img/plots/force_plot.png" alt="force_plot" width="1000" height="420"/>
</div>

