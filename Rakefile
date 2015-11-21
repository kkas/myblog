# coding: utf-8

desc "Push the site directory to github pages as the subdirectory"
task :site do |task, args|
  subdir = 'site'
  puts subdir
  sh "git subtree push --prefix #{subdir} origin gh-pages"
end
