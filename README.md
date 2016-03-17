# wp5-infrastructure-design

## Status

We are currently working on the following components in the WP5 (media studies) infrastructure.

**Note**: We are still in the early stages of development and design. The components mentioned below are susceptible to change. We hope to share code and details in the months to come.


### CKAN

To keep an overview of datasets (within media studies/CLARIAH) we have installed [CKAN](http://ckan.org/) registry.
We intend to use this registry to keep track of:
- (relevant) datasets from institutions
- datasets that were enriched/produced using CLARIAH technology

We focus on collections with usable/compatible data first, but also intend to register interesting prospects that could provide a high value for the intended group of (media, digital humanities) researchers.


### APIs

In our architecture we want to supply each component with an API, enabling uniform communication and a convenient way to access components that are distributed among different servers (for e.g. load balancing).

All APIs are implemented using [Flask](http://flask.pocoo.org/) and (probably) will be documented using [Swagger](http://swagger.io/)

Currently we are working on the following APIs:

- The [speech2text API](https://github.com/CLARIAH/wp5-speech2text-api)
- A search API for accessing the Beeld en Geluid catalogue
- A term extraction API for both Named Entity Recognition (NER) and term extraction
- Input validation API to validate whether audiovisual content is ready for further processing or requires transcoding
- Transcoding API interfacing with [FFmpeg](https://www.ffmpeg.org/)

### Processing pipeline

Using [RabbitMQ](https://www.rabbitmq.com/) we are building an processing pipeline that can delegate work to the different APIs. The processing pipeline aims to facilitate researchers in processing data - using one or more of the available APIs. The data provided by the researcher should either reference a dataset registered in CKAN or can be uploaded manually.


### Semantic Web

We are currently generating an "RDF'ized" version of the Beeld en Geluid catalogue.
We use [ClioPatria](http://cliopatria.swi-prolog.org/home) as our triplestore. The catalogue will also be linked with the [GTAA](http://gtaa.beeldengeluid.nl/) thesaurus.


### Central user/identity management

We're currently busy setting up and configuring an [OpenConext](https://openconext.org/) instance for handling all CLARIAH authentication and authorization
