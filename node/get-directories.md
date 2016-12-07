To get all the directires for a glob pattern of files:

```js
const glob = require('glob');

glob('src/**/*.test.js', function (err, files) {
    if (err) {
        console.error(err);
        return;
    }
    
    const directories = Array.from(
        files.map(f => f.substr(0, f.lastIndexOf('/')))
            .reduce((accum, f) => accum.add(f), new Set())
    );
    console.log(directories);
});
```
If you want it as a (async) function instead of a script:

```js
const glob = require('glob');

function getDirectories(path, cb) {
    glob(path, function (err, files) {
        if (err) {
            cb(err);
            return;
        }
        
        try {
            const directories = Array.from(
                files.map(f => f.substr(0, f.lastIndexOf('/')))
                    .reduce((accum, f) => accum.add(f), new Set())
            );
            cb(null, directories);
        } catch (e) {
            cb(e);
        }
    });
}
```
