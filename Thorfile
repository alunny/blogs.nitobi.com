require 'fileutils'
require 'net/ssh'

class Blog < Thor
  @@user = "alunny"
  @@server = "blogs.nitobi.com"
  
  method_options  :verbose=>:boolean
  def initialize(*args)
    super
  end
  
  desc "deploy", "Update site on blogs.nitobi.com/alunny"
  method_options
  def deploy
    commands = "cd myblog/blogs.nitobi.com; git pull origin master; jekyll"
    Net::SSH.start(@@server, @@user) do |ssh|
      result = ssh.exec! commands
      puts result if options["verbose"]
    end
  end

end