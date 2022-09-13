# GeoBlacklight Quick Start
This guide covers the quickest way to get up and running with GeoBlacklight, including:

 - How to install GeoBlacklight on your local computer.
 - How to create a new application.
 - How to add and index geospatial content.   

## Installation

  Bootstrap a new GeoBlacklight Ruby on Rails application using the template script:

```bash
DISABLE_SPRING=1 rails new app-name -m https://raw.githubusercontent.com/geoblacklight/geoblacklight/main/template.rb
```
  Then run the `geoblacklight:server` rake task to run the application:

```bash
$ cd app-name
$ bundle exec rake geoblacklight:server
```

* Visit your GeoBlacklight application at: [http://localhost:3000](http://localhost:3000)
* Visit the Solr admin panel at: [http://localhost:8983/solr/#/blacklight-core](http://localhost:8983/solr/#/blacklight-core)

### Index Example Data

Index the GeoBlacklight project's test fixtures via:

```bash
$ bundle exec rake "geoblacklight:index:seed[:remote]"
```

Additional Aardvark metadata can be harvested via [GeoCombine](https://github.com/OpenGeoMetadata/GeoCombine):

```bash
$ bundle exec rake "geocombine:clone[geobtaa]"
$ bundle exec rake "geocombine:index"
```
---
