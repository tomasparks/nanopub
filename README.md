MicroPub support for Static Blog Engine
=======================================

This php script provides micropub support for the [Hugo Static Blog Engine](https://gohugo.io). Incoming posts are rewritten to a [JSON-header Hugo Format](http://gohugo.io/content/front-matter/) and saved to the user's content store.

Currently, the script will handle the following indieweb functions:-

- [notes](https://indieweb.org/note)
- [articles](https://indieweb.org/article)
- [replies](https://indieweb.org/reply), adding the **title** of the article/note you are replying to
- [photos](https://indieweb.org/note), note that this functionality _requires_ the use of JSON-posts. **nanopub** is not presently equipped to handle multipart uploads
- [checkins](https://indieweb.org/checkin), this functionality is heavily informed by [OwnYourSwarm](https://ownyourswarm.p3k.io/) and the format that service uses
- [bookmarks](https://indieweb.org/bookmark)

**nanopub** offers the following functionality as described in the formal [Micropub Specification](https://www.w3.org/TR/micropub/)

Required
--------
- Supports header and form parameter methods of authentication
- Supports creating posts using `x-www-form-urlencoded` syntax

Optional
--------
- Supports updating and deleting posts
- Supports JSON syntax and source content query
- Supports replacement and deletion of properties
- As it uses a separate Media Endpoint it provides configuration query

[Full implementation report](https://micropub.rocks/implementation-reports/servers/132/dohoQpnIdZYxrwcpMgzj) is available on [micropub.rocks](https://micropub.rocks/)

**nanopub** additionally supports syndication of content to external silos. Currently it provides syndication to [Twitter](https://twitter.com) and [Mastodon](https://mastodon.social), although it also provides a framework implementation for any modern API-based endpoint. An example is provided of the script pinging the [micro.blog](https://micro.blog) service to update the user's feed.

The code is relatively self-explanatory and documented, and can be adjusted easily to meet different needs.

Installation
------------

Clone the contents into the `static` folder of your Hugo installation.

You'll need to set your site up with the requisite headers to:

- Use [IndieAuth](https://indieauth.com/setup) as an identity/token service
- Identify `nanopub.php` as your site's [micropub endpoint](https://indieweb.org/Micropub#How_to_implement)

On my site, these headers are provided as follows:

```html

<!-- indieweb components  -->
  <link rel="authorization_endpoint" href="https://indieauth.com/auth" />
  <link rel="token_endpoint" href="https://tokens.indieauth.com/token" />
  <link rel="micropub" href="https://ascraeus.org/nanopub.php" />

```

Then you'll have to configure the options in `configs.php`

- Twitter Keys can be obtained using the [Create New App](https://apps.twitter.com/app/new) on twitter.
- Mastodon Keys are more command-line driven, but relatively straightforward. See [the Mastodon API documentation](https://github.com/tootsuite/documentation/blob/master/Using-the-API/Testing-with-cURL.md)
- As Mastodon is a federated network, you do need to _explicitly_ specify your Mastodon Instance.
- If using the micro.blog function, you need to specify your site's rss/atom feed.

TODO
----
* [X] Save all content in the correct Hugo JSON format
* [X] Read all content from disk in correct microformats2 syntax
* [X] Make it work with a more complete set of micropub features
* [ ] Make a `setup.php` script to complete the required configuration settings.
* [ ] Implement rsvp's, itineraries &c
* [ ] Trigger sitegen on succesful operation.

Author
---
* **Daniel Goldsmith** <https://ascraeus.org>

Licences
--------
- **nanopub** is released under the [Free Public Licence 1.0.0](https://opensource.org/licenses/FPL-1.0.0). 
- The included and unmodified [TwitterAPIExchange.php](https://github.com/J7mbo/twitter-api-php) is Copyright (c) 2013 James Mallison (j7mbo.co.uk) and under an MIT Licence.

Acknowledgments
---------------
* The IndieAuth validation sequence was taken from [Amy Guy's Minimal Micropub](https://rhiaro.co.uk/2015/04/minimum-viable-micropub), without which I couldn't have done this.
* All at the #indieweb and #indieweb-dev IRC channels, who provided inspiration and support in equal measure.
* [@lyda](https://phrye.com)

Changes
-------
Version | Date | Notes
-------:|:----:|:-----
1.1 | 2017-11-14 | Rewrite of script to remove redundant and repetitive code.
|||FIX: Added a getallheaders() replacement for web servers without apache functions
1.0 | 2017-10-17 | First official release. 

 


>If someone is able to show me that what I think or do is not right, I will happily change, for I seek the truth, by which no one ever was truly harmed.  
_– Marcus Aurelius, Meditations, VI.21_
 