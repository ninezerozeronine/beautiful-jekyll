---
layout: post
title: Refining the look of a Google Custom Search in a Beautiful Jekyll page
tags: [beautiful-jekyll, css, google, google-custom-search]
image: /img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/preview.jpg
---

In [his blog post](https://deanattali.com/2015/03/12/beautiful-jekyll-how-to-build-a-site-in-minutes/) Dean runs through how to set up a Google Custom Search page.

This works well on a website with a white background but on one with customised colours the result isn't as appealing:

[![Poor initial results](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/bad-defaults.jpg)](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/bad-defaults.jpg)

(I've updated the search to search [the Home Depot website](www.homedepot.ca) so that there are some results to display)

The first step is to add some css specific to this page to override [what is being done in `main.css` for tables](https://github.com/ninezerozeronine/ninezerozeronine.github.io/blob/e0b741da8ce8cbf38cf1808ec0427ef6072e8776/css/main.css#L636-L670)

The front matter for the search page is updated to use the specific css:

```
---
layout: page
title: "Search"
css: "/css/search.css"
---
```

And `search.css` contains:

```
#google-custom-search {
  margin-top: 50px;
}

input.gsc-input,
.gsc-input-box,
.gsc-input-box-hover,
.gsc-input-box-focus,
.gsc-search-button,
.gsc-selected-option-container {
  box-sizing: content-box; 
  line-height: normal;
}

/* --- Tables --- */

table {
  padding: 0;
}
table tr {
  border-top: 1px solid #ECF3FA;
  background-color: #ECF3FA;
  margin: 0;
  padding: 0;
}
table tr:nth-child(2n) {
  background-color: #ECF3FA;
}
table tr th {
  font-weight: bold;
  border: 1px solid #ECF3FA;
  text-align: left;
  margin: 0;
  padding: 6px 13px;
}
table tr td {
  border: 0px solid #ECF3FA;
  text-align: left;
  margin: 0;
  padding: 6px 13px;
}
table tr th :first-child,
table tr td :first-child {
  margin-top: 0;
}
table tr th :last-child,
table tr td :last-child {
  margin-bottom: 0;
}
```

The top part was taken from [Dean's `search.css`](https://github.com/daattali/daattali.github.io/blob/master/css/search.css)

The result is better but not perfect:

[![Getting better](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/partly-customised.jpg)](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/partly-customised.jpg)

The last step is to edit the appearance of the Google Custom Search itself:

[![Cutomising colours](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/gcs-custom-colours.jpg)](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/gcs-custom-colours.jpg)

After this the end result is much better:

[![Final result](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/fully-customised.jpg)](/img/posts/2019-03-15-refining-look-gcs-beautiful-jekyll/fully-customised.jpg)

The downside of this method is that if the colour scheme in `_config.yaml` changes you need to remember to modify both the `search.css` file and the customisation on the Google side to match.