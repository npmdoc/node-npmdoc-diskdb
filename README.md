# api documentation for  [diskdb (v0.1.17)](http://arvindr21.github.io/diskDB)  [![npm package](https://img.shields.io/npm/v/npmdoc-diskdb.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-diskdb) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-diskdb.svg)](https://travis-ci.org/npmdoc/node-npmdoc-diskdb)
#### A Lightweight Disk based JSON Database with a MongoDB like API

[![NPM](https://nodei.co/npm/diskdb.png?downloads=true)](https://www.npmjs.com/package/diskdb)

[![apidoc](https://npmdoc.github.io/node-npmdoc-diskdb/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-diskdb_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-diskdb/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-diskdb/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-diskdb/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Arvind Ravulavaru",
        "email": "arvind.ravulavaru@gmail.com",
        "url": "http://thejackalofjavascript.com/"
    },
    "bugs": {
        "url": "https://github.com/arvindr21/diskdb/issues"
    },
    "dependencies": {
        "chalk": "^0.4.0",
        "merge": "^1.1.3",
        "node-uuid": "^1.4.1"
    },
    "description": "A Lightweight Disk based JSON Database with a MongoDB like API",
    "devDependencies": {
        "grunt": "^1.0.0",
        "grunt-contrib-jshint": "^1.0.0",
        "grunt-contrib-nodeunit": "^1.0.0",
        "grunt-contrib-watch": "^1.0.0",
        "jshint-stylish": "^0.2.0",
        "load-grunt-tasks": "^0.4.0",
        "time-grunt": "^0.3.1"
    },
    "directories": {},
    "dist": {
        "shasum": "8abd095196b33b406791f1494b6b13b4422240c4",
        "tarball": "https://registry.npmjs.org/diskdb/-/diskdb-0.1.17.tgz"
    },
    "files": [
        "lib"
    ],
    "gitHead": "dd4a3ec7df52ae55c2247ba9e9892fdd1249a909",
    "homepage": "http://arvindr21.github.io/diskDB",
    "keywords": [
        "diskDB",
        "JSON",
        "Database",
        "file system",
        "CRUD",
        "lightweight"
    ],
    "license": "MIT",
    "main": "lib/diskdb.js",
    "maintainers": [
        {
            "name": "arvindr21",
            "email": "arvind.ravulavaru@gmail.com"
        }
    ],
    "name": "diskdb",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/arvindr21/diskdb.git"
    },
    "scripts": {
        "test": "grunt"
    },
    "version": "0.1.17"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module diskdb](#apidoc.module.diskdb)
1.  [function <span class="apidocSignatureSpan">diskdb.</span>connect (path, collections)](#apidoc.element.diskdb.connect)
1.  [function <span class="apidocSignatureSpan">diskdb.</span>loadCollections (collections)](#apidoc.element.diskdb.loadCollections)
1.  object <span class="apidocSignatureSpan">diskdb.</span>util

#### [module diskdb.util](#apidoc.module.diskdb.util)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>ObjectSearcher ()](#apidoc.element.diskdb.util.ObjectSearcher)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>finder (collection, query, multi)](#apidoc.element.diskdb.util.finder)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>isValidPath (path)](#apidoc.element.diskdb.util.isValidPath)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>readFromFile (file)](#apidoc.element.diskdb.util.readFromFile)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>removeFile (file)](#apidoc.element.diskdb.util.removeFile)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>removeFiltered (collection, query, multi)](#apidoc.element.diskdb.util.removeFiltered)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>updateFiltered (collection, query, data, multi)](#apidoc.element.diskdb.util.updateFiltered)
1.  [function <span class="apidocSignatureSpan">diskdb.util.</span>writeToFile (outputFilename, content)](#apidoc.element.diskdb.util.writeToFile)



# <a name="apidoc.module.diskdb"></a>[module diskdb](#apidoc.module.diskdb)

#### <a name="apidoc.element.diskdb.connect"></a>[function <span class="apidocSignatureSpan">diskdb.</span>connect (path, collections)](#apidoc.element.diskdb.connect)
- description and source-code
```javascript
connect = function (path, collections) {
    if (util.isValidPath(path)) {
        var _db = {};
        _db.path = path;
        this._db = _db;
        console.log(s('Successfully connected to : ' + path));
        if (collections) {
            this.loadCollections(collections);
        }
    } else {
        console.log(e('The DB Path [' + path + '] does not seem to be valid. Recheck the path and try again'));
        return false;
    }
    return this;
}
```
- example usage
```shell
...
Install the module locally :
'''bash
$ npm install diskdb
'''

'''js
var db = require('diskdb');
db = db.connect('/path/to/db-folder', ['collection-name']);
// you can access the traditional JSON DB methods here
'''

## Documentation
### Connect to DB
'''js
db.connect(pathToFolder, ['filename']);
...
```

#### <a name="apidoc.element.diskdb.loadCollections"></a>[function <span class="apidocSignatureSpan">diskdb.</span>loadCollections (collections)](#apidoc.element.diskdb.loadCollections)
- description and source-code
```javascript
loadCollections = function (collections) {
    if (!this._db) {
        console.log(e('Initialize the DB before you add collections. Use : ', 'db.connect(\'path-to-db\');'));
        return false;
    }
    if (typeof collections === 'object' && collections.length) {
        for (var i = 0; i < collections.length; i++) {
            var p = path.join(this._db.path, (collections[i].indexOf('.json') >= 0 ? collections[i] : collections[i] + '.json'));
            if (!util.isValidPath(p)) {
                util.writeToFile(p);
            }
            var _c = collections[i].replace('.json', '');
            this[_c] = new require('./collection')(this, _c);
        }
    } else {
        console.log(e('Invalid Collections Array.', 'Expected Format : ', '[\'collection1\',\'collection2\',\'collection3\']'));
    }
    return this;
}
```
- example usage
```shell
...
### Load Collections
Alternatively you can also load collections like

'''js
var db = require('diskdb');
// this
db = db.connect('/examples/db');
db.loadCollections(['articles']);
//or
db.connect('/examples/db');
db.loadCollections(['articles']);
//or
db.connect('/examples/db')
  .loadCollections(['articles']);
//or
...
```



# <a name="apidoc.module.diskdb.util"></a>[module diskdb.util](#apidoc.module.diskdb.util)

#### <a name="apidoc.element.diskdb.util.ObjectSearcher"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>ObjectSearcher ()](#apidoc.element.diskdb.util.ObjectSearcher)
- description and source-code
```javascript
ObjectSearcher = function () {
    this.results = [];
    this.objects = [];
    this.resultIDS = {};
}
```
- example usage
```shell
...
coltn._f = path.join(db._db.path, (collectionName + '.json'));

coltn.find = function(query) {
    var collection = JSON.parse(util.readFromFile(this._f));
    if (!query || Object.keys(query).length === 0) {
        return collection;
    } else {
        var searcher = new util.ObjectSearcher();
        return searcher.findAllInObject(collection, query, true);
    }
};

coltn.findOne = function(query) {
    var collection = JSON.parse(util.readFromFile(this._f));
    if (!query) {
...
```

#### <a name="apidoc.element.diskdb.util.finder"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>finder (collection, query, multi)](#apidoc.element.diskdb.util.finder)
- description and source-code
```javascript
finder = function (collection, query, multi) {
    var retCollection = [];
    loop: for (var i = collection.length - 1; i >= 0; i--) {
        var c = collection[i];
        for (var p in query) {
            if (p in c && c[p] == query[p]) {
                retCollection.push(collection[i]);
                if (!multi) {
                    break loop;
                }
            }
        }
    }
    return retCollection;
}
```
- example usage
```shell
...
        return data;
    }
};

coltn.update = function(query, data, options) {
    var ret = {},
        collection = JSON.parse(util.readFromFile(this._f)); // update
    var records = util.finder(collection, query, true);
    if (records.length) {
        if (options && options.multi) {
            collection = util.updateFiltered(collection, query, data, true);
            ret.updated = records.length;
            ret.inserted = 0;
        } else {
            collection = util.updateFiltered(collection, query, data, false);
...
```

#### <a name="apidoc.element.diskdb.util.isValidPath"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>isValidPath (path)](#apidoc.element.diskdb.util.isValidPath)
- description and source-code
```javascript
isValidPath = function (path) {
    return fs.existsSync(path);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.diskdb.util.readFromFile"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>readFromFile (file)](#apidoc.element.diskdb.util.readFromFile)
- description and source-code
```javascript
readFromFile = function (file) {
    return fs.readFileSync(file, 'utf-8');
}
```
- example usage
```shell
...

module.exports = function(db, collectionName) {
var coltn = {};
coltn.collectionName = collectionName;
coltn._f = path.join(db._db.path, (collectionName + '.json'));

coltn.find = function(query) {
    var collection = JSON.parse(util.readFromFile(this._f));
    if (!query || Object.keys(query).length === 0) {
        return collection;
    } else {
        var searcher = new util.ObjectSearcher();
        return searcher.findAllInObject(collection, query, true);
    }
};
...
```

#### <a name="apidoc.element.diskdb.util.removeFile"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>removeFile (file)](#apidoc.element.diskdb.util.removeFile)
- description and source-code
```javascript
removeFile = function (file) {
    return fs.unlinkSync(file);
}
```
- example usage
```shell
...
        if (typeof multi === 'undefined') {
            multi = true;
        }
        collection = util.removeFiltered(collection, query, multi);

        util.writeToFile(this._f, collection);
    } else {
        util.removeFile(this._f);
        delete db[collectionName];
    }
    return true;
};

coltn.count = function() {
    return (JSON.parse(util.readFromFile(this._f))).length;
...
```

#### <a name="apidoc.element.diskdb.util.removeFiltered"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>removeFiltered (collection, query, multi)](#apidoc.element.diskdb.util.removeFiltered)
- description and source-code
```javascript
removeFiltered = function (collection, query, multi) {
    // break 2 loops at once -  multi : false
    loop: for (var i = collection.length - 1; i >= 0; i--) {
        var c = collection[i];
        for (var p in query) {
            if (p in c && c[p] == query[p]) {
                collection.splice(i, 1);
                if (!multi) {
                    break loop;
                }
            }
        }
    }
    return collection;
}
```
- example usage
```shell
...

    coltn.remove = function(query, multi) {
if (query) {
    var collection = JSON.parse(util.readFromFile(this._f));
    if (typeof multi === 'undefined') {
        multi = true;
    }
    collection = util.removeFiltered(collection, query, multi);

    util.writeToFile(this._f, collection);
} else {
    util.removeFile(this._f);
    delete db[collectionName];
}
return true;
...
```

#### <a name="apidoc.element.diskdb.util.updateFiltered"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>updateFiltered (collection, query, data, multi)](#apidoc.element.diskdb.util.updateFiltered)
- description and source-code
```javascript
updateFiltered = function (collection, query, data, multi) {
    // break 2 loops at once - multi : false
    loop: for (var i = collection.length - 1; i >= 0; i--) {
        var c = collection[i];
        for (var p in query) {
            if (p in c && c[p] == query[p]) {
                collection[i] = merge(c, data);
                if (!multi) {
                    break loop;
                }
            }
        }
    }
    return collection;
}
```
- example usage
```shell
...

    coltn.update = function(query, data, options) {
var ret = {},
    collection = JSON.parse(util.readFromFile(this._f)); // update
var records = util.finder(collection, query, true);
if (records.length) {
    if (options && options.multi) {
        collection = util.updateFiltered(collection, query, data, true);
        ret.updated = records.length;
        ret.inserted = 0;
    } else {
        collection = util.updateFiltered(collection, query, data, false);
        ret.updated = 1;
        ret.inserted = 0;
    }
...
```

#### <a name="apidoc.element.diskdb.util.writeToFile"></a>[function <span class="apidocSignatureSpan">diskdb.util.</span>writeToFile (outputFilename, content)](#apidoc.element.diskdb.util.writeToFile)
- description and source-code
```javascript
writeToFile = function (outputFilename, content) {
    if (!content) {
        content = [];
    }
    fs.writeFileSync(outputFilename, JSON.stringify(content, null, 0));
}
```
- example usage
```shell
...
    var retCollection = [];
    for (var i = data.length - 1; i >= 0; i--) {
        var d = data[i];
        d._id = uuid.v4().replace(/-/g, '');
        collection.push(d);
        retCollection.push(d);
    }
    util.writeToFile(this._f, collection);
    return retCollection;
} {
    data._id = uuid.v4().replace(/-/g, '');
    collection.push(data);
    util.writeToFile(this._f, collection);
    return data;
}
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
