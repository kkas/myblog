# coding: utf-8

subdir = 'site'

desc "Push the site directory to github pages as the subdirectory"
task :site do |task, args|
  sh "git subtree push --prefix #{subdir} origin gh-pages"
end
