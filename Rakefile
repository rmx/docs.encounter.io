require 'nanoc3/tasks'

desc "Compile the site"
task :compile do
  `nanoc compile`
end

desc "Publish to http://docs.rmx.im"
task :publish => [ :clean ] do
  FileUtils.rm_r('public') if File.exist?('public')

  `nanoc compile`

  # this should not be necessary, but I can't figure out how to
  # just keep a goddamn static file in the root with nanoc
  File.open("public/CNAME", 'w+') do |f|
    f.puts("docs.encounter.io")
  end

  ENV['GIT_DIR'] = File.expand_path(`git rev-parse --git-dir`.chomp)
  old_sha = `git rev-parse refs/remotes/origin/gh-pages`.chomp
  Dir.chdir('public') do
    ENV['GIT_INDEX_FILE'] = gif = '/tmp/docs.rmx.im-index'
    ENV['GIT_WORK_TREE'] = Dir.pwd
    File.unlink(gif) if File.file?(gif)
    `git add -A`
    tsha = `git write-tree`.strip
    puts "Created tree   #{tsha}"
    if old_sha.size == 40
      csha = `echo 'boom' | git commit-tree #{tsha} -p #{old_sha}`.strip
    else
      csha = `echo 'boom' | git commit-tree #{tsha}`.strip
    end
    puts "Created commit #{csha}"
    puts `git show #{csha} --stat`
    puts "Updating gh-pages from #{old_sha}"
    `git update-ref refs/heads/gh-pages #{csha}`
    `git push origin gh-pages`
  end
end

task :ref, :name do |t, args|
  name = ARGV.first.gsub(/^ref\[(.*)\]$/, '\1').split(' :: ')
  File.open('./content/api/ref/' + name[0] + '.md', 'w') do |f|
    f.write <<EOF
---
title: API - Reference - #{name[0]}
---

### #{name[0]} :: #{name[1]}
EOF
  end
end

task :event, :name do |t, args|
  name = ARGV.first.gsub(/^event\[(.*)\]$/, '\1').split(' :: ')
  File.open('./content/api/event/' + name[0] + '.md', 'w') do |f|
    f.write <<EOF
---
title: API - event - #{name[0]}
---

### event #{name[0]}

#{ if name[1] then
"## Event Data\n\n" + name[1].split(',').map {|x|
  "<span class='event-data-field'>" + x.strip + "</span>\n"
}.join("\n")
end }
EOF
  end
end
