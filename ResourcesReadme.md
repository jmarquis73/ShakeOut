Adding Resources:
-----------------
Add resources by going to the core:resources layout and making a new record
This is a typical resource with self explanatory titles; but, for the new page, there are some notable fields for organizing the resource:
..+ Thumbnails: if you set the extension field to 'gif', 'jpg', or 'jpeg', the page will try to use the URL field as thumbnail source. 
..+ Category: The resource will first be filed under its category_name field. This field is also important for category_name limited queries. If it does not have a category_name, it won't appear in queries that filter on that. If they don't have that filter, the resource will be categorized by its ResourceTypes.
..+ Region*: Specify shakeout_region to localize the resource to a region i.e. California. 
..+ Event key*: Alternatively to shakeout_region, you can specify shakeout_event_key.
\* The default shakeout_region is California and it is the default filter for resources. To change this or query based on specific event key see Implementation below.

Adding Categories:
-----------------
Currently there are only four categories with limited descriptions. To add more, simply make a new record in core:categories. 
Categories currently only have three fields you need to set: name, description, and image. The name is referred to by the resources, and must be reflected in the category field in the resources table.
The description and image url are assets for displaying the category with useful information in the splash screen.

Implementation:
-----------------
There are two main views, both located in the shakeout/resources directory: resourceTabView and resourceSplashView. The tab view displays resources in a tabulated display window w/ tabs corresponding to different resource categorizations. The splash view includes resourceTabView, but has an extra layer of UI- a splash screen of the categories- that lays on top.
Implementation is as easy as including the php files. The output of the files is stored in the `$divContent` variable so just assign that to a smarty box to place the view in that box. An example of implentation can be seen in the shakeout/howtoparticipate.php file.
By default, the query will filter by the shakeout_region: California. If you wish to refine by a different region, just set `$shakeoutRegion` before you include the file. If you want to specify other filters, you should set `$resourceQueryParams`.
`$resourceQueryParams` is an associative array that takes filter key, and filter value pairs. An example:
````	
    $shakeoutEvent = 9999;
    $resourceQueryParams = array("shakeout_event_key" => $shakeoutEvent);
````
To specify multiple filters, just add more key value pairs to the associative array, separated by commas. See PHP reference on declaring associative arrays if you need help.

Code Layout:
-----------------
Unfortunately, due to the way smarty templates function, you cannot have any html, style, or script in the page before the assignment of the smarty template. As a result, much of the content of these pages are encapsulated in strings. This is a bit annoying if you're used to working in a nice editor, but doesn't really change the content. If you don't have to work with smarties just unwrap the quotes and it should become much more legible. 
There are three main parts of the pages: php query, functions, and variable declarations at the top, the html (wrapped in strings), and sometimes some scripts or css at the bottom (also wrapped in strings).
I wrote initially unencapsulated by strings, and tried to streamline php insertion as much as possible. Ultimately these pages aren't that large so it shouldn't be hard to sift through. 	
