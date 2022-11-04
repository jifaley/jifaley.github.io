#神经元群落追踪Metric
by jifaley


##如何对齐不同神经元


###G-cut的Metric

Miss-Extra Score(MES)
`Xie2011_Anisotropic path searching for automatic neuron reconstruction`
$$
MES=\frac{S_G-S_{miss}}{S_G+S_{extra}}
$$
>where $S_G$ is the total length of all segments in the ground-truth trace, $S_{miss}$ and $S_{extra}$ is the total length of missing and extra segments in the automatic trace, respectively. MES provides a global measurement on how many parts of the neuron have been traced and how many undesired components are introduced by the automatic tracing algorithm.

试图将test和gold重建的点进行1-1匹配，然后计算匹配、失配的点的数量。有可能会对较密集或者较稀疏的重建有偏见。

###DIADEM Metric

`https://diadem.janelia.org/metric.html`

同样也是首先匹配test重建和gold重建之间的点，匹配机制比较复杂。貌似是gold这边的点比较重要。

###NeuroGPS-Tree的Metric


分别计算test和gold上的True Positive点(如果对面最近的点距离<8µm,则算TP)。

$$
Precision = \frac{TP_{test}}{ALL_{test}}
$$
$$
Recall = \frac{TP_{gold}}{ALL_{gold}}
$$

>The recall rate, precision rate and DIADEM score of the neuronal population reconstruction were calculated using the weighted average of the recall rate, the precision rate and the DIADEM score of the reconstructions of neuronal trees with many neurites, in which the weight was proportional to the total length of the neuronal processes of an individual neuron identified in the manual reconstruction.

Precision、Recall和DIADEM都是加权的,权重是gold重建中每个单独神经元的总长度。

###PLNPR的Metric

与NeuroGPS-Tree的相同，添加了F-score和Jaccard两项。
PLNPR实际上是对数据增强后使用NeuroGPS-Tree。
