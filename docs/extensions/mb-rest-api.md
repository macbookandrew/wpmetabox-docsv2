---
title: MB Rest API
---

import LiteYouTubeEmbed from 'react-lite-youtube-embed';
import 'react-lite-youtube-embed/dist/LiteYouTubeEmbed.css';

MB Rest API helps you retrieve and update custom fields via the WordPress REST API. It's very helpful if you develop an application that uses WordPress as a back end such as a mobile app. Or you need to integrate WordPress with another system.

The extension works only with custom fields created by Meta Box and extensions. For custom custom fields or fields created by other plugins, please refer to [WordPress documentation](https://developer.wordpress.org/rest-api/).

## Video tutorial

See how the plugin works in this quick video:

<LiteYouTubeEmbed id='YMjAIZLUeF4' />

## Getting custom fields' values in REST API responses

After installing and activating the plugin, [create some custom fields](/custom-fields/). Then just go to edit your posts and add some values to your custom fields as you usually do.

Now you can retrieve these values when viewing REST API responses. The plugin **automatically creates a new field `meta_box` in the response JSON array, which holds all custom fields' values**.

For example:

If you create a field group for posts like this:

![meta box for posts](https://i.imgur.com/61eFQIf.png)

And you get the post fields via REST API with URL `http://yourdomain.com/wp-json/wp/v2/posts/`, you'll see:

![custom fields values in rest api response](https://i.imgur.com/VL5UfKU.png)

(The response is an JSON string. The screenshot above uses Firefox browser to beautify the result. You can see similar result in Google Chrome as well)

If you have multiple meta boxes, the plugin will merge all fields in those meta boxes and return a single array in the `meta_box` field of the response.

Please note that the similar result will be returned for single post, terms, single term, users, single user. E.g. it works with the following endpoint in REST API:

```
http://yourdomain.com/wp-json/wp/v2/posts/
http://yourdomain.com/wp-json/wp/v2/posts/1234
http://yourdomain.com/wp-json/wp/v2/categories/
http://yourdomain.com/wp-json/wp/v2/categories/1234
http://yourdomain.com/wp-json/wp/v2/users/
http://yourdomain.com/wp-json/wp/v2/users/1234
```

## Updating custom fields value via REST API

To update custom fields value via REST API, add a new field `meta_box` to your POST requests. This field should be either an array of `'field_id' => 'field_value'` or a JSON string of  this array.

The plugin will automatically fetch the fields and update the corresponding custom fields.

