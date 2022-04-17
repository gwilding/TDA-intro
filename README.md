# Intro to Topological Data Analysis

In this notebook I'll briefly outline a few basic concepts of TDA. A much more detailed discussion can be found in the book by Edelsbrunner & Harer (2010): [**Computational Topology: An introduction**](https://books.google.nl/books?id=LiljEAAAQBAJ&lpg=PP1&ots=JbpA1elQR6&dq=Computational%20Topology%3A%20An%20Introduction&lr&pg=PP1#v=onepage&q=Computational%20Topology:%20An%20Introduction&f=false). I will make use of alpha complexes, and do the computations with [Gudhi](http://gudhi.gforge.inria.fr/).

Alpha-complexes allow one to construct connected shapes from point clouds, and subsequently analyse their structure, form, and shape. They are closely linked to [Voronoi diagrams](https://en.wikipedia.org/wiki/Voronoi_diagram) and [Delaunay triangulation](https://en.wikipedia.org/wiki/Delaunay_triangulation). In a Voronoi diagram (see the figure below) space (or a plane, as in the figure) is partitioned into cells, where each cell is the region closest to the *seed* (or generator) of this region. These cells are called *Voronoi cells*.

<figure>
    <img src="./figures/Euclidean_Voronoi_diagram.svg" alt="Voronoi cells" width=400>
    <figcaption>Voronoi cells. <a href="https://commons.wikimedia.org/wiki/File:Euclidean_Voronoi_diagram.svg">Author: Balu Ertl</a></figcaption>
</figure>

## Delaunay triangulations

The Voronoi diagram of a set of points is the *dual* of the Delaunay triangulation of these points (meaning there is a one-to-one correspondence between the two). This can be seen in the figure below, with the Voronoi cells (red lines) of a set of black points, and the corresponding Delaunay triangulation of the black points. If two black points are connected via an edge of the (black) Delaunay triangulation, the corresponding Voronoi cells also touch along an edge. The Delaunay triangulation can also be referred to as a Delaunay complex.

<figure>
    <img src="./figures/Delaunay_Voronoi.svg" alt="Voronoi cells" width=400>
    <figcaption>Voronoi cells and Delaunay triangulation. <a href="https://commons.wikimedia.org/wiki/File:Delaunay_Voronoi.svg">Author: Nü Es</a></figcaption>
</figure>


## Alpha shape or alpha complex

An alpha shape is a *filtered* sub-complex of the Delaunay complex. To construct it we choose a value $\alpha$, construct a set of balls centred on the seed points, and then form connections according to the merging balls. This is illustrated in the figure below.

![Alpha complex (generated using this notebook)](./figures/alpha_complex1.png)

## TDA

Topological data analysis now allows us to analyse the structure and shape of these objects through tracking multi-dimensional holes. These multi-dimensional holes can be imagined as being surrounded by loop. I illustrate this in the following figure, where I'm showing a sphere and a torus. Both are hollow, and both contain a hole at their centre. This is essentielly a **two-dimensional hole**, as it can be contained by a two-dimensional manifold (in this case, the surfaces of the sphere and the torus).

The torus also contains **one-dimensional holes**: They are outlined as the two coloured bands on its surface: one through the central hole, and one around its equator. All of the above examples are "holes" in the sense that they can't be closed without breaking the (suface of) the objects - just by shifting them around (like rubber bands) we can not merge them into a point. If we tried putting two different rubber bands on the surface of the sphere, we would first notice that we can transform the first into the second, and then that, in fact, we can collapse it into a point. The surface of a sphere therefore does not contain any one-dimensional holes like the torus.

Finally, there are also the rather abstractly phrased **zero-dimensional holes**: Both objects consist of a single connected component, and the holes we can count would correspond to gaps in the structure. For example, the sphere and the torus are *not* connected, and therefore separated by such a gap. We can use this behaviour to look into clustering characteristics of structures.

The number of $k$-dimensional holes is referred to as the $k$th-Betti number $\beta_k$, and quantifies the topology of a structure. Via the alpha complexes illustrated above we can obtain a structure from a point cloud, and see how its topology changes when we change the parameter alpha. Changing alpha will change the number of holes in a structure. We will look at this more closely in the notebook.

![Sphere and Torus](./figures/sphere_torus.png)
