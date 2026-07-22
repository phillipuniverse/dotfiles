require 'rake'

# foo.symlink links to ~/.foo; foo.symlink-nodot links to ~/foo
def link_target(linkable)
  file = linkable.split('/').last
  if file.end_with?('.symlink-nodot')
    "#{ENV["HOME"]}/#{file.sub(/\.symlink-nodot$/, '')}"
  else
    "#{ENV["HOME"]}/.#{file.sub(/\.symlink$/, '')}"
  end
end

desc "Hook our dotfiles into system-standard positions."
task :install do
  linkables = Dir.glob('*/**{.symlink,.symlink-nodot}')

  skip_all = false
  overwrite_all = false
  backup_all = false

  linkables.each do |linkable|
    overwrite = false
    backup = false

    target = link_target(linkable)

    if File.exists?(target) || File.symlink?(target)
      unless skip_all || overwrite_all || backup_all
        puts "File already exists: #{target}, what do you want to do? [s]kip, [S]kip all, [o]verwrite, [O]verwrite all, [b]ackup, [B]ackup all"
        case STDIN.gets.chomp
        when 'o' then overwrite = true
        when 'b' then backup = true
        when 'O' then overwrite_all = true
        when 'B' then backup_all = true
        when 'S' then skip_all = true
        when 's' then next
        end
      end
      next if skip_all
      FileUtils.rm_rf(target) if overwrite || overwrite_all
      `mv "#{target}" "#{target}.backup"` if backup || backup_all
    end
    `ln -s "$PWD/#{linkable}" "#{target}"`
  end
end

task :uninstall do

  Dir.glob('**/*{.symlink,.symlink-nodot}').each do |linkable|

    target = link_target(linkable)

    # Remove all symlinks created during installation
    if File.symlink?(target)
      FileUtils.rm(target)
    end

    # Replace any backups made during installation
    if File.exists?("#{target}.backup")
      `mv "#{target}.backup" "#{target}"`
    end

  end
end

task :default => 'install'
