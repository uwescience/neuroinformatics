---
layout: post
comments: true
title: "Dynamic mode decomposition and best practices for sharing research code"
date: 2018-02-16
author: Eleanor Lutz
---

# Dynamic Mode Decomposition and best practices for sharing research code

This week James Kunert-Graf gave an overview of his recent work on Dynamic Mode Decomposition. We also discussed some of the best practices and tips for sharing code with other researchers. 

## Dynamic Mode Decomposition
James' work addresses the problem of automatically detecting and categorizing time-resolved resting state networks from a noisy and high-dimensional fMRI dataset. There are several existing methods to explore this high-dimensional dataset, such as Independent Component Analysis (ICA). James' work uses [Dynamic Mode Decomposition](https://arxiv.org/pdf/1409.5496.pdf), or DMD, to cluster this fMRI data. Compared to ICA, DMD can be helpful for detecting separate networks that are active at the same time. In addition, James' work showed that DMD can find clean modes that closely align with known patterns of brain activity. These methods for clustering large, noisy neuro datasets can help find brain regions with similar temporal dynamics. 

## Best practices for sharing research code

### When to share research code: 
We talked about the balance between sharing code as early as possible, while still making sure the code is commented and otherwise useable by other people. Several people agreed that code should be shared when the paper preprint is posted, at the very latest. Other suggestions included sharing the code from the beginning of the project, with the aim of inviting others to contribute and/or share suggestions and improvements throughout the process. Once the paper is officially published, it can be helpful to archive the published version with a DOI number, because Github repos are constantly updated and may not reflect the published paper in the future.

### What to share in terms of data and code: 
Because of privacy or permissions constraints, it might not be possible to include the raw data in the same location as the code. To give people the option to run the code without accessing external data, it might be useful to include a toy dataset to demonstrate code functionality. This can also be helpful for extremely large datasets, or to avoid possible deprecation issues with an external database not under the researchers' control. Another option is to include a script that can download all the relevant external data automatically upon execution, or simply provide written instructions for accessing data. 

### How to share research code: 
Shared code should ideally be functional years in the future. It should also be easy to install and run, at least for key functionalities like reproducing all the paper figures. Jupyter notebooks are useful for saving both the code and the output as one document, and one suggestion was to include a cell at the very top that prints version strings for all dependencies. The [watermark](https://github.com/rasbt/watermark) extension in Jupyter notebook can also print the environment information including hardware details. Version management can also be done through services like Docker or Singularity, although these services can sometimes make it difficult for the user to understand how the environment was created and replicate it themselves. To address this issue (and as a general rule of thumb), a requirements file should also be included that lists important version details. 