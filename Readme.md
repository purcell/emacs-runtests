Under construction

Example runtests script

```sh
#!/bin/bash
rootDir="$(git rev-parse --show-toplevel)"
if grep -qm 1 defineTest $1
then
    description="$(grep -m 1 "describe(" $1 | sed 's/\s*describe(//' | sed 's/, function.*//')"
    currentDir="$(pwd)"
    QUERY=$(node -e "console.log(decodeURIComponent($description))")
    cd $rootDir
    echo "define test $currentDir $rootDir '$QUERY'"
    ./node_modules/mocha-phantomjs/bin/mocha-phantomjs -R dot http-pub/test/index.html?grep=$QUERY
    cd $currentDir
else
    $rootDir/node_modules/mocha/bin/mocha -b -R dot --colors $*
fi
```
