# DBSCAN-
DBSCAN notes

Data is everywhere. How do you know which one constitutes a certain cluster, hence a certain type of behaviour? Density. If the data points are close to each other then they are dense. Density of same clusters are more or less same. Epsilon (e) is such a hyper-parameter which decides the density of each cluster. Epsilon is the same for all the clusters.


Is epsilon enough? In order to determine which data point is which type of data point (core, boundary and outlier), another required hyper-parameter is epsilon neighbourhood (n). Only if the data point has at least a certain number of neighbours, then it is a core point.


Case 1. data point has neighbours >=n : Core object

Case 2. data point has neighbours <n:

Among those neighbours, is any one of them a core object(reachable by core object)? Yes? Border Object

No? Noise


Reachable vs Directly Density-Reachable


If you can reach one point from another point via an epsilon-radius circle, then you are reachable. This is a symmetric relation. But is it directly density reachable? No. To be so, both points have to be core objects.

Only one of them is? Say q and p. q is a core object (q is always assigned to the core object). Then p is directly density reachable from q. q is not directly density-reachable from p.

Neither is? p is not directly density reachable from q. q is not directly density reachable from p.


Density Reachable


- Again not symmetric
- o is directly density reachable from q. (p is epsilon-neighbour of q and q is a core object)
- p (not a requirement to be a core object) is directly density reachable from o. (o is also core object)


But p is not a core object; so the relationship is asymmetric.


Density Connected


Two points a and b (not required to be core objects) can be density connected to each other. Requirement? if there is a core object q such that both a and b are density reachable from q. Remember for them to be density connected, all points in between also have to be core objects.

Density connected but not density reachable


For a and b to be density connected, they need not be core objects.

For a and b to be density reachable by either, one of them have to be core objects.

a to b density connected, but a not density reachable from b and neither is b density reachable from a. A and b are not core objects then.


Density reachable but not density connected

Not possible


For a point to be in a cluster:

It has to be a core object or a border object


For a set S to be called a cluster:

1. Core object or Border object (Density reachable from one point in the cluster)

(All points in set S is density reachable from a core object or is a core object itself)

Note: It cannot be density reachable from a border object. Only from the core object.

1. Density connected to all the objects in the cluster.

(If 2 points are not core objects but is connected to a core object of that cluster)

1. If one of the objects(core objects only, not border objects because it would violate the condition of connectivity) in the cluster has other points in epsilon radius but those points are not in the cluster, then the cluster is incomplete and therefore not a fully formed cluster. (This is the condition for Maximality).




DBSCAN Algorithm:

for i in dataset:

if i ==core object:

i=cluster member

All points(even if they are not core objects) density reachable from i = cluster member

else:

i=noise
