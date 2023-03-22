---
layout: post
title: SafeBound A Practical System for Generating Cardinality Bounds
categories: [Paper]
---
# First Pass
## Basic Information
### Title : SafeBound A Practical System for Generating Cardinality Bounds

### Authors : University of Washington

### Abstract(Based Self-Understanding): 
Cardinality estimators often underestimate the true cardinalities of query operators, which will guide optimizer choose costly query execution plans. Pessimistic Cardinality estimation is alternative approach to alleviate this problem, but existing pessimistic cardinality estimators are not practical due to relying limited statistics on data and lack of handling predicates. This paper proposes SafeBound, which is the first practical system to generate cardianlity bounds. SafeBound extends the existing framework with predicates, introduces a practical compression approach for join degree sequences of the relied framework, and implements an efficient inference algorithm. By improving the runtime of expensive OLAP workloads, SafeBound system achieves up to 80% lower end-to-end execution time than PostgreSQL, and is on par or better than the SOTA ML-based cardinality estimators as well as pessimistic ones. It also saves up to 500x in query optimization time and 6.8x in space overhead compared than SOTA cardinality estimation methods.

### Sections :

Cardinality Bounding Problems

Degree Sequence

Degree Sequence Bound

Overview of SafaBound

Extend with prodicates

Vaild Expression

Fast Computation of Cardinality Bounds

Discussion with More Complex Join 

Optimization

Limitations

Experimental Evaluation




### Introduction :

### Conclusion :

## Answer 5C

### Category :

### Context :

### Correctness :

### Contributions :

### Clarity :


# Second Pass

## Related Papers


# Third Pass

## Re-Implement The Paper