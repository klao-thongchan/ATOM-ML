# plot_wordcloud
----------------

<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">plot_wordcloud</strong>(index=None,
title=None, figsize=(10, 6), filename=None, display=True, **kwargs)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/plots.py#L4241">[source]</a>
</span>
</div>

Plot a wordcloud from the corpus. The text for the plot is extracted
from the column named `corpus`. If there is no column with that name,
an exception is raised.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>index: int, str, sequence or None, default=None</strong><br>
Index names or positions of the documents in the corpus to
include in the wordcloud. If None, it selects all documents
in the dataset.
</p>
<p>
<strong>title: str or None, default=None</strong><br>
Plot's title. If None, the title is left empty.
</p>
<p>
<strong>figsize: tuple, default=(10, 6))</strong><br>
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
<p>
<strong>**kwargs</strong><br>
Additional keyword arguments for the <a href="https://amueller.github.io/word_cloud/generated/wordcloud.WordCloud.html">WordCloud</a> class.
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

atom = ATOMClassifier(X_text, y_text)
atom.plot_wordcloud()
```

<div align="center">
    <img src="../../../img/plots/plot_wordcloud.png" alt="plot_wordcloud" width="720" height="460"/>
</div>
