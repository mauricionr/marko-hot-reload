Marko Sample - Hot Reloading
===============================

# Get started

```bash
git clone git@github.com:marko-js-samples/marko-hot-reload.git
cd marko-hot-reload
npm install
node server
```

# Enabling Hot Reloading

There are two steps to allowing Marko templates to be hot reloaded on the server:

___Step 1: Enable hot reloading:___

```javascript
require('marko/hot-reload').enable();
```

___Step 2: Tell the Marko runtime when a template is modified:___

Marko does not come with a mechanism for watching Marko template files for changes. Your app must include the code for watching a change to a file and then pass along the full template path to Marko so that the modified template can be hot reloaded. For example, using the [builtin fs file watching service](https://nodejs.org/api/fs.html#fs_fs_watch_filename_options_listener):

```javascript
require('fs').watch(templatesDir, function (event, filename) {
    if (/\.marko$/.test(filename)) {
        // Resolve the filename to a full template path:
        var templatePath = path.join(templatesDir, filename);

        console.log('Marko template modified: ', templatePath);

        // Pass along the *full* template path to marko
        require('marko/hot-reload').handleFileModified(templatePath);
    }
});
```

# Using browser-refresh

You can also use the [browser-refresh](https://github.com/patrick-steele-idem/browser-refresh) module to watch for changes to Marko template files. You just need to add the following line of code into the main script for your app:

```javascript
require('marko/browser-refresh').enable();
```

Then you would use [browser-refresh](https://github.com/patrick-steele-idem/browser-refresh) to launch your Node.js app. For example:

```bash
npm install browser-refresh --global
browser-refresh server.js
```

For more details, please see the docs for the [browser-refresh](https://github.com/patrick-steele-idem/browser-refresh) module.

