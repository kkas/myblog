# coding: utf-8

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
