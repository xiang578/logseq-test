---
public: true
file: [Interpreting Trajectories from Multiple Views_2022_Chen.pdf](file:///Users/xry/Dropbox/zotero-lib/Interpreting Trajectories from Multiple Views_2022_Chen.pdf)
file-path: file:///Users/xry/Library/CloudStorage/Dropbox/zotero-lib/Interpreting Trajectories from Multiple Views_2022_Chen.pdf
title: hls__Interpreting Trajectories from Multiple Views_2022_Chen
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

most of them decompose a trajectory into several segments and then compute the travel time by integrating the attributes from all segments
ls-type:: annotation
hl-page:: 1
hl-color:: blue
multi-view trajectory representation
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
a segment encoder is developed to capture the spatio-temporal dependencies at a fine granularity
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
n adaptive self-attention module is designed to boost performance
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
o characterize the natural trajectory structure consisting of alternatively arranged links and intersections
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
realize a tradeoff between the multi-view spatio-temporal features
ls-type:: annotation
hl-page:: 1
hl-color:: yellow
[:span]
ls-type:: annotation
hl-page:: 2
hl-color:: green
[:span]
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
traditional ETA algorithms mainly employ the divide-and-conquer strategy by representing a trajectory as a segment sequence and then summing up the local predictions
ls-type:: annotation
hl-page:: 1
hl-color:: blue
segment-view representation is artificially produced to capture the fined-grained local traffic conditions, which is however not comprehensive in characterizing the natural structure of the road network
ls-type:: annotation
hl-page:: 1
hl-color:: green
preserve static road characteristics, such as pavement type, road width and road functional level
ls-type:: annotation
hl-page:: 1
hl-color:: green
valued information such as the waiting time, the number of traffic lights, and the historical traffic volume
ls-type:: annotation
hl-page:: 1
hl-color:: green
the link- and intersection-views characterize the trajectory attributes from a coarse perspective; a link can be further decomposed into several segments, and hence the segment-view representation models the spatial dependencies at a fine granularity
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
On the one hand
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
However, without explicitly modeling the link-view characteristics, existing studies can hardly model the coherent consistency across segments within the same links.
ls-type:: annotation
hl-page:: 2
hl-color:: red
On the other hand
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
Hierarchical Self-Attention Network for Estimating the Time of Arrival
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
HierETA exploits the hierarchical relationship among the three views to portray the underlying road structure
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
proposed hierarchical self-attention network organizes the segment-, link-, and intersection-views efficiently according to their natural relationships.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
adaptive self-attention network to jointly leverage the global and local patterns for spatio-temporal dependency modeling within the multi-view representation framework.
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
hierarchy-aware attention decoder 
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
GMAN [ 50] employs a graph multi-attention structure to extract the spatial and temporal relationships
ls-type:: annotation
hl-page:: 2
hl-color:: green
graph representation learning generally suffers from the negative impact from irrelevant spatial neighboring regions, resulting in error propagation especially when the involved area grows larger
ls-type:: annotation
hl-page:: 2
hl-color:: green
graph modeling is limited to process only narrow neighboring regions and falls short on developing large-scale urban-wise systems
ls-type:: annotation
hl-page:: 2
hl-color:: yellow
DeepTTE
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
DeepGTT
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
learns the representation of spatio-temporal information using a multi-relational network;
ls-type:: annotation
hl-page:: 3
hl-color:: blue
extracts the travel speed and representation of road network from historical trajectories based on tensor decomposition and graph embedding.
ls-type:: annotation
hl-page:: 3
hl-color:: blue
we design an adaptive self-attention network to explicitly capture the spatio-temporal dependencies of the trajectory using multi-view sequences
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
Attribute Feature Extractor
ls-type:: annotation
hl-page:: 3
hl-color:: yellow
Hierarchical Self-Attention Network for Multi-View Trajectory Representation
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
Hierarchy-Aware Attention Decoder
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
capture the spatiotemporal dependencies of segments in the same link 
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
a local semantic pattern
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
a gating mechanism
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
Joint Link-Intersection Encoder.
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
the joint link-intersection encoder also includes a self-attention layer, a residual connection and a layer normalization
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
as links and intersections appear alternatively
ls-type:: annotation
hl-page:: 4
hl-color:: yellow
coarse-scale representation
ls-type:: annotation
hl-page:: 4
hl-color:: red
t fails to model the consistency shared within the same link
ls-type:: annotation
hl-page:: 4
hl-color:: red
employ two BiLSTMs to respectively encode the links and intersections
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
local pattern 
ls-type:: annotation
hl-page:: 5
hl-color:: red
segment-view context feature that captures the local traffic conditions 
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
joint link-intersection context feature that preserves the common road attributes
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
separately processing each segment without considering the link-view correlation is problematic as it lacks the feedback from the link-view consistency. 
ls-type:: annotation
hl-page:: 5
hl-color:: red
attention guidance that adopts the link-view consistency to further adjust the segment-view attention
ls-type:: annotation
hl-page:: 5
hl-color:: red
we can adaptively select the most relevant features from different representation granularities.
ls-type:: annotation
hl-page:: 5
hl-color:: yellow
travel time estimation is closely related to the critical components
ls-type:: annotation
hl-page:: 5
hl-color:: green
EXPERIMENTS
ls-type:: annotation
hl-page:: 5
hl-color:: green
probability density functions (PDFs) and cumulative distribution functions (CDFs) 
ls-type:: annotation
hl-page:: 5
hl-color:: green
[:span]
ls-type:: annotation
hl-page:: 6
hl-color:: yellow
We repeat each experiment for five times except the statistics-based approach Route-ETA and report the mean and the standard deviation of different runs.
ls-type:: annotation
hl-page:: 6
hl-color:: green
mean absolute error (MAE), root mean squared error (RMSE), mean absolute percentage error (MAPE), and satisfaction rate (SR), similar to existing approaches [ 23 ]. Specifically, SR refers to the fraction of trips with error rates less than 10% and a higher SR indicates better performance and customer satisfaction
ls-type:: annotation
hl-page:: 6
hl-color:: green
[:span]
ls-type:: annotation
hl-page:: 7
hl-color:: yellow
ConstGAT considers the graph structures of the road network to exploit the joint relations of spatio-temporal information.
ls-type:: annotation
hl-page:: 7
hl-color:: blue
[:span]
ls-type:: annotation
hl-page:: 7
hl-color:: green
That is, interpreting the trajectory from multiple views effectively portrays the hierarchical structure of road network and eases the error propagation for estimating the travel time.
ls-type:: annotation
hl-page:: 7
hl-color:: green
window sizes
ls-type:: annotation
hl-page:: 8
hl-color:: green
[:span]
ls-type:: annotation
hl-page:: 8
hl-color:: yellow
he correlation between adjacent segments slightly decreases while the modeling uncertainty increases.
ls-type:: annotation
hl-page:: 8
hl-color:: green
[:span]
ls-type:: annotation
hl-page:: 8
hl-color:: green
The local attention in encoder is removed to verify the effectiveness for modeling the semantic traffic condition.
ls-type:: annotation
hl-page:: 8
hl-color:: green
verify the necessity of extracting the structural traffic pattern.
ls-type:: annotation
hl-page:: 8
hl-color:: green
removing the joint link-intersection encoder
ls-type:: annotation
hl-page:: 8
hl-color:: green
HierETA performs better than both variants that eliminating local and global attentions, which is contributed to the introduction of the global structural and local semantic patterns.
ls-type:: annotation
hl-page:: 8
hl-color:: yellow