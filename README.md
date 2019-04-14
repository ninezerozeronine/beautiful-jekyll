# ninezerozeronine

This is the source for http://www.ninezerozeronine.com

The template comes from [Dean Attali's Beautiful Jekyll project](http://deanattali.com/beautiful-jekyll). The original readme for that can be found here: https://github.com/daattali/beautiful-jekyll#readme

Dean made a [blog post](https://deanattali.com/2015/03/12/beautiful-jekyll-how-to-build-a-site-in-minutes/) that provides extra deatil on some extra customisations.

Here are the modifications I've made on top of his original template (Other than very basic changes in the `_cofig.yml` file):

## Added Google custom search

* Sign up for google custom search (https://cse.google.com). Use the full width option and customise the colours to match the page colours.
* Add search.md page and code snippet
* Add search.css from deanattalis current home page, add overrides to table values defined in `main.css`. 

## Add link to tags, search and projects in navbar

* Make entries with names that match the corresponding .md files under the root in the navbar-links section in `_config.yml`

## Add favicon

* Use http://convertico.com/ to make an ico file after scaling the png to 64x64 in Photoshop. Call the file favicon.ico and put it under the root.

## Add custom URL
* Added a CNAME file containing the url of the page (www.ninezerozeronine.com)
* Configured DNS setting in host provider:
 * host: www, record:CNAME, data: ninezerozeronine.github.io
 * host: @, record A, data: 192.30.252.153
 * host: @, record A, data: 192.30.252.154
* Went to the repo settings and chose:
 * Use custom domain
 * Enforce HTTPS

## Add flickr social link

* Modfication to `_data/SocialNetworks.yaml`

## Add contact form

* Use formspree.io and the information in [Deans post](http://disq.us/p/1qmi76b)