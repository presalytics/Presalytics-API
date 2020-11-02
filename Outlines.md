# Story Outlines

A Story's "Outline" is that most important element of a story.  The outline is a json document that contains a series of rendering instructions for a presalytics.io Story.  

Outlines are rendered from the data in this json object by a "Renderer", which is [special type of object in the Presalytics Python Library](https://presalytics.github.io/python-client/presalytics/#presalytics.Renderer) with methods  that convert outlines to html.  

# Outline Properties

A Story's outline should conform to the the [Story Outline JSON Schema](https://api.presalytics.io/story/outline-schema/0.3.1/story-outline.json).  The schema defines the properties detailed below:

* `title`: The title of story.  This property is synced the the title of the [Story](/docs/stories) object.

* `description`: Text notes for other editors. Typically used to describe made in the current revision of the outline.

* `info`: Metadata about this story outline.  Includes data on revision number, date created, date modified, creator name and revision notes

* `pages`: A list of the Story Outline Pages.  See the [pages](#pages) section below for more information.

* `themes`: A list of themes of the story outline.  A theme typically defines default colors and text formats (e.g., fonts) for a story.  


### Pages

A `page` within a Story outline defines instructions of converting a set of [widgets](#widgets) to html.  The page object governs the layout of widgets on page in the story. A page object has the following properties:

* `name`: The name of the page

* `kind`: A unique string that maps to class that implements the [PageTemplateBase Class](https://presalytics.github.io/python-client/presalytics/index.html#presalytics.PageTemplateBase) in the Presalytics Pythonlib.  Classes that implement this class have `__component_kind__` property that maps the the kind of this page, and a `render()` method that implements this class.

* `widgets`: A list of [widgets](#widgets) that this page renders.  See Below for more information

* `plugins`: A list of plugins used when rendering this page.  [See Below](#plugins).


### Widgets

The `widget` object is the lowest-level building block for Presalytics Stories. A widget is a flexible object that can map a data source (e.g., a SQL query) to an html fragment.  

* `name`: The name of the widget

* `kind`: A unique string that maps to class that implements the [WidgetBase Class](https://presalytics.github.io/python-client/presalytics/index.html#presalytics.WidgetBase) in the Presalytics Pythonlib.  Classes that implement this class have `__component_kind__` property that maps the the kind of this page, and a `render()` method that implements this class.

* `data`: A set of requeirement parameters needed to convert this widget into html.  The strcuture of the data object will be different for each widget kind.

* `plugins`: A list of plugins used when rendering this page.  [See Below](#plugins).

### Plugins

`plugin` objects are resuable scripts and styles that are used help pages and widgets render.  For example, if a widget requires a certain javascript library in order to render properly, a `script` plugin can be used to place a script tag in the html.  Libraries such as `React.js`, `D3.js`, etc.  can all be loaded natively in a Story, and rendered accordingly. A `style` plugin can be used load either custom inline styles or and external link (e.g., bootstrap).  

Properties of the `plugin` object are as follows:

* `name`: a name for this plugin

* `kind`: The plugin type.  Either "style" for style pligns or "script" for script plugins

* `data`: Any data required for the plugin to load correctly.  Could include key-value pairs to include in a script or style plugin that gets loaded via a template.