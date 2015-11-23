# coding: utf-8
require 'rubygems'

subdir = 'site'
destdir = 'site/_site'

desc "Push the site directory to github pages as the subdirectory"
task :site do |task, args|
  sh "git subtree push --prefix #{subdir} origin gh-pages"
end

desc "Generate the site in the "
task :generate do
  sh "jekyll build --source #{subdir} --destination #{destdir}"
end

# reference: https://github.com/jekyll/jekyll/blob/master/Rakefile
desc "Run jekyll serve"
task :serve do
  require 'jekyll'

  options = {
    'source' => File.expand_path(subdir),
    'destination' => File.expand_path(destdir),
    'watch' => true,
    'serving' => true
  }
  Jekyll::Commands::Build.process(options)
  Jekyll::Commands::Serve.process(options)
end
