CodeMirror for TinyMCE4
=======================

The [TinyMCE][] wysiwyg editor comes with a very basic HTML source editor.This
plugin for TinyMCE makes editing HTML source code a more pleasant experience. It
is based on the excellent [CodeMirror][] code editor, developed by Marijn Haverbeke.
This plugin offers the following functionality:

- Syntax highlighting of HTML, Javascript and PHP code
- Line numbers
- Highlighting the line currently being edited
- Automatic indentation
- Many undo/redo levels
- Search/Replace functionality
- Etc. etc.

 [TinyMCE]: http://www.tinymce.com/
 [CodeMirror]: http://codemirror.net/

Installation
------------

1. Download and install TinyMCE 4 and make sure it runs correctly with default settings.
2. Download this repository found at https://github.com/christiaan/tinymce-codemirror
3. Place the directory `plugins/codemirror` in the `tinymce/plugins` directory.
4. Download CodeMirror (version 4 or later) from http://codemirror.net/codemirror-latest.zip.
5. Unpack codemirror-latest.zip inside the plugins/codemirror folder that was
   just created. A folder named codemirror-4.8 (or similar) will be created.
6. Activate the codemirror plugin in TinyMCE:

    plugins: ['codemirror']

7. Optionally, add the code button to TinyMCE’s toolbar:

    toolbar: 'undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | code'

8. Test: You should see a Source code item in the Tools menu. Click it to edit
   the HTML source code.

Configuration
-------------
Additional configuration options

You can modify the behaviour of the codemirror plugin, by adding a codemirror
object to the TinyMCE configuration.

**indentOnInit**: boolean (false) CodeMirror automatically indents code. With
the indentOnInit option, you tell the Source Code editor to indent all code when
the editor opens. This might be slow for large documents.

**fullscreen** boolean (false) Whether to load the tinymce plugin and codemirror
in full screen mode.

**width**: int (800) Codemirror window width

**height**: int (550) Codemirror window height

**path**: string (codemirror) You might already have CodeMirror hosted elsewhere
(outside TinyMCE). In that case, you can reuse that CodeMirror instance, by
overriding the default path. For example:

    path: 'http://www.mysite.com/tools/codemirror-4.8'

**config**: Object CodeMirror configuration object, which is passed on to the
CodeMirror instance. Check http://codemirror.net/doc/manual.html for available
configuration options.

**jsFiles**: Array Array of CodeMirror Javascript files you want to
(additionally) load. For example:

    jsFiles: [
       'mode/clike/clike.js',
       'mode/php/php.js'
    ]

The following Javascript files are always loaded: lib/codemirror.js,
addon/edit/matchbrackets.js, mode/xml/xml.js, mode/javascript/javascript.js,
mode/css/css.js, mode/htmlmixed/htmlmixed.js, addon/dialog/dialog.js,
addon/search/searchcursor.js, addon/search/search.js,
addon/selection/active-line.js.


**cssFiles**: Array Array of CodeMirror CSS files you want to (additionally)
load. For example:

    cssFiles: [
       'theme/neat.css',
       'theme/elegant.css'
    ]

The following CSS files are always loaded: lib/codemirror.css,
addon/dialog/dialog.css.

Config example

```js
tinymce.init({
  selector: '#html',
  plugins: 'codemirror',
  toolbar: 'undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | code',
  codemirror: {
    indentOnInit: true, // Whether or not to indent code on init.
    fullscreen: true,   // Default setting is false
    path: 'CodeMirror', // Path to CodeMirror distribution
    config: {           // CodeMirror config object
       mode: 'application/x-httpd-php',
       lineNumbers: false
    },
    width: 800,         // Default value is 800
    height: 600,        // Default value is 550
    jsFiles: [          // Additional JS files to load
       'mode/clike/clike.js',
       'mode/php/php.js'
    ]
  }
});
```

Compatibility
-------------

This TinyMCE plugin is compatible with pretty much all browsers out there,
including Firefox, Google Chrome, Safari and Internet Explorer, version 8 or
better. It is NOT compatible with Interner Explorer 6 or 7, simply because
CodeMirror itself does not work in these versions.

Contributing
------------
When making changes to `plugins/codemirror/plugin.js`, be sure to run
`npm run prepublish` before committing. The `prepublish` script will generate
the `plugins/codemirror/plugin.min.js` file.

To run `npm run prepublish` you need uglify-js. Run following command inside your codemirror folder to get the needed files:
`sudo npm install uglify-js`

This will generate the subfolder `node_modules` inside codemirror.

Changelog
---------

Version 1.5 - 2016-09-14
- Bugfix: Cursor position inside JS, style or &nbps; #2
- Bugfix: z-index issue with table panel and source code dialog #6
- Add: Added CSS and set default CM theme
- Add: Better defaults, per codeMirror
- Add: codemirror config window width and height

Version 1.4 - 2014-12-15
- Bugfix: Replace setLine call to replaceRange (for CodeMirror 4)
  This fixed `&#x0;` appearing in the source code.
- Note: This plugin requires CodeMirror version 4 (3 is no longer supported)

Version 1.3 - 2014-03-04
- Bugfix: If any text was highlighted in CodeMirror and the code dialog is
  closed and saved, the selected text was removed from TinyMCE.
- Macintosh users now see Macintosh keyboard shortcuts.

Version 1.2 - 2013-09-04
- Dirty state of CodeMirror now passed on to TinyMCE.
- When submitting CodeMirror code to TinyMCE, cursor position is retained.
  Note: this only works when the cursor is *not* inside a <tag>.

Version 1.1 - 2013-07-19
- New options jsFiles and cssFiles.

Version 1.0 - 2013-06-29
- Initial release.

Contributors
------------

Arjan Haverkamp <arjan@avoid.org> - original author

Contributors details, check on GitHub: https://github.com/christiaan/tinymce-codemirror/graphs/contributors