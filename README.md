# api documentation for  [migrate (v0.2.3)](https://github.com/visionmedia/node-migrate#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-migrate.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-migrate) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-migrate.svg)](https://travis-ci.org/npmdoc/node-npmdoc-migrate)
#### Abstract migration framework for node

[![NPM](https://nodei.co/npm/migrate.png?downloads=true)](https://www.npmjs.com/package/migrate)

[![apidoc](https://npmdoc.github.io/node-npmdoc-migrate/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-migrate_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-migrate/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-migrate/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-migrate/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "TJ Holowaychuk",
        "email": "tj@vision-media.ca"
    },
    "bin": {
        "migrate": "./bin/migrate"
    },
    "bugs": {
        "url": "https://github.com/visionmedia/node-migrate/issues"
    },
    "dependencies": {
        "dateformat": "^1.0.12"
    },
    "description": "Abstract migration framework for node",
    "devDependencies": {
        "mocha": "^2.2.1"
    },
    "directories": {},
    "dist": {
        "shasum": "4f436085e2d86dc6472539e55500b65b00179811",
        "tarball": "https://registry.npmjs.org/migrate/-/migrate-0.2.3.tgz"
    },
    "engines": {
        "node": ">= 0.4.x"
    },
    "gitHead": "3393559b9493a325e0a9358e9315f490efe8cdcb",
    "homepage": "https://github.com/visionmedia/node-migrate#readme",
    "keywords": [
        "migrate",
        "migrations"
    ],
    "license": "MIT",
    "main": "index",
    "maintainers": [
        {
            "name": "tjholowaychuk",
            "email": "tj@vision-media.ca"
        },
        {
            "name": "joaosa",
            "email": "jjadonotenter@gmail.com"
        },
        {
            "name": "linusu",
            "email": "linus@folkdatorn.se"
        }
    ],
    "name": "migrate",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/visionmedia/node-migrate.git"
    },
    "scripts": {
        "test": "mocha"
    },
    "version": "0.2.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module migrate](#apidoc.module.migrate)
1.  [function <span class="apidocSignatureSpan">migrate.</span>load (stateFile, migrationsDirectory)](#apidoc.element.migrate.load)
1.  [function <span class="apidocSignatureSpan">migrate.</span>set (path)](#apidoc.element.migrate.set)
1.  object <span class="apidocSignatureSpan">migrate.</span>set.prototype

#### [module migrate.set](#apidoc.module.migrate.set)
1.  [function <span class="apidocSignatureSpan">migrate.</span>set (path)](#apidoc.element.migrate.set.set)

#### [module migrate.set.prototype](#apidoc.module.migrate.set.prototype)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>_migrate (direction, migrationName, fn)](#apidoc.element.migrate.set.prototype._migrate)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>addMigration (title, up, down)](#apidoc.element.migrate.set.prototype.addMigration)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>down (migrationName, fn)](#apidoc.element.migrate.set.prototype.down)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>load (fn)](#apidoc.element.migrate.set.prototype.load)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>migrate (direction, migrationName, fn)](#apidoc.element.migrate.set.prototype.migrate)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>save (fn)](#apidoc.element.migrate.set.prototype.save)
1.  [function <span class="apidocSignatureSpan">migrate.set.prototype.</span>up (migrationName, fn)](#apidoc.element.migrate.set.prototype.up)



# <a name="apidoc.module.migrate"></a>[module migrate](#apidoc.module.migrate)

#### <a name="apidoc.element.migrate.load"></a>[function <span class="apidocSignatureSpan">migrate.</span>load (stateFile, migrationsDirectory)](#apidoc.element.migrate.load)
- description and source-code
```javascript
load = function (stateFile, migrationsDirectory) {

  var set = new Set(stateFile);
  var dir = path.resolve(migrationsDirectory);

  fs.readdirSync(dir).filter(function(file){
    return file.match(/^\d+.*\.js$/);
  }).sort().forEach(function (file) {
    var mod = require(path.join(dir, file));
    set.addMigration(file, mod.up, mod.down);
  });

  return set;
}
```
- example usage
```shell
...

'''

## Programmatic usage

'''javascript
var migrate = require('migrate');
var set = migrate.load('migration/.migrate', 'migration');

set.up(function (err) {
  if (err) throw err;

  console.log('Migration completed');
});
'''
...
```

#### <a name="apidoc.element.migrate.set"></a>[function <span class="apidocSignatureSpan">migrate.</span>set (path)](#apidoc.element.migrate.set)
- description and source-code
```javascript
function Set(path) {
  this.migrations = [];
  this.path = path;
  this.pos = 0;
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.migrate.set"></a>[module migrate.set](#apidoc.module.migrate.set)

#### <a name="apidoc.element.migrate.set.set"></a>[function <span class="apidocSignatureSpan">migrate.</span>set (path)](#apidoc.element.migrate.set.set)
- description and source-code
```javascript
function Set(path) {
  this.migrations = [];
  this.path = path;
  this.pos = 0;
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.migrate.set.prototype"></a>[module migrate.set.prototype](#apidoc.module.migrate.set.prototype)

#### <a name="apidoc.element.migrate.set.prototype._migrate"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>_migrate (direction, migrationName, fn)](#apidoc.element.migrate.set.prototype._migrate)
- description and source-code
```javascript
_migrate = function (direction, migrationName, fn){
  var self = this
    , migrations
    , migrationPos;

  if (!migrationName) {
    migrationPos = direction == 'up' ? this.migrations.length : 0;
  } else if ((migrationPos = positionOfMigration(this.migrations, migrationName)) == -1) {
    return fn(new Error("Could not find migration: " + migrationName));
  }

  switch (direction) {
    case 'up':
      migrations = this.migrations.slice(this.pos, migrationPos+1);
      break;
    case 'down':
      migrations = this.migrations.slice(migrationPos, this.pos).reverse();
      break;
  }

  function next(migration) {
    if (!migration) return fn(null);

    self.emit('migration', migration, direction);
    migration[direction](function(err){
      if (err) return fn(err);

      self.pos += (direction === 'up' ? 1 : -1);
      self.save(function (err) {
        if (err) return fn(err);

        next(migrations.shift())
      });
    });
  }

  next(migrations.shift());
}
```
- example usage
```shell
...
 var self = this;
 this.load(function(err, obj){
   if (err) {
     if ('ENOENT' != err.code) return fn(err);
   } else {
     self.pos = obj.pos;
   }
   self._migrate(direction, migrationName, fn);
 });
};

/**
* Get index of given migration in list of migrations
*
* @api private
...
```

#### <a name="apidoc.element.migrate.set.prototype.addMigration"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>addMigration (title, up, down)](#apidoc.element.migrate.set.prototype.addMigration)
- description and source-code
```javascript
addMigration = function (title, up, down){
  this.migrations.push(new Migration(title, up, down));
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.migrate.set.prototype.down"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>down (migrationName, fn)](#apidoc.element.migrate.set.prototype.down)
- description and source-code
```javascript
down = function (migrationName, fn){
  this.migrate('down', migrationName, fn);
}
```
- example usage
```shell
...
and state loaded from 'stateFile'.

### 'Set.up([migration, ]cb)'

Migrates up to the specified 'migration' or, if none is specified, to the latest
migration. Calls the callback 'cb', possibly with an error 'err', when done.

### 'Set.down([migration, ]cb)'

Migrates down to the specified 'migration' or, if none is specified, to the
first migration. Calls the callback 'cb', possibly with an error 'err', when
done.

## License
...
```

#### <a name="apidoc.element.migrate.set.prototype.load"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>load (fn)](#apidoc.element.migrate.set.prototype.load)
- description and source-code
```javascript
load = function (fn){
  this.emit('load');
  fs.readFile(this.path, 'utf8', function(err, json){
    if (err) return fn(err);
    try {
      fn(null, JSON.parse(json));
    } catch (err) {
      fn(err);
    }
  });
}
```
- example usage
```shell
...

'''

## Programmatic usage

'''javascript
var migrate = require('migrate');
var set = migrate.load('migration/.migrate', 'migration');

set.up(function (err) {
  if (err) throw err;

  console.log('Migration completed');
});
'''
...
```

#### <a name="apidoc.element.migrate.set.prototype.migrate"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>migrate (direction, migrationName, fn)](#apidoc.element.migrate.set.prototype.migrate)
- description and source-code
```javascript
migrate = function (direction, migrationName, fn){
  if (typeof migrationName === 'function') {
    fn = migrationName;
    migrationName = null;
  }
  var self = this;
  this.load(function(err, obj){
    if (err) {
      if ('ENOENT' != err.code) return fn(err);
    } else {
      self.pos = obj.pos;
    }
    self._migrate(direction, migrationName, fn);
  });
}
```
- example usage
```shell
...
* Run down migrations and call 'fn(err)'.
*
* @param {Function} fn
* @api public
*/

Set.prototype.down = function(migrationName, fn){
 this.migrate('down', migrationName, fn);
};

/**
* Run up migrations and call 'fn(err)'.
*
* @param {Function} fn
* @api public
...
```

#### <a name="apidoc.element.migrate.set.prototype.save"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>save (fn)](#apidoc.element.migrate.set.prototype.save)
- description and source-code
```javascript
save = function (fn){
  var self = this
    , json = JSON.stringify(this);
  fs.writeFile(this.path, json, function(err){
    if (err) return fn(err);

    self.emit('save');
    fn(null);
  });
}
```
- example usage
```shell
...
  if (!migration) return fn(null);

  self.emit('migration', migration, direction);
  migration[direction](function(err){
    if (err) return fn(err);

    self.pos += (direction === 'up' ? 1 : -1);
    self.save(function (err) {
      if (err) return fn(err);

      next(migrations.shift())
    });
  });
}
...
```

#### <a name="apidoc.element.migrate.set.prototype.up"></a>[function <span class="apidocSignatureSpan">migrate.set.prototype.</span>up (migrationName, fn)](#apidoc.element.migrate.set.prototype.up)
- description and source-code
```javascript
up = function (migrationName, fn){
  this.migrate('up', migrationName, fn);
}
```
- example usage
```shell
...

## Programmatic usage

'''javascript
var migrate = require('migrate');
var set = migrate.load('migration/.migrate', 'migration');

set.up(function (err) {
  if (err) throw err;

  console.log('Migration completed');
});
'''

## Creating Migrations
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
