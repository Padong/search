# StartHQ Search API

## Overview

[StartHQ](https://starthq.com) provides federated search across all your web apps via a [browser extension](https://starthq.com/ext). This README describes how to implement your own search provider and requires that you have a StartHQ account with developer features enabled. To get this, simply sign up via the link above and then drop us a line requesting access via the "Feedback" item in the dropdown menu in the upper right.



## Provider Types

### HTML Provider

Find the page with the app's search results, this needs to be an HTML page generated on the server, not a single page app where the DOM is built up using JS on the client; quick way to determine if the page is generated on the server is to "View Source" and search for the search term - e.g. https://mail.google.com/mail/h/aez8fwf893g7/?s=q&q=starthq

If the default version of the web app doesn't generate the HTML on the server, use a User Agent switcher browser extension to access it as if though you were on a mobile device - you should get a mobile web version of the service which will most likely have server generated HTML; note this doesn't always work so you may need to Google for this or try e.g. m.dropbox.com instead of www.dropbox.com.

Make a note of the query parameter entered in the search and replace it with `{{term}}` - this is your "query" string.

The translate string for an HTML provider should be "parseHTML(response)".

For each of `name`, `description` and `link`, find the CSS selector needed to retrieve the elements you need. The easiest way to do this is using the bookmarklet from http://selectorgadget.com/ - start by clicking the elements you want included, then the ones you want excluded, then included and so on until only the elements you want are included.

Finally, use the [AngularJS expression language](http://docs.angularjs.org/guide/expression) (which is a subset of JavaScript) and the DOM API (https://developer.mozilla.org/en-US/docs/Web/API/Node) to retrieve the data you need, e.g.: "element.textContent" to get the textual contents of the element or element.getAttribute("href") to get the value of the href attribute.

To test that this works correctly, fire up e.g. Chrome Developer tools (press F12 in Chrome), open the Console tab and type in the following: var element = document.querySelectorAll‎('.repolist-name a')[0] where '.repolist-name a' is the selector string above; then on the next line type in e.g. element.getAttribute("href") i.e. the Angular expression from above.

Check out [search.js](https://github.com/starthq/search/blob/master/search.js) for more examples.


### JSON provider

This is work in progress.
