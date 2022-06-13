---
toc: true
layout: post
description: A breif intoduction to all the hackathon attendees.
categories: [markdown]
title: Meet the attendees
---
# Meet the hackathon attendees

## David Ackerman [@davidackerman](https://github.com/davidackerman)
I am a software engineer/data analyst interested in teasing out useful information from complex datasets, regardless of domain. I went from computational astrophysics research in undergrad, to experimental and computational membrane biophysics research in grad school, to software engineering at Janelia. As a member of Scientific Computing at Janelia, I have worked on a variety of projects involving large-scale image processing and analysis, including FlyEM and CellMap, where my work has ranged from image alignment to segmentation analysis. I look forward to learning about what everyone else works on, and getting more involved on the machine learning side of things.

## Diane Adjavon
Brand new machine learning researcher at Janelia with a focus on computer vision tools for better microscopy annotation. I worked on predicting fluorescence from bright-field images in grad school, where I learned the importance of human interpretation and interaction on performance, both qualitatively and quantitatively.
During the hackathon I’m hoping to dive into the possibilities for human-machine interaction for better training, combining fine-tuning and transfer learning, annotation tools, and active learning.

## Davis Bennett [@d-v-b](https://github.com/d-v-b)
I’m a data engineer in the CellMap project team. I work on our data sharing site ([OpenOrganelle](https://www.lee.hms.harvard.edu/)) and our general data storage strategy. My “wish list” currently includes:
- standardize our spatial metadata / project storage layout to something community-driven (e.g. OME-NGFF)
- Implement a backend for our ML models such that they present their output as a lazy chunked data source that can be viewed with chunk-friendly visualization tools (neuroglancer, bigdataviewer)
- Get the aforementioned backend running on aws
- Easy lossy image compression for zarr / n5 arrays (e.g., jpeg)
- Make multiresolution pyramids on GPUs

## John Bogovic [@bogovic](https://github.com/bogovicj)
Computer scientist in the Saalfeld lab whose research focuses primarily on image registration, especially inter-modality (e.g. CLEM). Develops and maintains BigWarp, and contributes to imglib2, bigdataviewer, and n5. Denizen of forum.image.sc. During the hackathon, I plan to continue developing a OME-NGFF’s standard for coordinate transformations, and hope to hear about everyone’s approaches to data wrangling, with an eye to using metadata to make our coding lives happier.

## Genevieve Buckley [@GenevieveBuckley](https://github.com/GenevieveBuckley)
Scientist and programmer from CryoEM facility at Monash University in Melbourne, Australia. Maintainer for [dask-image](https://www.lee.hms.harvard.edu/) and [napari](https://www.lee.hms.harvard.edu/). 
Possible projects (let me know if you want to team up on anything, or have your own project idea you’d like to work on together):
- Training and prediction on large CryoEM volumes
    - Priority: Our facility wants to do organelle prediction (especially for FIBSEM datasets), following in the footsteps of [Heinrich et al.](https://www.nature.com/articles/s41586-021-03977-3)
- Annotation tools
    - Paintera (I’m new to painters, but would like to use it better)
        - Questions: Editing labels generated outside paintera, I can’t erase label areas. (I *can* erase labels drawn in the painters session)
        - Documentation improvements: I’m offering to make tutorial videos
        - Development: I’d like to upgrade the version of JavaFX Paintera uses, so it can run on my M1 Macbook. Some help needed setting up my dev env.
    - Zarpaint napari plugin. annotate directly into a zarr file. 
        - We are currently extending zarpaint to add slice interpolation features, see https://github.com/GenevieveBuckley/slice-interpolation 
- Big data handling
    - dask: `to_n5` function (to match `to_zarr`, `to_parquet`, etc.)
    - dask-image: multi-resolution dataset generator (given a full resolution dataset, compute lower resolutions and save to N5/zarr file)
    - dask-image: switch imread to use imageio instead of pims under the hood

## Ryan Conrad [@conradry](https://github.com/conradry)
I’m a software engineer at the NIH focused on deep learning. Recent projects include the CEM500K and CEM1.5M datasets for unsupervised pre-training and transfer learning, the CEM-MitoLab dataset for training instance segmentation models to detect mitochondria, and the empanada library and corresponding napari plugin for panoptic segmentation of 2D and 3D EM data (especially FIBSEM). Lately, I’ve been transitioning my data pipeline to work with OME-Zarr and am very interested in the associated metadata discussion. Really, all of the projects are interesting to me but ML and annotation tools are near the top of the list. Another topic of interest, that wasn’t mentioned, are methods for integrating existing ML datasets with different label spaces/ontologies in order to train more robust and general models. 

## Draga Doncila Pop [@DragaDoncila](https://github.com/DragaDoncila)
Computer science PhD student from Monash University in Melbourne, Australia, working on an interactive cell tracking annotation and segmentation framework, and napari core developer. I want to learn how current tools allow for interactive annotation on large volumes and how we can improve the standardization of data formats and their metadata for storage, transfer and visualization. 
Our ideal segmentation and tracking solution would be capable of taking natural annotations and corrections on volume sections and using those to predict unseen sections and correct existing ones. We would prefer to keep a relatively simple learning model for feature extraction in favor of a rapid and robust optimization model that can solve on the fly and incorporate human annotations for rapid re-solve.
In general:
- Image data formats and metadata
- Training & prediction on large volumes
- Annotation tools

## Jan Funke [@funkey](https://github.com/funkey)
Computer vision and machine learning researcher at Janelia, working on applications to all sorts of microscopy image analysis. In the context of this hackathon, we are interested in building interactive machine learning methods, which we call "**life-supervised learning**".

A life-supervised machine learning method learns on the fly as a user annotates a volume. It provides incremental updates to so far not annotated areas to either proof-read or accept as-is. In such a system, there is no difference between manual annotation of structures of interest, ground-truth generation, and proof-reading: As an annotator opens a new dataset and starts segmenting structures of interest, a machine learning algorithm is trained in the background to continuously make predictions in so far unannotated areas. Just as for humans, the training of the model is a continuous, life-long process. Over time, the algorithm gradually improves and the annotator transitions from teaching the model to correcting errors made by the model due to model error or data noise. Importantly, and in contrast to conventional pipelines, the training signal for the model is highly focused throughout the whole lifetime: Only structures that were erroneously predicted need to be corrected, and only those corrections are used to refine the model.

Such a system could be realized by splitting the machine learning method into two parts: (1) a slow, high-capacity learner to predict semantically meaningful embeddings, and (2) a fast, low-capacity learner to turn the embeddings into the target (e.g., a semantic segmentation). This separation will allow the system to be:

- **Interactive**: Corrections made by a user should quickly proliferate to other, not annotated areas. This will be realized by the fast, low-capacity learner.
- **Consistently Improving**: the system should keep learning as more annotations are available. This will be realized by the slow, high-capacity learner, which will keep continuously improving the semantic embeddings on all available annotations.
- **Persistent**: User annotations should never be overwritten, even if other, similar structures have been annotated differently. This will be realized by extrapolation from annotated data points (i.e., transductive learning).

## Kyle Harrington [@kephale](https://github.com/kephale)
Computer scientist working as a senior research scientist at Oak Ridge National Lab. 
Web: https://kyleharrington.com 

I have big zarr images on an HPC that need to be segmented, but no ground truth labels. At the hackathon I am cleaning up my workflow for general usage. In this workflow I use napari to interactively paint and train models + predict segmentations in HPC environments. 

Topics of interest:
- Image data formats and metadata
- Backend development
- Scalable ML [networks]
- ML finetuning and transfer learning
- Training and prediction on large volumes
- Annotation tools

## Larissa Heinrich [@neptunes5thmoon](https://github.com/neptunes5thmoon)
I'm a PhD student in the Saalfeld lab working on machine learning problems for volume electron microscopy data. Specifically I have worked on super resolution to improve axial resolution in serial section data and segmentation of synapses and organelles.
I'm interested in developing network architectures that can effectively utilize large receptive fields. Further I'm hoping to work on transfer learning, self-supervised pre-training, finetuning or anything else that might help reduce the amount of training data we need. I also thoroughly enjoy discussions about the ongoing efforts regarding metadata standards.

## Caleb Hulbert
I am a software engineer in the Saalfeld lab, working primarily on Paintera, and helping maintain lab projects. My background was initially in biology, working in both a maize genetics lab, and a computational neuroscience lab in the past, before focusing more on software development. I’m interested in working on annotation tools for this hackathon, and engaging in active learning. I’m also interested in some of the ongoing efforts regarding image data formats and metadata.

## Dagmar Kainmueller [@kainmueller](https://github.com/kainmueller)
I am a computer scientist working on machine learning for image analysis, mainly instance- and panoptic segmentation. Towards generalizable / interactive ML, we’re looking into combining (or unifying?) components like cycleGAN, semi-supervised pipelines like momentum contrast, Bayesian DL, XAI, also RFs for fast user feedback, etc. Also very interested in existing / upcoming infrastructure (we’ve been playing with napari, paintera, ilastik) wondering where and how to best integrate our models

## Dominik Kutra [@k-dominiki](https://github.com/k-dominik)
I’m a research software engineer in Anna Kreshuk’s lab at EMBL Heidelberg. I work on [ilastik](www.ilastik.org), so accessible machine learning is close to my heart. I’m interested in making software easy to use (both for developers and non-coding users) - all aspects from algorithmic performance, UX/API design, deployment. The latter is especially challenging with the neural networks. Other topics I’m interested in:
- Interoperability
- Interactive deep learning

## Caroline Malin-Mayor
I am a computer vision researcher currently getting my PhD at University of Toronto. Previously I was a Scientific Computing Associate working in the Funke lab on cell tracking from sparsely annotated data in large light-sheet datasets of drosophila, zebrafish, and mouse. I am most interested in making this work more accessible to other researchers and end-users, which is challenging due to the size of the datasets and complexity of the algorithm. More generally, this falls under training/prediction on large volumes and backend development, as well as fine tuning the pre-trained models for application to new datasets.

## Tri Nguyen
Hi! I have been a postdoc in the [Lee Lab](https://www.lee.hms.harvard.edu/) at Harvard Medical School for about 4 years now working on segmentation of a cerebellum. Since I came to Janelia in 2018 to work with Jan on Daisy and then the culmination of an analysis of the cerebellum, I have pretty much touched on every aspects of segmentation and am now excited to work on decreasing the cost of segmentation through overcoming imaging defects/misalignments, transfer learning through cyclegan, superresolution, cheap groundtruthing, proofreading, etc. In one particular topic, I am excited to learn and brainstorm with people on how to tackle the issue of continual learning as it is well known in ML world that today's architectures are prone to forget when exclusively presented with novel training samples.

## Wei Ouyang [@oeway](https://github.com/oeway)
I am currently a researcher at Science for Life Laboratory and KTH Royal Insitute of Technology, Stockholm, Sweden.I developed [ImJoy](https://imjoy.io) for building interactive tools using web and python. I am coordinating a collaborative effort of BioImage [Model Zoo](https://bioimage.io) which aims to build a platform for sharing AI models in bioimage analysis. I am responsible for building cloud computing infrastructure to enable test runs of models in the BioImage Model Zoo. I am working on the BioEngine and Hypha for allowing scaling AI models and application serving.

For the hackathon, I am interested in discussing with the CellMap team and others about:
- AI model sharing standard and the BioImage Model Zoo
- Scalable AI model serving (inference and training) in the cloud
- Interactive model training, for collaboration between research groups, public AI challenges or citizen science
- ImJoy, web-based image analysis, web assembly, web based image visualization and annotation

## Will Patton [@pattonw](https://github.com/pattonw)
I am a software engineer / machine learning practitioner interested in tooling and algorithm development for applying machine learning quickly, easily, and efficiently. I did my undergrad in Mathematics and Computational Modeling, and have worked at Janelia since graduating in May 2018. Since joining Janelia I have worked with a couple labs and project groups, most recently as a part of Scientific Computing and the CellMap project team. Of particular interest to me are the model related categories (finetuning/transfer learning, training/prediction on large volumes, scalable ML networks). I am very excited to collaborate with the other participants, and learn from their work.

## Tobias Pietzsch [@tpietzsch](https://github.com/tpietzsch)
I'm a computer scientist working as a freelancer for Scientific Computing at Janelia (among others). I develop and maintain ImgLib2 and BigDataViewer, and contribute to Mastodon, MaMuT, Labkit, etc. I'm interested in all aspects of image processing, analysis, visualization, and storage. (But in practice, I mostly work on tools for interactive visualization and annotation.) For the hackathon, I would like to see what everybody is working on. I would like to learn more about the active learning project, i.e., the big picture and where our tools fit in.
I would also love to do some hacking. Random topic selection:
- support images with masks (alpha/binary) in ImgLib2/BigDataViewer,
- implement HTTP backend for N5
- support HDF5 backend for BDV on Apple ARM64
- finish work on improving BDV UI on HiDPI screens
I'm also willing to dive into OME-NGFF and metadata discussions, if I'm forced to... :smile:

## Stephan Preibisch [@StephanPreibisch](https://github.com/StephanPreibisch)
I am a computer scientist that also worked for some years experimentally with single molecule techniques. The major projects I contributed to so far are ImgLib2, BigStitcher, Render, RS-FISH, STIM and some more. I am the director of Scientific Computing at HHMI Janelia and very interested in reconstruction and analysis of very large (peta-scale) lightsheet and electron microscopy datasets, machine learning, and Open Science Software in general. For the hackathon I would like to get an overview of everyone’s work and would like to contribute to our new active learning project and integrate existing tools such as BigStitcher better with downstream tools for image segmentation.

## Franz Rieger [@riegerfr](https://github.com/riegerfr)
I’m a first year PhD student in Jörgen Kornfeld’s lab working on ML for connectomics. We try to take advantage of the vast amounts of unlabelled data via self supervised pre-training of segmentation models. To give back to the ML community we are aiming to improve the segmentation architectures and we are also working on more biologically plausible self-supervised learning approaches. During the hackathon I would like to explore novel segmentation approaches.

## Konrad Rokicki [@krokicki](https://github.com/krokicki)
I’m the manager of software engineering in Scientific Computing, and I created the Janelia Workstation for FlyLight and MouseLight, for enabling end-user access to large collections of bioimage data sets. Davis, Aubrey and I have discussed prototyping support for CellMap data sets in Workstation. I’ve begun by adding functionality to make remote n5/zarr containers available for browsing in the Workstation, and Davis is working on creating a database for the data set metadata. The next step is for me to integrate BigDataViewer into the Workstation, to be able to quickly view any data set with the click of a button, without the user having to think about file paths or data locality.  During the hackathon, I’d like to benefit from the groups’ collective experience and insight to guide my integration of BDV, and to discuss what other high-level functionality might be useful for further enabling accessibility.

## Stephan Saalfeld [@axtimwalde](https://github.com/axtimwalde)
Computer Scientist interested in image analysis (of neurons and other cells, also any other image data) and open source software.  Really likes the size, dazzling richness, and confusing artifacts of large 3D electron microscopy.  Wrote some parts of ImgLib2, BigDataViewer, Paintera, and a few other open source tools.  Currently group leader at Janelia working on scalable image analysis of large 3D EM data together with CellMap project team and others.  I would love to learn about everybody else’s work and integrate your ideas and tools with our ideas and tools, e.g. have Paintera interactively generate cellular organelle predictions, edit them and start retraining, or interactively use contour predictors to aid manual annotation.

## Deborah Schmidt [@frauzufall](https://github.com/frauzufall) 
Research Software Engineer for Helmholtz Imaging with experience in human computer interaction, data visualization, ImageJ2 / SciJava core development, usability, DevOps, reproducibility. Together with Martin I was part of a team publishing a [whole beta cell reconstruction](https://rupress.org/jcb/article/220/2/e202010039/211599/3D-FIB-SEM-reconstruction-of-microtubule-organelle), including Blender visualizations. I work with Kyle on [Album](https://rupress.org/jcb/article/220/2/e202010039/211599/3D-FIB-SEM-reconstruction-of-microtubule-organelle) for sharing reproducible software solutions via single python files.

Looking forward to meeting people and potentially working on the Label Editor (label visualization based on BDV), integrating the existing beta cell segmentation strategies into Album solutions, compatibility of Album solutions with other frameworks, alo happy to do visualizations and open to other ideas.

## Arlo Sheridan [@sheridana](https://github.com/sheridana)
Machine learning researcher working on various segmentation, restoration and multi-object tracking projects at the Salk Institute. Previously worked in the Funke lab at Janelia on neuron segmentation in large EM volumes. I am interested in generalizable/scalable networks, transfer + active learning, and visualization.

## Aubrey Weigel [@avweigel](https://github.com/avweigel)
I started grad school as a physicist building microscopes to study diffusion of protein channels on the plasma membrane. I then spent my postdoc looking inside the cell at the ER, Golgi, and everything in between. Over time I’ve shifted from using light microscopy to study dynamics in living systems to using electron microscopy to study morphologies and ultrastructure in ‘not-so-living’ systems. I now lead the [CellMap project team](https://www.janelia.org/project-team/cellmap), an evolution of the [COSEM project team](https://www.janelia.org/project-team/cosem), to interrogate the 3D architecture and subcellular structures of cells in tissues using approaches like volume EM, CLEM, and expansion microscopy. Maybe not surprisingly, I’m interested - as both a user and project manager - in all areas of the proposed topics.

## Martin Weigert [@maweigert](https://github.com/maweigert)
I am a computer scientist with an interest in machine learning based image reconstruction and segmentation, as well as the development of open source python tools such as CSBDeep and stardist. I am currently a group leader at EPFL, where my team is focused on developing unsupervised methods for ml-based bioimage analysis and the extension of segmentation methods to different data modalities. For the hackathon, I am (above all) interested in exchange of scientific ideas and discussing fundamental limitations of current approaches (both software and methods wise).

## Marwan Zouinkhi [@mzouink](https://github.com/mzouink)
I started as a software engineer and a mobile developer then I shifted into scaling image analysis for my PHD. Last November, I joined Janelia as part of the Scientific computing team and CellMap project. I am interested in scaling image processing of large multi-dimensional datasets and automatizing image reconstructions. Currently, I am working on a versioned data store service that will be used in the active learning project. During the hackathon I plan to integrate the versioned storage into Paintera and ML applications.
