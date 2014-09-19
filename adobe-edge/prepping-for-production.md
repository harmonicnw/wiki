# Prepping Adobe Edge animation files for production

* Copy _edge_includes/edge.x.x.x.min.js_ to the js folder
* Copy _edge_includes/jquery.x.x.x.min.js_ to the js folder (unless site already has a suitable version of jquery)
* Move _[project_name]_edgePreload.js_ to js folder
* Update reference to _[project_name]_edgePreload.js_ in <HEAD> of HTML
* Edit _[project_name]_edgePreload.js_
  * if jquery is already present on site:
    * comment out htFallbacks for jquery
    * comment out aLoader for jquery
  * in htFallbacks, add js folder to local path  for _edge.x.x.x.min.js_
  * in aLoader, swap paths for local and online reference to _edge.x.x.x.min.js_ (remote reference should be in yepnope block for fallback, local should come first)
  * in aLoader, add js folder to local path for _edge.x.x.x.min.js_
  * add js folder to local path for _[project_name]_edge.js_ in load
  * add js folder to local path for _[project_name]_edgeActions.js_ in load
* Edit [project_name]_edge.js
  * If images folder is not at /images, replace the images directory here
      ```var im='images/'```

## For testing the package locally...
...don't forget to include the jquery file in the HTML if you have stripped it out of the Edge code.

```<script src="../../edge_includes/jquery-2.0.3.min.js"></script>```


## For integration in WordPress...
...links to javascript and images should look something like:

```/wp-content/themes/fortgeorge/edge/[your-project-name]/js/[project_name]_edge.js```


Tips for using multiple animations in a single page

References:
* http://blogs.adobe.com/edge/2012/05/15/bootstrapping-edge-compositions/
* http://www.adobe.com/devnet-docs/edgeanimate/api/current/index.html

Rename Stage Ids from Stage to Stage1, Stage2, ...

This function will allow access individual compositions:
```
AdobeEdge.bootstrapCallback(function (compId) {
	AdobeEdge.getComposition(compId).getStage().play();
});
```

This function binds a function to an event
```
AdobeEdge.Symbol.bindTimelineAction( compId, "stage", "Default Timeline", "complete", function(sym, e) {
	AdobeEdge.getComposition(compId).getStage().play();
}
```