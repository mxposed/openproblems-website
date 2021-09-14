---
title: "Frequently Asked Questions"
type: book
date: "2021-08-02T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 100
---

Here are a list of common questions and answers related to the competition

## What if I only want to compete for one of the prizes in a task?

As described in the Tasks documentation, each task has up to five prizes. However, competitors need not compete for all prizes in a task. In Task 1 - Modality Prediction, for example, a competitor may compete on the subtask of predicting RNA from ATAC measurements. In this case, a submitted method may simply exit without writing a submission to disk.

## How can I upload a pre-trained model?
Competitors may submit pre-trained models for any of the tasks in the competition. Model parameters may included in the submission directory. They can be then made accessible to the submission script by editing the `config.vsh.yaml` file to list the parameter file under the `resources` section.

For example if you'd like to add a file containing model weights with the filename `weights.pt`, edit the resources block to look like the following:
```yaml
resources:
  # Script containing method
  - type: python_script
    path: script.py
  # Model weights file
  - type: file
    path: weights.pt
```
The model parameter file will now be accessible to the script in the working directory. This could be accessed, for example, by running `torch.load("./weights.pt")`.

For more information, see [Updating the Configuration](neurips_docs/submission/starter_kits/#updating-the-configuration).

## Why am I seeing "Process terminated with an error exit status (137)" when I generate a submission?

Exit code 137 is the SIGKILL out of memory error. It means one of the processed in the submission script ran out of memory. One common cause of is the default memory constraint for Docker Desktop is 2GB. If you're using Docker Desktop, you can edit the [Resources Configuration](https://docs.docker.com/desktop/mac/#resources).

If this isn't the issue, your script might be using too much memory and getting killed by your kernel. To limit the memory used by your script, try deleting unused variables or working with sparse matrix formats.