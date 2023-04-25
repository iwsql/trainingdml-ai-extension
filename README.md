# TrainingDML-AI Extension Specification

- **Title:** TrainingDML-AI
- **Identifier:** <https://stac-extensions.github.io/trainingdml-ai/v1.0.0/schema.json>
- **Field Name Prefix:** trainingdml-ai
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @iwsql

This document explains the fields of The Training Data Markup Language for Artificial Intelligence (TrainingDML-AI)  Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification. Training data plays a fundamental role in Earth Observation (EO) Artificial Intelligence Machine Learning (AI/ML), especially Deep Learning (DL). The TrainingDML-AI Extension provides detailed metadata for formalizing the information model of geospatial machine learning training data. This includes but is not limited to the following aspects: 

·    How the training data is prepared, such as provenance or quality;

·    How to specify different metadata used for different ML tasks such as scene/object/pixel levels; 

·    How to differentiate the high-level training data information model and extended information models specific to various ML applications; 

·    How to introduce external classification schemes and flexible means for representing ground truth labeling.



- Examples:
  - Dota-v1.5 Dataset:
    -  [Item example-Dota-v1.5 Dataset](examples/DOTA-1.5_Dataset/whu_buildings_trainingdata_0000.json): Shows the basic usage of the extension in a STAC Item
    -  [Collection example-Dota-v1.5 Dataset](examples/DOTA-1.5_Dataset/collection.json): Shows the basic usage of the extension in a STAC Collection
  
  - WHU building Dataset:
    -  [Item example-WHU building Dataset](examples/WHU-building_Dataset/item.json): Shows the basic usage of the extension in a STAC Item
    -  [Collection example-WHU building Dataset](examples/WHU-building_Dataset/collection.json): Shows the basic usage of the extension in a STAC Collection
  
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:
- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name           | Type                      | Description |
| -------------------- | ------------------------- | ----------- |
| trainingdml-ai:amount_of_training_data | number              | **Required**, Total  number of training samples in the AI training dataset. |
| traingingdml-ai:updated_time | string | Time when the AI training dataset was updated. |
| trainingdml-ai:metrics_in_LIT       | MetricsInLIT Object | Results of performance metrics achieved by AI/ML algorithms in the peer-reviewed  literature. |
| trainingdml-ai:image_size           | [String]            | Size of the images used in the EO training dataset.          |
| trainingdml-ai:number_of_classes    | number              | Total number of classes in the AI training dataset.          |
| trainingdml-ai:quality              | Quality Object      | Quality description of training datasets.                    |
| trainingdml-ai:data_sources         | [string]            | Citation of data sources.                                    |
| trainingdml-ai:changeset            | Changeset Object    | Changed  training samples between two versions in the collection level. |
| trainingdml-ai:number_of_labels     | number              | Total number of labels in the  individual AI training sample. |

In addition, fields from the following extensions must be imported in the item:

