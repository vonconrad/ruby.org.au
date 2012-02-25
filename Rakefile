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
      File.open("output/#{template}.html", "w") do |f|
        f << layout.render do
          Tilt.new("pages/#{template}.html.erb").render
        end
      end
    end
  end

  task :all => [:stylesheets, :pages]
end
