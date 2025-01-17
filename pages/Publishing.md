type:: [[Feature]]
platform:: [[Desktop]]
description:: This feature publishes a graph as a [[Publish Web]], single page application.

- ## Usage
	- [[Publishing (Desktop App Only)]] is a tutorial to publish your first graph.
	- An alternative to publishing from the menu is running the command `Export public graph pages as html`.
- ## Functionality
	- Publishing permissions are per page, depending on whether the page is "public".
		- By default no pages are public. Individual pages can be marked as public with the property `publish:: true`.
		- Alternatively, in [[Settings]] all pages can be made public by default and then the property `publish:: false` can be used to make specific pages private.
	- All published pages are displayed in a read-only mode.
	- Published apps should read user configuration in [[config.edn]] and [[custom.css]].
	- ### Available Features
	  id:: 63595c2e-2383-42d4-ad20-5647758a7337
		- Most features in a [[Publish Web]] app should work e.g. page [[Search]], block links and page links. Anything that involves editing won't work of course since the app is read-only.
		- query-table:: true
		  query-properties:: [:page :platform :initial-version]
		  #+BEGIN_QUERY
		  {:title "These features are not available in a Publish Web App"
		   :query [:find (pull ?p [*])
		                :where
		                (page-property ?p :type "Feature")
		                (or
		                     ;; Hardcode not Publish Web values for now as not didn't work here
		                     (page-property ?p :platform "Desktop")
		                     ;; All mentions of both of these in platform is to mention it as an exception
		                     ;; Can create a different property value if this becomes too cumbersome
		                     (and (page-property ?p :platform "All Platforms")
		                              (page-property ?p :platform "Publish Web")))]}
		  #+END_QUERY
		- Some features that aren't available do have workarounds. For example, applying a [[Custom theme]] is a common request. Since themes are plugins, they do not just work as plugins are [[Desktop]] only. You can workaround this with this example custom.css
		  ```css
		  // This uses the logseq-dev-theme but the url can be changed to any theme's github url
		  @import url("https://cdn.jsdelivr.net/gh/pengx17/logseq-dev-theme@main/custom.css");
		  ```
- ## Additional Links
	- https://github.com/pengx17/logseq-publish - Popular approach to publishing graphs on github
	- https://github.com/sawhney17/logseq-schrodinger - Plugin to export Logseq pages to Hugo