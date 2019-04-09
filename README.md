# ninezerozeronine

This is the source for http://www.ninezerozeronine.com

The template comes from [Dean Attali's Beautiful Jekyll project](http://deanattali.com/beautiful-jekyll). The original readme for that can be found here: https://github.com/daattali/beautiful-jekyll#readme

Here are the modifications I've made on top of his original template (Other than very basic changes in the `_cofig.yml` file):

## Add link to tags in navbar

* Make entries with names that match the corresponding .md files under the root in the navbar-links section in `_config.yml`

## Add favicon

* Use http://convertico.com/ to make an ico file after scaling the png to 64x64 in Photoshop. Call the file favicon.ico and put it under the root.

## Add custom URL
* Followed guidelines on https://deanattali.com/2015/03/12/beautiful-jekyll-how-to-build-a-site-in-minutes/
* Added a CNAME file containing the url of the page (www.ninezerozeronine.com)
* Configured DNS setting in host provider:
 * host: www, record:CNAME, data: ninezerozeronine.github.io
 * host: @, record A, data: 192.30.252.153
 * host: @, record A, data: 192.30.252.154
* Went to the repo settings and chose:
 * Use custom domain
 * Enforce HTTPS