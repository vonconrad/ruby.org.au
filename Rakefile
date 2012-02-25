require "rubygems"
require "bundler/setup"

require "tilt"

PAGES = %w(index)

task :default => 'build:all'

namespace :build do
  task :stylesheets do
    sh 'compass compile -c compass-config.rb'
  end

  task :pages do
    layout = Tilt.new('layout.html.erb')
    PAGES.each do |template|
      puts "Rendering pages/#{template}"
      File.open("site/#{template}.html", "w") do |f|
        f << layout.render do
          Tilt.new("pages/#{template}.html.erb").render
        end
      end
    end
  end

  task :all => [:stylesheets, :pages]
end

task :deploy do
  gh_pages = `git show-ref -s refs/heads/gh-pages`.strip
  site = `git ls-tree -d HEAD site | awk '{print $3}'`.strip
  new_commit = `echo 'Update site' | git commit-tree #{site} -p #{gh_pages}`.strip
  `git update-ref refs/heads/gh-pages #{new_commit}`
end
