---
layout: post
title: Tensorflow Basics
date: 2018-02-04
---

## Tensorflow Basics

- based on https://www.tensorflow.org/programmers_guide/graphs

### Graph

- TensorFlow graph is a dataflow graph
- TensorFlow set up a **graph** and runs it through **session**
- nodes: units of computation ex) variable, operation..
- edges: data consumed or produced


- cf) tf.estimator.Estimator : high-level API. kind of ready-made graph

#### tf.Graph
 - Graph structure
 - Graph collections: *tf.add\_to\_collection* makes a list of objects with a key(defined in *tf.GraphKeys*) and using *tf.get_collection* , you can look up all objects associated with the key.