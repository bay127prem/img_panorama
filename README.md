# Creating a panorama from multiple images

In the context of creating a panorama from multiple images, each image can be considered as a node in a graph, and the transformation from one image to another can be considered as an edge. The weight of each edge can be determined by the quality of the transformation which is the number of inliers after applying a RANSAC algorithm for homography estimation.

A Maximum Spanning Tree is a subset of the edges of a connected, edge-weighted undirected graph that connects all the vertices together, without any cycles and with the maximum possible total edge weight. 

When creating a panorama, we want to use the transformations that are the most reliable, i.e., the ones with the highest weights (or the highest quality). By constructing a maximum spanning tree, we are ensuring that we are using the most reliable transformations to stitch the images together, because the MST will include the edges with the highest weights.

This approach also avoids cycles, which could lead to inconsistencies in the transformations. For example, if we have a cycle of transformations that takes us from image A to image B, then to image C, and then back to image A, the final transformation might not perfectly align with the original image A due to errors in the transformations. By using a MST, we avoid such cycles and thus avoid these potential inconsistencies.
