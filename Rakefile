desc "Parse haml layouts"
task :haml do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/ && 
    for f in *.haml; do [ -e $f ] && haml $f ${f%.haml}.html; done
  })
  puts "done."
end

desc "synchronize with S3"
task :sync do
  system "s3cmd sync --rr --delete-removed _site/ s3://robin.wenglewski.de"
end

desc "Launch preview environment"
task :preview => [:haml, :clean] do
  system "jekyll --auto --server"
end

desc "Build site"
task :build => [:haml, :clean] do |task, args|
  system "jekyll"
end

task :clean do
  system "rm -rf _site"
end


namespace :compass do  

  desc 'Delete temporary compass files'
  task :clean do
    system "rm -fR css/*"
  end

  desc 'Run the compass watch script'
  task :watch do
    system "compass watch"
  end

  desc 'Compile sass scripts'
  task :compile => [:clean] do
    system "compass compile"
  end
  
end
