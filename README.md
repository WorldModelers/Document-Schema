# World Modelers Document Management
This repository aims to establish a framework for managing documents collected and curated _prior_ to these documents being used by machine reading software. There are 3 primary goals for this effort:

1. Ensure that documents available to readers are consistently structured.
2. Ensure traceability of documents across the World Modelers pipeline.
3. Ensure that World Modeler teams understand the document schema as well as how to access the documents.

## Schema Overview
The `document-schema.json` file contains a [JSON Schema](http://json-schema.org/) for World Modeler documents prior them being processed by machine reading software. This schema file can be loaded to [the JSON Schema tool](https://jsonschema.net/) for for review through a graphical interface.

This schema was collaboratively designed by World Modeler teams at the UAZ hackathon on 6/11/2019. The goal was to create a flexible schema that is extensible to a wide range of document types and use cases, but maintains key information about document provenance.

## Schema Validation
There are numerous schema validation libraries for a variety of programming languages, many of which can be found [here](http://json-schema.org/implementations.html). [`Schema-Validation.ipynb`](https://github.com/WorldModelers/Document-Schema/blob/master/Schema-Validation.ipynb) is a Jupyter Notebook demonstrating validation against this schema using the Python `jsonschema` library.

## Document Processing
Documents can be processed using the [`Document-Processor.ipynb`](https://github.com/WorldModelers/Document-Schema/blob/master/Document-Processor.ipynb) Jupyter Notebook. Ultimately, this processing step should be software, not a notebook, but since currently data curation is manual, not automated, this step requires an engineer-in-the loop to adjust the code to handle new documents. As such, this Notebook provides reference/stub code, not the ultimate document processing solution.

## Document Retrieval
Documents can be retrieved using the [`Document-Retrieval.ipynb`](https://github.com/WorldModelers/Document-Schema/blob/master/Document-Retrieval.ipynb) Jupyter Notebook. This provides an example of querying for or bulk downloading documents using Elasticsearch's Python API. Additionally, Elasticseach has clients in [several other programming languages](https://www.elastic.co/guide/en/elasticsearch/client/index.html).

One thing to note about Elasticsearch is that the JSON document it returns contains top-level Elasticsearch specific metadata, while the actual `document` of interest must be accessed via the `_source` key. However the `_source` does not contain the document `_id`, which is contained at the top-level `_id`. Therefore, for a document to be compliant with [document-schema.json](https://github.com/WorldModelers/Document-Schema/blob/master/document-schema.json) we must extract `_source` and add the `_id` to it.