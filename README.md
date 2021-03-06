<p align="center">
<img src="https://github.com/flyconnectome/2020hemibrain_examples/blob/main/images/hemibrain.png?raw=true" width="400">
</p>

# 2020hemibrain examples
This repository stores example code for [Schlegel, Bates et al. (2020)](https://www.biorxiv.org/content/10.1101/2020.12.15.401257v1). Here we describe tools in both R and python to work with connectome data for the adult fly brain. This is principally the dense [Janelia FlyEM hemibrain connectome](https://www.janelia.org/project-team/flyem) project, but also sparse connectomic reconstructions from the [full adult female brain (FAFB) dataset](https://neuropil.janelia.org/tracing/fafb/v14/).

<p align="center">
<img src="https://github.com/flyconnectome/2020hemibrain_examples/blob/main/images/hemibrain_to_FAFB.png?raw=true" width="700">
</p>

If you encounter any issues or have questions, please don't hesitate to open an issue.

## Relevant libraries
### R
#### the natverse
The [natverse](https://github.com/natverse) is an ecosystem of R tools for neuroanatomy [(Bates & Manton et al. 2020)](https://elifesciences.org/articles/53350). It is essentially a collection of interoperable R packages to import, visualise, analyse, manipulate and export 3D neuroanatomical data, including neurons, brains and brain regions. It has been used to study brain and circuit organisation in species from flies to fish and mice. These R package allow you to do general neuron analyses, and enable you to move data between different fly brains. The key generalist package in this ecosystem is `nat` (the **n**euro**a**natomy **t**oolbox). Importantly, the natverse contains the following packages:

##### rcatmaid
This [catmaid](http://natverse.org/rcatmaid/) package provides access to the [CATMAID](https://catmaid.readthedocs.io/en/stable/) API for R users. At present it provides low level functions for appropriately authenticated GET/POST requests, optionally parsing JSON responses. There are also intermediate level functions that retrieve skeleton (i.e. neuron) information, connectivity information for one or more neurons as well as a number of other API endpoints. In the context of our paper, it was used to access manual neuron reconstructions from [FAFB dataset](https://neuropil.janelia.org/tracing/fafb/v14/), some of which was original tracing for this work (hemilineage morphology comparisons) and much of which we have already reported [(Bates & Schlegel et al., 2020)](https://www.sciencedirect.com/science/article/pii/S0960982220308587). You will need a user name, password and unique token to access some CATMAID instances, e.g. there is a [private FAFB instance](https://neuropil.janelia.org/tracing/fafb/v14/), and a [public one](https://catmaid-fafb.virtualflybrain.org/) (no credentials required) for the same data, but with fewer reconstructions.

##### fafbseg
The goal of the [fafbseg package](http://natverse.org/fafbseg/) is to provide support for analysis of segmented EM data. This includes support for working with neuroglancer mesh data for the [FAFB dataset](https://pubmed.ncbi.nlm.nih.gov/30033368/). In particular there is support for the [FlyWire](https://ngl.flywire.ai/?local_id=0405d158a8adf61ef9013563b65a3535) and [Google brain automatic segmentations](https://www.biorxiv.org/content/10.1101/605634v1) of FAFB data.

##### neuprintr
The goal of [neuprintr](https://github.com/natverse/neuprintr) is to provide R client utilities for interacting
with the neuPrint connectome analysis service. neuPrint is set of tools
for loading and analysing connectome data into a Neo4j database. You can
find [neuprint](https://github.com/connectome-neuprint/neuPrint) on
Github. The main focus is analysis of the
[hemibrain](https://www.janelia.org/project-team/flyem/hemibrain),
densely reconstructed adult Drosophila brain dataset available [here](https://neuprint.janelia.org/).
For more information, have a look [here](https://neuprint.janelia.org/help).

##### hemibrainr
The goal of [hemibrainr](https://github.com/natverse/hemibrainr) is to provide useful code for preprocessing and
analysing data from the [Janelia FlyEM
hemibrain](https://www.janelia.org/project-team/flyem) project. It contains specific functionality for splitting neurons into axons and dendrites, including split edgelists for connectivity. It also has the capability to load large amount of precomputed data on flywire, FAFB and hemibrain neurons from a linked Google drive. Please see [this article](https://flyconnectome.github.io/hemibrainr/articles/google_filestream.html).

### Python
#### navis
[navis](https://navis.readthedocs.io/en/latest/) (*n*euron *a*nalysis and *vis*ualization) is the Python equivalent of R's
[nat](https://natverse.github.io/nat/) and a lot of the other packages are built on top of it. It handles data representing neurons, such as
skeletons or meshes, and lets you analyze and manipulate it. `navis` has a [quickstart](https://navis.readthedocs.io/en/latest/source/tutorials/quickstart.html)
guide, an extensive [API documentation](https://navis.readthedocs.io/en/latest/source/api.html) and several
[tutorials](https://navis.readthedocs.io/en/latest/source/gallery.html) including one to fetch hemibrain data via neuprint. `navis` also provides an interfaces with R natverse functions for example `nat.nblast` or `xform_brain` (see tutorials)

#### pymaid
[pymaid](https://pymaid.readthedocs.io/en/latest/) is a library that lets you interact programmatically with a CATMAID server: fetch neurons, add/remove
annotations or query connectivity, to name but a few.

#### fafbseg-py
[fafbseg](https://fafbseg-py.readthedocs.io/en/latest/) is analogous to the R package of the same name: an ever evolving library containing various
functions to interact with the auto-segmented data available for the FAFB data set. At the moment, this is data from the Seung lab at Princeton (hosted
on _flywire_) and Peter Li at Google (hosted e.g. as skeletons in the CATMAID autoseg instances). Functions to query the Buhmann et al. FAFB synapse
data will soon be added too.

#### neuprint-python
[neuprint-python](https://connectome-neuprint.github.io/neuprint-python/docs/) is a Python client developed and maintained by Stuart Berg (HHMI Janelia
Research Campus) that allows you to programmatically query the hemibrain connectome hosted on https://neuprint.janelia.org/. `navis` wraps this library
and adds a few convenience functions to fetch hemibrain data.

## Code Examples
### R
#### Authorisation with neuPrint
`examples/R/authorisation.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/authorisation.Rmd)
how to connect your R session to neuPrint so you can read data from the connectome analysis service.

#### Make a custom query with neuprint
`examples/R/customquery.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/customquery.Rmd)
neuPrint includes both an [API](https://neuprint.janelia.org/help/api) which
provides a range of queries as well as the option to send custom queries
written in the [Cypher query language](https://neo4j.com/developer/cypher-query-language/)
of the [Neo4j](https://neo4j.com) graph database. It is probably worth making queries via the API if they will solve your problem.
However custom queries offer maximum flexibility.

#### Work with antennal lobe projection neurons from neuprint
`examples/R/hemibrain_opns.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/hemibrain_opns.Rmd)
use `neuprintr` to pull morphology and synaptic data for hemibrain antennal lobe projection neurons from neuprint, and perform basic analyses.

#### Examine connectivity for antennal lobe receptor neurons
`examples/R/hemibrain_opns.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/hemibrain_alrn_connectivity.Rmd)
use `hemibrainr` to work with data and meta data related to ALRNs and the glomeruli they innervate.

#### Axon and dendrite splits for neurons
`examples/R/hemibrain_axons_dendrites.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/hemibrain_axons_dendrites.Rmd)
use `hemibrainr` to pull morphology and synaptic data for hemibrain neurons and split them, and their connectivity, into axon their axon and dendrite compartments. This split has been overlooke in Drosophila neuroscience to date but it likely to be crucial in understaning the role of neurons in  circuits.

#### Examine ALPN connectivity to their downstream targets
`examples/R/hemibrain_alpns_toons.Rmd`
[link](https://github.com/flyconnectome/2020hemibrain_examples/blob/main/examples/R/hemibrain_alpns_toons.Rmd)
use `hemibrainr` to pull connectivity information, which is broken down by axon and dendrite. Use this and other metadata to build a complex heatmap describing the connectivity of ALPN axons onto their downstream targets, deeper in the brain.

### Python
#### Olfactory Layers - Network Traversal
`examples/Python/1_network_traversal_model.ipynb` [link](examples/Python/1_network_traversal_model.ipynb)
showcases the network traversal model used to sort neurons into layers with respect to the olfactory system.

#### ALLN morphology
`examples/Python/2_ALLN_typing_morphology.ipynb` [link](examples/Python/2_ALLN_typing_morphology.ipynb)
contains basic analysis of antennal lobe local neurons (ALLNs).

#### AL glomeruli meshes
`examples/Python/3_glomerul_meshes.ipynb` [link](examples/Python/3_glomeruli_meshes.ipynb)
demonstrates generating meshes from synapses clouds.

## Issues?
If you run into errors or something is not working, please open an issue and we'll try to help asap.

## Acknowledging the tools

The R packages were principally created by [Alexander Shakeel Bates](https://scholar.google.com/citations?user=BOVTiXIAAAAJ&hl=en) and [Gregory Jefferis](https://en.wikipedia.org/wiki/Gregory_Jefferis) with Romain [Franconville](https://scholar.google.com/citations?user=I7yBLlsAAAAJ&hl=en)
now providing key contributions. You can get R package citations like this:

```{r citation, eval = FALSE}
citation(package = "package_namr")
```

## Acknowledging the data

* **The hemibrain connectome (hemibrain:v1.1)**: Scheffer, L.K., Xu, C.S., Januszewski, M., Lu, Z., Takemura, S.-Y., Hayworth, K.J., Huang, G.B., Shinomiya, K., Maitlin-Shepard, J., Berg, S., et al. (2020). A connectome and analysis of the adult Drosophila central brain. eLife 9. [doi: https://doi.org/10.1101/2020.05.29.080473](https://doi.org/10.1101/2020.05.29.080473)
