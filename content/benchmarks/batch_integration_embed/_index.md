+++
title = "Batch integration embed"
summary = "Removing batch effects while preserving biological variation (embedding output)"
headless = false
theme = "op"
+++
<!--- TODO: add links --->


## The task

This is a sub-task of the overall batch integration task. Batch (or data) integration
integrates datasets across batches that arise from various biological and technical
sources. Methods that integrate batches typically have three different types of output:
a corrected feature matrix, a joint embedding across batches, and/or an integrated
cell-cell similarity graph (e.g., a kNN graph). This sub-task focuses on all methods
that can output joint embeddings, and includes methods that canonically output corrected
feature matrices with subsequent postprocessing to generate a joint embedding. Other
sub-tasks for batch integration can be found for:

* [graphs](../batch_integration_graph/), and
* [corrected features](../batch_integration_features)

This sub-task was taken from a
[benchmarking study of data integration
methods](https://www.biorxiv.org/content/10.1101/2020.05.22.111161v2).

## The metrics

Metrics for batch integration (embed) measure how well batches are mixed while
biological signals are preserved. They are divided into batch correction and biological
variance conservation metrics.

### Batch correction

* **kBET**: kBET determines whether the label composition of a k nearest neighborhood of
a cell is similar to the expected (global) label composition
(Buettner et al., Nat Meth 2019). The test is repeated for a random subset of cells,
and the results are summarized as a rejection rate over all tested neighborhoods.
* **Silhouette batch score**: The absolute silhouette width is computed over batch
labels per cell. As 0 then indicates that batches are well mixed and any deviation from
0 indicates a batch effect, we use the 1-abs(ASW) to map the score to the scale [0;1].
* **Principal component regression (PC regression)**: This compare the explained
variance by batch before and after integration. It returns a score between 0 and 1
(scaled=True) with 0 if the variance contribution hasn’t changed. The larger the score,
the more different the variance contributions are before and after integration.

### Biological variance conservation

* **Cell cycle score**: The cell-cycle conservation score evaluates how well the
cell-cycle effect can be captured before and after integration.
* **Isolated label silhouette**: This score evaluates the compactness for the label(s)
that is(are) shared by fewest batches. It indicates how well rare cell types can be
preserved after integration.
* **Cell type ASW**: The absolute silhouette with is computed on cell identity labels,
measuring their compactness.
