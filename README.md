# template for frontend hackaton 

```bash
mkdir config 
mkdir src  src/scss src/css src/js src/fonts
mkdir dist dist/css dist/js dist/fonts
mkdir vendors
touch src/scss/app.scss src/js/app.js src/index.html
```


## Add Rakefile for html minification

```bash
cd vendor
curl https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/htmlcompressor/htmlcompressor-1.5.3.jar --output htmlcompressor-1.5.3.jar
touch Rakefile
```



```Rakefile
task :default => [:show]

task :show do
    puts 'build:html'
    puts 'build:scss'
    puts 'build:webpack'
end
namespace :build do
    # https://code.google.com/archive/p/htmlcompressor/
    # java -jar htmlcompressor.jar --type html -o /to/ /from/
    task :html do
        sh "java -jar vendor/htmlcompressor-1.5.3.jar --type html src/*.html -o dist/"
        #   -o output folder
    end
end

namespace :server do
    task :run do

    end
end
```


## build css from bootstrap using sass

```bash
gem install sass
```
add a task into Rakefile

```Rakefile
    task :css do
        sh "sass src\scss\app.scss:dist\css\app.css --style compact"
    end
```

## build css and copy the fonts files of font-awesome

```bash
cd vendor
git submodule add https://github.com/FortAwesome/Font-Awesome
```

copy the font from git submodule 

```Rakefile
    task :css do
        sh 'cp vendor/Font-Awesome/web-fonts-with-css/webfonts/* dist/fonts/'
        sh 'sass src\scss\app.scss:dist\css\app.css --style compact'
    end
```

## build js *(bootstrap) using webpack as submodule fail

bootstrap has two dependences: JQuery and popper.js




```bash
npm init
npm install webpack webpack-cli webpack-dev-server --save-dev

npm install jquery popper.js bootstrap

cd vendor
git submodule add https://github.com/jquery/jquery
cd vendor/jquery/
npm run build
# generate jquery.js jquery.min.js
git submodule add https://github.com/FezVrasta/popper.js
```

add to src/js/app.js

```javascript
/* into src/js/app.js */
require('../../vendor/jquery/dist/jquery.min.js')
require('../../vendor/popper.min.js')
require('../../vendor/bootstrap/dist/js/bootstrap.min.js')
``` 

create a config file to webpack

```bash
mkdir config
npm init -y
touch src/js/app.js
echo 'alert("hello world compilation from webpack")' >> src/js/app.js
touch config/webpack.dev.js
```

```javascript
const path=require("path")

module.exports = {
    mode: "development",
    entry:{
        app: "./src/js/app.js"
    },
    output:{
        filename: "[name]-bundle.js",
        path: path.resolve(__dirname,"../dist/js")
    },
}
```