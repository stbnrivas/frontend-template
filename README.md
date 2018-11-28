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
        # sh "sass src\scss\app.scss:dist\css\app.css --style watch"
        # sh "sass src\scss\app.scss:dist\css\app.css --style nested"
        sh "sass src\scss\app.scss:dist\css\app.css --style compact"
        # sh "sass src\scss\app.scss:dist\css\app.css --style expanded"
        # sh "sass src\scss\app.scss:dist\css\app.css --style compressed"
    end
```
