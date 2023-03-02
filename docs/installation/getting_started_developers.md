
# Getting Started for Developers

Purpose: how to install a local instance of GeoBlacklight for Development purposes.  


## Installation for Development

1. To set up a working space, navigate to where you'd like to put your test GeoBlacklight app and then clone the repository:
```
$ git clone git@github.com:geoblacklight/geoblacklight.git
```

2. Once the files are downloaded, run
```
$ cd geoblacklight
$ bundle exec rake geoblacklight:server
```

This command executes everything needed to run a local version of GeoBlacklight. In order to see the version you have running, open a web browser and go to [http://localhost:3000/](http://localhost:3000/). You should be able to navigate around the site. Remember that your Rails server is running locally, so to stop it, run ^C (ctrl + c).


!!! tip
	If you run into issues running this rake task, try removing your `Gemfile.lock` file and removing the test app with `rm -R .internal_test_app`. Then run `bundle install` before running the above command again.


### Running Solr and Rails server separately

You may decide to run either the Solr server or Rails server separately. With Solr, for instance, run
```
$ rake geoblacklight:solr
```
Then, open another Terminal window, navigate to the place where your app is located, and run:
```
$ rake engine_cart:server
```
Once the server is running, you can open a web browser and visit the URL it prompts, usually [http://localhost:8983/solr/#/blacklight-core](http://localhost:8983/solr/#/blacklight-core) to see the admin interface of your test instance of Solr. As before, remember that ^C (ctrl + c) stops the server.

## Unit Testing

### Running all the tests
As you develop and make changes, you may want to run tests on parts of the app to see if any warning occur. You can run the following to test the app
```
$ rake ci
```
Note that a test like this could take up to 5-6 minutes to complete, or longer. Warnings, deprecations, and other messages will be printed on your Terminal screen.

### Running the tests separately
```
$ rake geoblacklight:solr
```
Then, in another terminal window:
```
$ rspec spec/
```
*Note:* It is not necessary to run tests after every change you make. You can, for instance, change the name of a facet field, save your file, and then refresh your browser to see the change. However, if you add a new fixture metadata record, you will have to stop the servers and then restart them so the new file will be indexed.

---
