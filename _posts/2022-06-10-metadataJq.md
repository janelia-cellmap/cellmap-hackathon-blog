---
toc: false
layout: post
description: John Bogovic presents metadata standards and translation with jq
categories: [metadata,json,jq,zarr,ome-ngff,transformations]
title: Metadata discussion
image: images/metadata-discussion.png
---

John Bogovic ([@bogovicj](https://github.com/bogovicj)) from the [Saalfeld lab at Janelia](https://www.janelia.org/lab/saalfeld-lab)
gave a demonstration and led a discussion on metadata related topics.

## "Translation" demo and tutorial

Metadata are important in correctly interpreting and processing data, but software often require that these metadata
be formatted in a particular way. Software differ in exactly what the particular way should be.

Metadata "translation" takes metadata formatted in one way and produces the same metadata formatted
in for another. We have found that doing this on-the-fly (without modifying files) is useful, especially 
when modifying the source metadata is not possible or practical.

The demo included:
* A description and demo of the JSON processor [jq](https://stedolan.github.io/jq/).
* Working through [this tutorial](https://github.com/saalfeldlab/n5-ij/wiki/TranslateMetadata#tutorial) for converting between two different N5 metadata "dialects".
  * Pointers to existing [jq helper functions for n5](https://github.com/saalfeldlab/n5-imglib2/blob/master/src/main/resources/n5.jq).
  * See below for the example script we learned from.
* A demonstration of on-the-fly metadata conversion built into [Fiji's N5 plugin](https://github.com/saalfeldlab/n5-ij).
  * Virtually modify the names / paths of datasets using the [n5 container tree](https://github.com/saalfeldlab/n5-ij/wiki/N5-Container-Tree).



## NGFF specification discussion

Next, the group discussed the [coordinate transformation metadata standard](https://github.com/bogovicj/ngff/blob/30cade5073324dd8a5acaec0fa71a592a0c4a3ff/latest/index.bs#L333)
that John is preparing for OME's ["Next generation file formats (NGFF)" specification](https://github.com/ome/ngff/).

Specifically discussed were:
* Current and future [use cases](https://github.com/ome/ngff/issues/84) for the specification.
* The benefits of [defining coordinate systems ("spaces")](https://github.com/ome/ngff/issues/94).
* What [types of transformations](https://github.com/ome/ngff/issues/101) should be included?
* Describing transformations that apply to [a subset of coordinates](https://github.com/bogovicj/ngff/wiki/Subspaces)
  * What name the spec should give to particular transformations<sup>1</sup>.
  * How much is appropriately left implicit for convenience.
  * Thinking about points as [lists](https://github.com/bogovicj/ngff/wiki/Transforms-notes,-examples,-proposals#list-point) or [with structure](https://github.com/bogovicj/ngff/wiki/Transforms-notes,-examples,-proposals#structured-points).


More details about OME-NGFF can be found in the [paper](https://www.nature.com/articles/s41592-021-01326-w), or
in [the specification](https://ngff.openmicroscopy.org/latest/). As well, there is a brief discussion of OME-NGFF
in [John Bogovic's EMBL-Janelia seminar](https://youtu.be/nYzYiXi0sYs?t=1460).


## jq tutorial script

Given the [`n5.jq` helper functions](https://github.com/saalfeldlab/n5-imglib2/blob/master/src/main/resources/n5.jq)
(see [`arrayAndUnitToTransform`](https://github.com/saalfeldlab/n5-imglib2/blob/master/src/main/resources/n5.jq#L57-L65)),
the script:

```
include "n5";
def isN5v: type == "object" and has("pixelResolution");

def convert: .pixelResolution |
    [ [ .dimensions[0], 0, 0, 0,
        0, .dimensions[1], 0, 0,
        0, 0, .dimensions[2], 0 ],
      .unit ]
    | arrayAndUnitToTransform;

walk( if isN5v then . + convert else . end )
```

takes this input:

```json
{
    "pixelResolution": {
        "dimensions": [8, 7, 6],
        "unit": "mm"
    }
}
```

and produces this output:

```json
{
    "pixelResolution": {
        "dimensions": [8, 7, 6],
        "unit": "mm"
    },
    "spatialTransform": {
        "transform":{
            "type": "affine",
            "affine": [8, 0, 0, 0, 0, 7, 0, 0, 0, 0, 6, 0]
        },
        "unit":"mm"
    }
}
```

------------

<sup>1</sup>leading to John's "`identity` crisis"
