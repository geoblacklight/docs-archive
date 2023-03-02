## Create an application

### Generating your Rails application

For more information about generating a Rails application see the [Getting Started with Rails](http://guides.rubyonrails.org/getting_started.html) guide. Before, make sure you have Rails installed by running the following:
```sh
$ rails -v
```
If you get an error run:

```sh
$ gem install rails
```
Now you should have Rails installed on your machine and are ready to proceed.

  1. Create a new Rails application using the GeoBlacklight template, in which **"your_app_name"** can be anything you want to name your app.

     ```sh
     $ rails new your_app_name
     ## For example, you could also use `rails new mockup_geoblacklight`
     ```
  1. Switch to its folder

     ```sh
     $ cd your_app_name
     ```

  1. Run the rails server.

     ```sh
     $ rails s -b 0.0.0.0
     ```

     We are running the Rails server with the "-b" option which is binding the server to the 0.0.0.0 IP address. This is only necessary if your are running the application on your Vagrant virtual machine.
     {: .flash-alert}

     Now you can visit the Rails application at [http://127.0.0.1:3000](http://127.0.0.1:3000). You should see "Yay! You're on Rails" CTRL + c will stop server.

     ![rails_welcome](https://guides.rubyonrails.org/images/getting_started/rails_welcome.png "Welcome aboard!")

**Note** You will need to leave the Terminal window open while the Rails server is running.

  1. *Optional* Initialize your git repository and commit your changes

     ```sh
     $ git init
     $ git add .
     $ git commit -m 'initial commit of Rails application'
     ```

<hr>

### Install GeoBlacklight

Now that we have started our Rails application, we need to install GeoBlacklight.

  1. Add GeoBlacklight to your `Gemfile`. To do this, navigate to the Gemfile in your application, open it with a text editor, and paste the following in to add it to the list of gems:

     ```ruby
     # In ./Gemfile
     gem 'blacklight'
     gem 'geoblacklight'
     ```

  1. Install required gems and their dependencies

     ```sh
     $ bundle install
     ```

  1. Run Blacklight generator (with devise authentication)

     ```sh
     $ rails g blacklight:install --devise
     ```

  1. Run GeoBlacklight generator (overrides Blacklight default Solr config)

     ```sh
     $ rails g geoblacklight:install -f
     ```

     Depending on how your machine is setup you may need to prepend the rails or rake command with [bundle exec](http://bundler.io/man/bundle-exec.1.html).
     {: .flash-alert}

  1. Run database migrations

     ```sh
     $ rake db:migrate
     ```


     Quick tip: All of these tasks (1 - 5) are included as part of template to generate a new GeoBlacklight application.
     
     To run that generator just run:
     {: .flash-notice}

     ```sh
     $ DISABLE_SPRING=1 rails new your_app_name -m https://raw.githubusercontent.com/geoblacklight/geoblacklight/main/template.rb
     ```

     Remember to `cd your_app_name` into the directory before starting the server if you are using the template generator.
     {: .flash-notice}


  1. Start the Solr and Rails server.

     ```sh
     $ rake geoblacklight:server
     ```
  
     Running this command will download and start the [Solr server](http://127.0.0.1:8983/solr). Other commands available to control Solr include:
     {: .flash-notice}


     ```sh
     $ rake solr:clean # Useful when seeing a "core already exists" error.
     $ rake solr:start # Starts Solr independently of the Rails server in the background (without loading core)
     $ rake solr:stop # Stops Solr
     $ rake solr:restart # Stops and restarts an already running background Solr server
     ```

  1. Navigate to [http://127.0.0.1:3000](http://127.0.0.1:3000). You should see the GeoBlacklight homepage. CTRL + c will stop both the Solr and Rails server.


  1. *Optional* Commit your work

     ```sh
     $ git add .
     $ git commit -m 'installed Blacklight and GeoBlacklight'
     ```

    
     Great job for making it this far. You now have a working GeoBlacklight application!
     {: .flash-success}

### Install RSpec
[RSpec](http://rspec.info/) is a behavior-driven development framework for Ruby. It is the recommended way to test your application and is used by both the Blacklight and GeoBlacklight projects.

  1. Add `rspec-rails` to both the `:development` and `:test` groups in the `Gemfile`. Again, open the `Gemfile` with a text editor and paste the line below into the respective groups.

     ```sh
     # In ./Gemfile
     group :development, :test do
       gem 'rspec-rails', '~> 3.0'
     end
     ```

  1. Download and install RSpec

     ```sh
     $ bundle install
     ```

  1. Initialize the spec/ directory (where specs will reside) with

     ```sh
     $ rails generate rspec:install
     ```

  1. Run your tests (specs) by running

     ```sh
     $ bundle exec rspec
     ```

     Writing tests for your application is outside the scope of this guide, but there are plenty of great examples out there. Check out the <a href="http://robots.thoughtbot.com/how-we-test-rails-applications">Thoughtbot blog</a>.
     {: .flash-notice}

  1. *Optional* Commit your work

     ```sh
     $ git add .
     $ git commit -m 'Installed RSpec'
     ```
     
## Customize your application
### Basic principles

When it comes to customizing your GeoBlacklight application there are some basic principles to keep in mind.

  1. The less you override the easier it is to upgrade.

     Blacklight and GeoBlacklight adhere to some basic principles which all adopters to override helper methods, view partials, and even classes. A lot of things are configurable out of the box. However, there are some best practices around what to override and where to do it to make sure your application can take advantage to improvements to both Blacklight and GeoBlacklight.  Both projects use [semantic versioning](http://semver.org/) to make this upgrade path easier for adopters.

     [Providing your own view templates](https://github.com/projectblacklight/blacklight/wiki/Providing-your-own-view-templates) - Blacklight Wiki (Customizing the User Interface)

  1. Reach out and ask for help on the [Blacklight Developers](https://groups.google.com/forum/#!forum/blacklight-development) or [GeoBlacklight](https://groups.google.com/forum/#!forum/geoblacklight-working-group) Google Groups

     Asking questions, reaching out to others, and getting feedback from experienced developers is a great practice in general. In this particular case its helps foster the community and start conversations that might help others.

### Customize metadata shown

In this example we are going to change the way the GeoBlacklight is configured to show certain metadata fields on an items page. This is the same way a Blacklight application would configure these fields.

1. Make sure your Solr server and Rails application are started.

     ```sh
     $ rake geoblacklight:server
     ```

2. Open the `app/controllers/catalog_controller.rb` file in your text editor.


     Hint: `catalog_controller.rb` is located at "app/controllers/catalog_controller.rb" in your application


3. Scroll down to lines 137 - 144

     ```ruby
     ...
     config.add_show_field Settings.FIELDS.CREATOR, label: 'Author(s)', itemprop: 'author'
     config.add_show_field Settings.FIELDS.DESCRIPTION, label: 'Description', itemprop: 'description', helper_method: :render_value_as_truncate_abstract
     config.add_show_field Settings.FIELDS.PUBLISHER, label: 'Publisher', itemprop: 'publisher'
     config.add_show_field Settings.FIELDS.PART_OF, label: 'Collection', itemprop: 'isPartOf'
     config.add_show_field Settings.FIELDS.SPATIAL_COVERAGE, label: 'Place(s)', itemprop: 'spatial', link_to_facet: true
     config.add_show_field Settings.FIELDS.SUBJECT, label: 'Subject(s)', itemprop: 'keywords', link_to_facet: true
     config.add_show_field Settings.FIELDS.TEMPORAL, label: 'Year', itemprop: 'temporal'
     config.add_show_field Settings.FIELDS.PROVENANCE, label: 'Held by', link_to_facet: true
     ...
     ```
     These configuration options relate to fields that are indexed in Solr. You can disable a metadata field being shown on an items show page. If you navigate to an [items page](http://127.0.0.1:3000/catalog/stanford-cg357zz0321), it will currently show field called publisher. Maybe you would like to rename that field to "Data publisher".

4. Modify the label in line 139

     ```ruby
     # change this
     config.add_show_field Settings.FIELDS.PUBLISHER, label: 'Publisher', itemprop: 'publisher'
     # to this
     config.add_show_field Settings.FIELDS.PUBLISHER, label: 'Data publisher', itemprop: 'publisher'
     ```

     Save the file and reload the page. You should see the label change.

5. Next we will remove the "Author(s)" metadata field from being shown. Comment out or remove the `Settings.FIELDS.CREATOR` line (137).

     ```ruby
     # config.add_show_field Settings.FIELDS.CREATOR, label: 'Author(s)', itemprop: 'author'
     ```
     Save the file and reload the page. You should no longer see the "Author(s)" field.

     You have now customized a layer's show page!


### Changing the style of your application

GeoBlacklight uses [Twitter Bootstrap](http://getbootstrap.com/) as a base for UI components and is implemented using the [bootstrap-sass](https://github.com/twbs/bootstrap) gem. This approach should make things easier for adopters wanting to customize the look and feel of their application. [Bootstrap variables](https://github.com/twbs/bootstrap/blob/main/scss/_variables.scss) can easily be modified which will change how the application looks.

You can update Bootstrap variables in your `_customizations.scss`!

Change link color

     ```scss
     // in app/assets/stylesheets/_customizations.scss
     // Links
     $link-color: green;
     ```

Change default border style

     ```scss
     // in app/assets/stylesheets/bootstrap-variables.scss
     // Borders
     $border-width: 2px;
     $border-radius: .4rem;
     ```


Great job! You can configure a whole host of options using this Bootstrap customization technique. Once again, here is the list of Bootstrap variables you can customize https://github.com/twbs/bootstrap/blob/main/scss/_variables.scss .
  

### Overriding a partial

Lets say you want to override the homepage that is shown in GeoBlacklight that can easily be done by just creating same-named a partial at the same path in your GeoBlacklight application.

1. Check out home page partial on Github. [https://github.com/geoblacklight/geoblacklight/blob/main/app/views/catalog/_home_text.html.erb](https://github.com/geoblacklight/geoblacklight/blob/main/app/views/catalog/_home_text.html.erb)

2. This same partial is being overriden from Blacklight [https://github.com/projectblacklight/blacklight/blob/master/app/views/catalog/_home_text.html.erb](https://github.com/projectblacklight/blacklight/blob/master/app/views/catalog/_home_text.html.erb)

3. Create a file with the same name and path in your application.

     ```sh
     $ mkdir -p app/views/catalog
     $ touch app/views/catalog/_home_text.html.erb
     ```

4. Edit this file and add some custom text

     ```erb
     This is the home page.

     Search bar:
     <%= render_search_bar %>
     ```

     See how easy that was? You even included another partial!


### Customize i18n keys

Blacklight and GeoBlacklight use [i18n](http://guides.rubyonrails.org/i18n.html) for internationalization support. These keys provide a quick way to customize your app without having to override partials.

1. Open up file `config/locales/blacklight.en.yml`

     ```yaml
     en:
       blacklight:
         application_name: 'Blacklight'
     ```

2. Edit the file, adding a customization to the search form label

     ```yaml
     en:
       blacklight:
         application_name: 'Your Geo App'
         search:
           form:
             submit: 'Search this'
     ```

     Refresh your home page and you should see the submit button text changed. If you inspect the html you will notice the HTML title attribute changed.

     More configurable keys are available, check out what you can customize using this approach:
      - <a href='https://github.com/projectblacklight/blacklight/blob/master/config/locales/blacklight.en.yml'>Blacklight Configurable Keys</a>
      - <a href='https://github.com/geoblacklight/geoblacklight/blob/main/config/locales/geoblacklight.en.yml'>GeoBlacklight Configurable Keys</a>

## Index Solr Documents

GeoBlacklight uses the GeoBlacklight Schema, Version 1.0 as a template for metadata documents indexed by Solr.

GeoBlacklight provides a rake task to index documents as fixtures for tests. We will use this rake task to index several documents as an example.

### Download fixture metadata documents

1. Assuming that you have already navigated to the directory of your GeoBlacklight app, create a directory for some Solr documents and then move to it:

     ```sh
     $ mkdir -p spec/fixtures/solr_documents && cd spec/fixtures/solr_documents
     ```

2. Download some metadata documents (in JSON format) to the directory

     ```sh
     $ curl -O https://gist.githubusercontent.com/mejackreed/84abc598927c43af665b/raw/geoblacklight-documents.json
     ```

3. Move back to app root directory

     ```sh
     $ cd - # Or cd ../../../
     ```

4. Make sure your Solr server and Rails application are started.

     ```sh
     $ rake geoblacklight:server
     ```

5. *Optional* Commit your work

     ```sh
     $ git add .
     $ git commit -m 'Adds in JSON fixtures'
     ```

The fixtures directory is useful for quickly indexing a small number documents in Solr (built specifically for populating Solr for testing). I would caution though in using this task for large scale indexing and committing, as we've developed other best practices for production-scale indexing.

Now you should see <a href="http://127.0.0.1:3000">facets listed</a> on the lower left hand part of the page. Try a search! You can <a href="http://127.0.0.1:3000/?q=*">search for *</a> to search for everything.


