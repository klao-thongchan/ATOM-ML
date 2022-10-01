# plot_pca
----------

<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">plot_pca</strong>(title=None,
figsize=(10, 6), filename=None, display=True)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/plots.py#L486">[source]</a>
</span>
</div>

Plot the explained variance ratio vs the number of components. If the
underlying estimator is [pca](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.pca.html)
(for dense datasets), all possible components are plotted. If the
underlying estimator is [TruncatedSVD](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.TruncatedSVD.html)
(for sparse datasets), it only shows the selected components. The blue
star marks the number of components selected by the user. Only
available if [pca](../../../user_guide/feature_engineering/#pca) was
applied on the data.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>title: str or None, default=None</strong><br>
Plot's title. If None, the title is left empty.
</p>
<p>
<strong>figsize: tuple, default=(10, 6)</strong><br>
Figure's size, format as (x, y).
</p>
<p>
<strong>filename: str or None, default=None</strong><br>
Name of the file. Use "auto" for automatic naming.
If None, the figure is not saved.
</p>
<p>
<strong>display: bool or None, default=True</strong><br>
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



## Example

```python
from atom import ATOMClassifier

atom = ATOMClassifier(X, y)
atom.feature_selection(strategy="pca", n_features=11)
atom.plot_pca()
```

<div align="center">
    <img src="../../../img/plots/plot_pca.png" alt="plot_pca" width="700" height="420"/>
</div>
