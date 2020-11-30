# 2020hemibrain (name to be changed) examples
This repo example code for Schlegel, Bates et al. (2020) (link). 

## Relevant libraries
### R 

### Python
#### navis
[navis](https://navis.readthedocs.io/en/latest/) (*n*euron *a*nalysis and *vis*ualization) is the Python equivalent of R's
[nat](https://natverse.github.io/nat/) and a lot of the other packages are built on top of it. It handles data representing neurons, such as 
skeletons or meshes, and lets you analyze and manipulate it. `navis` has a [quickstart](https://navis.readthedocs.io/en/latest/source/tutorials/quickstart.html) 
guide, an extensive [API documentation](https://navis.readthedocs.io/en/latest/source/api.html) and several 
[tutorials(https://navis.readthedocs.io/en/latest/source/gallery.html) including one to fetch hemibrain data via neuprint. `navis` also provides an interfaces with R natverse functions for example `nat.nblast` or `xform_brain` (see tutorials)

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

### Python
