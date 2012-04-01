require "rubygems"
require "bundler/setup"

require "tilt"

PAGES = %w(index)

task :default => 'build:all'

namespace :build do
  desc "Build the stylesheets, outputting to ./site/css"
  task :stylesheets do
    sh 'compass compile -c compass-config.rb'
  end
  
  desc "Build the javascripts, outputting to ./site/js"
  task :javascripts do
    sh 'mkdir -p ./site/js'
    sh 'cp -r javascripts/*.js ./site/js'
  end

  desc "Copy the static images to ./site/images"
  task :images do
    sh 'mkdir -p ./site/images'
    sh 'cp -r images/* ./site/images'
  end
  
  desc "Setup the CNAME"
  task :cname do
    sh 'cp CNAME ./site/'
  end

  desc "Build the page templates, outputting to ./site"
  task :pages do
    layout = Tilt.new('layout.html.haml')
    PAGES.each do |template|
      puts "Rendering pages/#{template}"
      File.open("site/#{template}.html", "w") do |f|
        f << layout.render do
          Tilt.new("pages/#{template}.html.haml").render
        end
      end
    end
  end

  desc "Build all the dynamic bits of the site"
  task :all => [:stylesheets, :javascripts, :pages, :cname, :images]
end

desc "Commit the latest version of the site to the gh-pages branch"
task :deploy do
  site = `git ls-tree -d HEAD site | awk '{print $3}'`.strip
  new_commit = `echo 'Update site' | git commit-tree #{site} -p refs/heads/gh-pages`.strip
  `git update-ref refs/heads/gh-pages #{new_commit}`
end
