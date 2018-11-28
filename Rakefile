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
    task :css do
        # sh "sass src\scss\app.scss:dist\css\app.css --style watch"
        # sh "sass src\scss\app.scss:dist\css\app.css --style nested"
        sh "sass src\scss\app.scss:dist\css\app.css --style compact"
        # sh "sass src\scss\app.scss:dist\css\app.css --style expanded"
        # sh "sass src\scss\app.scss:dist\css\app.css --style compressed"
    end
    task :watch do
    end
end



namespace :server do
    task :run do

    end
end