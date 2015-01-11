# Data API

The Guggenheim Helsinki open anonymous architecture competition attracted 1,715 entries from 77 countries, the largest in history. The Solomon R. Guggenheim Foundation has published some images and text of all submissions through an [online gallery](http://designguggenheimhelsinki.org/stageonegallery/), and through the API publishes the full data set of submissions.

This README file documents the contents available through the API and where to find them.


## Roadmap

Version 1 (`v1`) of the API publishes the full submission content as it was submitted by competition entrants in PDF and JPG files. As the competition is anonymous, each entrant was given a random unique identifier (`id`) and was instructed to only refer to their submission through this identifier. API `v1` publishes the three parts of each entry at a common endpoint arranged in directories named for their identifier (see the URI Structure section below for details). Version 1 only presents a simple `GET` option for the content and some static `.json` files as a directory to find the published files.

Subsequent versions may improve upon the accessibility of the documents, their formats and other common API functionality. Updates will be made here if and when new versions are made available.


## Content

Each `submission` consists of three `parts`:  

* `partA` is an A4-format PDF document containing a 500-word explanation of the design concept.
* `partB` is a 4-page A1-format PDF document containing numbered boards that represent the key project criteria. Each board establishes the competitor’s approach. Boards may contain a mix of media such as drawings, words, sketches, photos, and visualizations.
* `partC1` and `partC2` are each individual images taken from boards that the submitters have selected to be representative of their projects.
* `partC3` is an A4-format PDF document containing a 150-word summary of the design concept.

As the data set will likely evolve over time, each of these parts have been broken down by file type and hashed according to descriptive titles for the purposes of API calls. This mapping is articulated in the `key.json` file which links the descriptions of each document with its presentation in the data schema as given in `directory.json`, discussed below.


## URI Structure (where to find the content)

The URI structure may evolve over time but will remain backwards compatible so links will not be broken.

The content will be served through the Amazon cloud and will be accessible through an endpoint that takes the form of `domain.com/version/directory/id/filename.ext` where:  

* `domain.com` is where the data is stored: `https://s3-us-west-2.amazonaws.com/api.designguggenheimhelsinki.org/`
* `version` is the version you wish to access. For version 1 it is: `v1`
* `directory` is where the data is stored. For version 1 it is: `data`
* `id` is the unique identifier of the submission in the form of `GH-XXXX`, where XXXX is a random number that ranges between 8-12 digits
* `filename` is constructed of the id and the part of the submission being requested separated by dashes, such as `GH-XXXX-partA`
* `ext` is the file extension


## Data Schema: Identifiers and the Directory

To access the published content, a list of identifiers has been provided in `.json` format. As the identifiers are random, there is no possibility to build a sequencing loop to find them all efficiently, they need to be pulled from the given array.

The identifiers are listed in the `identifiers.json` file as a simple array. There are a total of 1715. To access the files, the content of this document will have to be combined with the URI structure pattern to cycle through all identifiers and construct the live URLs of each desired file.

Alternatively, the `directory.json` file can be used to access the files. This document provides URLs to each file explicitly and may later be used to present additional metadata about each submission. Subsequent versions of the API will likely present an interface similar to that of this document once a full database is in place.

**Note: the `directory.json` file will be uploaded shortly.

## Accessing the Data

In order to access the data, each file URL must be constructed using the information above. An example in HTML/Javascript has been provided in the `/examples` folder and can be inspected online [here](https://s3-us-west-2.amazonaws.com/api.designguggenheimhelsinki.org/v1/examples/index.html).

An example URL will look like:
`https://s3-us-west-2.amazonaws.com/api.designguggenheimhelsinki.org/v1/data/GH-03631231/GH-03631231-partC1.jpg`

The `directory.json` file can also be found online at:
`https://s3-us-west-2.amazonaws.com/api.designguggenheimhelsinki.org/v1/directory.json`


## Feedback, Questions, Comments

Please get in touch with us at [helsinki@guggenheim.org](mailto:helsinki@guggenheim.org) for any feedback or special requests.