- the [Label Extension Specification](https://github.com/stac-extensions/label) to describe label label of training data.
- the [ML AOI Extension Specification](https://github.com/stac-extensions/ml-aoi) to describe training type of training data.

### Additional Field Information

#### trainingdml-ai:amount_of_training_tata 

Total number of training samples in the AI training dataset.

#### trainingdml-ai:created_time 

 Time when the AI training dataset was created. 

#### trainingdml-ai:updated_time  

Time when the AI training dataset was updated. 

####  trainingdml-ai:metrics_in_LIT 

Results of performance metrics achieved by AI/ML algorithms in the peer-reviewed  literature.  

#### trainingdml-ai:image_size

Size of the images used in the EO training dataset.  The imageSize  is recommended to be expressed in the form of "width\*height". If the imageSize of the training data in dataset is not the same, you can use the imageSize of Smallest size image and the imageSize of largest image to express, such as "minWidth\**minHeight~maxWidth*\*maxHeight".

#### trainingdml-ai:number_of_classes 

Total number of classes in the AI training dataset.

####  trainingdml-ai:number_of_labels 

Total number of labels in the  individual AI training sample.  

#### trainingdml-ai:quality  

Quality description of training datasets. Quality will be aligned with the DQ_DataQuality class in the ISO 19157:2013 spatial data quality model, and the quality assessment metrics for the sample dataset are described using the quality metric classes defined in ISO 19157:2013.

#### trainingdml-ai:data_sources  

Citation of data sources.  

#### trainingdml-ai:changeset

changed  training samples between two versions in the collection level. ChangeSet is used to locate updates to a specific version of a sample dataset by its identifier "datasetId" and version "version".

There are three types of updates for sample data units: "add" for adding new sample data units, "modify" for modifying existing sample data units, and "delete" for removing sample data units. "Modify" includes changes to metadata of sample data, changes to original data used in sample data, and additions, modifications, and deletions of all labeled objects in the sample data.

### metricsInLIT 

This is the introduction for the purpose and the content of the metricsInLIT Object used in field: trainingdml-ai:metricsInLIT.

| Field Name | Type                                          | Description                                                  |
| ---------- | --------------------------------------------- | ------------------------------------------------------------ |
| doi        | string                                        | **REQUIRED**. Digital object identifier of the peer-reviewed literature. |
| algorithm  | string                                        | AI/ML algorithms used in the peer-reviewed literature.       |
| metrics    | [Map<string,  string\|number\|Boolean\|null>] | **REQUIRED**. Metrics and results of AI/ML algorithms in the peer-reviewed literature. |

### quality

This is the introduction for the purpose and the content of the Quality Object used in filed: trainingdml-ai:quality.

| Field Name | Type             | Description                                                  |
| ---------- | ---------------- | ------------------------------------------------------------ |
| scope      | Scope Object     | **REQUIRED**. the scope of quality information is specified. |
| report     | [qualityElement] | Quality reports about the training dataset.                  |

### qualityElement

This is the introduction for the purpose and the content of the qualityElement. Elements related to quality, or more specifically, bias that can be used to reduce the errors when using AI/ML. For example, any knowledge of the TD imbalance and mislabeling can be stored in TD quality.

| Field Name        | Type   | Description                                           |
| ----------------- | ------ | ----------------------------------------------------- |
| type              | string | **REQUIRED**. Type of evaluation quality.             |
| measure           | string | **REQUIRED**. Reference to measure used.              |
| evaluation_method | string | **REQUIRED**. Evaluation information.                 |
| result            | string | Value obtained from applying a data quality measure.. |

### changeset 

This is the introduction for the purpose and the content of the Changeset Object used in filed: trainingdml-ai:changeset. changeset Object records changed training samples between two versions in the collection level, including added training samples, modified training samples and deleted training samples.

| Field Name   | Type                                                         | Description                                                  |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id           | string                                                       | **REQUIRED**. Identifier of the changeset.                   |
| change_count | number                                                       | **REQUIRED**. Total number of changed training samples.      |
| version      | string                                                       | Version of the training dataset that the changeset belongs to. |
| createdTime  | date                                                         | Created time of the changeset.                               |
| add          | [[linkObject](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md#link-object)] | Added training samples.                                      |
| modify       | [[linkObject](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md#link-object)] | Modified training samples.                                   |
| delete       | [[linkObject](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md#link-object)] | Deleted training samples.                                    |

## Best Practices

### Core and other extensions fields

It is higly recommended to use the following fields to describe the training dataset:

| Field name                                                   | TrainingDML-AI usage                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [providers](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md#provider-object) | People or organizations who provide the AI training dataset. |
| [label: overviews](https://github.com/stac-extensions/label/blob/main/README.md#label-overview-object) | Statistics results of training samples in each class.        |
| [label: classes](https://github.com/stac-extensions/label/blob/main/README.md#class-object) | **REQUIRED**. Classes used in the AI training dataset.       |
| [label: tasks](https://github.com/stac-extensions/label/blob/main/README.md#item-properties) | **REQUIRED**. Type description of the EO task.               |
| [label: methods](https://github.com/stac-extensions/label/blob/main/README.md#item-properties) | Methods used in the labeling procedure.                      |
| [ml-aoi: split](https://github.com/stac-extensions/ml-aoi#item-properties-and-collection-fields) | Training type of the individual AI.                          |
| [eo: bands](https://github.com/stac-extensions/eo#band-object) | Description of the image bands used in the EO training dataset. |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
