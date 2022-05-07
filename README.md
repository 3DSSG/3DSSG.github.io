# 3DSSG: 3D Semantic Scene Graphs

3DSSG provides 3D semantic scene graphs for [3RScan](waldjohannau.github.io/RIO). A semantic scene graph is defined by a set of tuples between nodes and edges where nodes represent specific 3D object instances in a 3D scan. Nodes are defined by its semantics, a hierarchy of classes as well as a set of attributes that describe the visual and physical appearance of the object instance and their affordances. The edges in our graphs are the semantic relationships (predicates) between the nodes such as `standing on, hanging on, more comfortable than` or `same material`.

In summary, our dataset features 1482 scene graphs with 48k object nodes and 544k edges.

### Paper
If you find the data useful please consider citing:

```
@inproceedings{3DSSG2020,
    title={Learning 3D Semantic Scene Graphs from 3D Indoor Reconstructions},
    author={Wald, Johanna and Dhamo, Helisa and Navab, Nassir and Tombari, Federico},
    booktitle={Conference on Computer Vision and Pattern Recognition (CVPR)}, 
    year={2020}
}
```

```
@inproceedings{RIO2019,
    title={RIO: 3D Object Instance Re-Localization in Changing Indoor Environments},
    author={Wald, Johanna and Avetisyan, Armen and Navab, Nassir and Tombari, Federico and Niessner, Matthias},
    booktitle={International Conference on Computer Vision (ICCV)},
    year = {2019}
}
```

## Data Organization

The data in the provided *.zip files is organized as follows:
```
[3DSSG.zip](http://campar.in.tum.de/public_datasets/3DSSG/3DSSG.zip)
|-- objects.json
    List of all object instances (nodes) of our semantic graphs
|-- relationships.json
    List of all semantic relationships (edges) of our semantic graphs
|-- affordances.txt
    Provides affordances for each of the 528 classes
|-- attributes.txt
    List of all 93 attributes together with their category
|-- classes.txt
    List of all 528 classes in 3RScan with corresponding lexcial description
|-- relationships.txt
    List of all 41 relationsihps
|-- wordnet_attributes.txt
    Extracted lexcial attributes of each of the 528 classes
```

## Data Formats

The following are overviews of the data formats used in 3DSSG:

**Object instances (nodes) (`objects.json`)**:

```javascript
{
  "scans": [
    {
      ...
    },
    {
      "scan": "531cff10-0021-28f6-8f94-80db8fdbbbee", // scan id from 3RScans scan
      "objects": [
        {
          "global_id": "6", // global instance id from 3DSSG.zip/classes.txt
          "id": "1", // instance id from 3RScans semseg.json
          "label": "floor",
          "ply_color": "#aec7e8", // ply color from 3RScans labels.instances.annotated.ply
          "affordances": [ "placing items on", "walking on" ],
          "attributes": {
            "texture": [ "tiled" ],
            "lexical": [ "inside", "lower", "horizontal" ],
            "color": [ "brown" ],
            "material": [ "ceramic" ],
            "shape": [ "flat" ]
          }
        },
        {
          "global_id": "8",
          "id": "30",
          "label": "plant",
          "ply_color": "#8c9965",
          "affordances": [ "watering", "moving" ],
          "attributes": {
            "other": [ "nonrigid" ],
            "size": [ "big" ]
          }
        },
        {
          "global_id": "10",
          "id": "33",
          "label": "table",
          "ply_color": "#78b980",
          "affordances": [ "placing items on", "cleaning", "carrying" ],
          "attributes": {
            "shape": [ "rectangular" ],
            "color": [ "brown" ],
            "material": [ "wooden" ]
          }
        }, 
        {
          ... 
        }
      ]
    }
  ]
}
```

**Object relationships (edges) (`relationships.json`)**:

```javascript
{
  "scans": [
    {
      "relationships": [
        [
          8,  // object: instance id from 3RScans semseg.json and objects.json objects["id"]
          1,  // object: instance id from 3RScans semseg.json and objects.json objects["id"]
          15, // relationships id (from 3DSSG/relationships.txt)
          "standing on" // semantic relationship (from 3DSSG/relationships.txt)
        ],
        [ 9, 1, 14, "attached to" ],
        [ 11, 14, 10, "higher than" ],
        [ 35, 34, 13, "same as" ], 
        ...
      ],
      "scan": "531cff10-0021-28f6-8f94-80db8fdbbbee"
    }, { 
      ... 
    }
  ]
}
```

## Subset Data

Additional files used for validation and training our networks can be found in 3DSSG_subset.zip.

```
[3DSSG_subset.zip](http://campar.in.tum.de/public_datasets/3DSSG/3DSSG_subset.zip)
|-- relationships.json
    Subset of the semantic relationships (edges) of our semantic graphs used for training
|-- relationships_validation.json
    Splitted graphs with subset of the semantic relationships (edges) used for validation
|-- relationships_train.json
    Splitted graphs with subset of the semantic relationships (edges) used for training
|-- classes.txt
    Subset of 160 classes used for training
|-- relationships.txt
    Subset of 27 relationships used for training
```

### Notes:
* Please see our [project page](https://3DSSG.github.io) for more information.
* Our retrieval setup can be found [here](https://campar.in.tum.de/public_datasets/3DSSG/retrieval.zip)
