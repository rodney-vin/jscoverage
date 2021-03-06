jscoverage
==========
![logo](https://raw.github.com/fishbar/jscoverage/master/logo.png)

jscoverage tool, both node.js or javascript support

[![Build Status](https://travis-ci.org/fishbar/jscoverage.svg)](https://travis-ci.org/fishbar/jscoverage)


### install

```sh
npm install jscoverage
```

### changelog

from v0.5.0， jscoverage start using uglify2, and enhance the coverage range.
now, jscoverage will find out which branch you missed!
jscoverage can run with mocha, even with mocha's html-cov reporter.
since mocha's html-cov dose not display branch cov info, jscoverage supply a new html-cov reporter

### get source code

```sh
git clone git://github.com/fishbar/jscoverage.git
```

### using jscoverage with mocha

let mocha load jscoverage using -r options, like:
```sh
mocha -r jscoverage --covignore .covignore --covout html --covinject true test
```
the case above, mocha do nothing with these options: --covignore , --covout --covinject
but jscoverage can recognise them, all support options are here:

  --covignore [filepath] # like gitignore, tell jscoverage to ignore these files

  --covout [output report] # can be: summary, detail, json, html, lcov, default summary

  --coverage [high,middle,low] # coverage level, default is: 90,70,30 , means 90% is high, 30% is low

  --covinject [boolean] # switch if inject code for easytest(exports._get, _replace, _reset), default is false

default jscoverage will search .covignore in the project root

### using jscoverage as cli command

```shell
jscoverage
# print help info
jscoverage source.js
# convert source.js to source-cov.js
jscoverage source.js dest.js
# convert source.js to dest.js
jscoverage sourcedir destdir --exclude a.js,b.js,c.js,*.min.js
# convert all files in sourcedir to destdir, exclude list will be ignored
```
jscoverage will copy exclude file from source dir to dest dir

### using jscoverage programmatically

comming soon

### using inject api for node.js test

```js
var testMod = require('module/for/test.js');

testMod._get('name');
testMod._replace('name', value);
testMod._reset();
testMod._call();
```
### inline ignore annotation

using bellow comment, jscoverage will ignore the following block/statement

```js
  /* @covignore */
```

### mocha global leaks detect

The follow object will be detected, all of them are created by jscoverage.

  * _$jscoverage
  * _$jscmd

