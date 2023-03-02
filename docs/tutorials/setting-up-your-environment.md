---
title:  "Setting up your environment"
hide:
  - toc
---

GeoBlacklight has similar prerequisites to [Blacklight][bldependencies]. It diverges from Blacklight requirements by using a customized Solr schema and configuration, [OpenGeoMetadata](https://opengeometadata.org).

## Software you should have installed on your development computer

  - [Ruby > 3.0][installruby]
  - [Rails > 6.0][installrails]
  - [Git][installgit]
  - [Java > JRE version 11 or higher][installjava]
  - [Node.js > 14.15 LTS][installnode]
  - [Yarn > 1.13][installyarn]

It is recommended to install the latest versions of Ruby, Rails, and Node.js. We strive to keep GeoBlacklight updated with these versions. A great, almost always up-to-date, tutorial on getting a Ruby on Rails development environment is available here: [https://gorails.com/setup](https://gorails.com/setup).

!!! tip
	
	Using version management tools for compatible versions of Ruby ([rvm](https://rvm.io/), [rbenv](https://github.com/rbenv/rbenv/), [asdf](https://asdf-vm.com/)) and Node ([nvm](https://github.com/nvm-sh/nvm/blob/master/README.md), [asdf](https://asdf-vm.com/)) can make development easier.

## Browser Testing

Cross-browser testing provided by:

<a href="https://www.browserstack.com/"><img src="https://user-images.githubusercontent.com/784196/43614155-d65e3f98-9677-11e8-8ecf-89f0746f91e0.png" width="150"></a>



[geoblacklight]:        http://geoblacklight.org
[geoblacklightproject]: /projects/geoblacklight
[installruby]:          https://gorails.com/setup#ruby
[installrails]:         https://gorails.com/setup#rails
[installgit]:           https://gorails.com/setup#git
[installjava]:          http://www.oracle.com/technetwork/java/javase/downloads/index.html
[rubyonrails]:          http://rubyonrails.org/
[bldependencies]:       https://github.com/projectblacklight/blacklight/wiki/Quickstart
[installnode]:          https://nodejs.org/en/download/package-manager/
[installyarn]:          https://yarnpkg.com/lang/en/docs/install/
