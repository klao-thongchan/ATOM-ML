# predict_log_proba
-------------------

<div style="font-size:20px">
<em>method</em> <strong style="color:#008AB8">predict_log_proba</strong>(X, verbose=None)
<span style="float:right">
<a href="https://github.com/tvdboom/ATOM/blob/master/atom/basepredictor.py#L242">[source]</a>
</span>
</div>

Get class log-probabilities on unseen data or rows in the dataset. New
data is first transformed through the model's pipeline. Transformers
that are only applied on the training set are skipped. If called from a
trainer, the best model in the pipeline (under the `winner` attribute)
is used. If called from a model, that model is used. The estimator must
have a `predict_log_proba` method.

<table style="font-size:16px">
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Parameters:</strong></td>
<td width="80%" class="td_params">
<p>
<strong>X: int, str, slice, sequence or dataframe-like</strong><br>
Index names or positions of rows in the dataset, or unseen feature
set with shape=(n_samples, n_features).
</p>
<strong>pipeline: bool, sequence or None, optional (default=None)</strong><br>
Transformers to use on the data before predicting.
<ul style="line-height:1.2em;margin-top:5px">
<li>If None: Only transformers that are applied on the whole dataset are used.</li>
<li>If False: Don't use any transformers.</li>
<li>If True: Use all transformers in the pipeline.</li>
<li>If sequence: Transformers to use, selected by their index in the pipeline.</li>
</ul>
<p>
<strong>verbose: int or None, optional (default=None)</strong><br>
Verbosity level of the output. If None, it uses the transformer's own verbosity.
</p>
</td>
</tr>
<tr>
<td width="20%" class="td_title" style="vertical-align:top"><strong>Returns:</strong></td>
<td width="80%" class="td_params">
<strong>np.array</strong><br>
The class log-probabilities of the input samples, with shape=(n_samples,)
for binary classification tasks and (n_samples, n_classes) for multiclass
classification tasks.
</td>
</tr>
</table>
<br />



## Example

```python
from atom import ATOMClassifier

atom = ATOMClassifier(X, y)
atom.run(["Tree", "AdaB"], metric="AP", n_calls=10)

# Make predictions on new data
predictions = atom.adab.predict_log_proba(X_new)
```