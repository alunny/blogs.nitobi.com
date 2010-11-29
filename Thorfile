require 'erb'
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
  
  desc "new_post TITLE IS MULTIPLE WORDS", "New blog post"
  method_options :editor=>:boolean, :verbose=>:boolean
  def new_post(*args)
    template_file = '_meta/_posts/new_post.md'
    basename = Date.today.to_s + "-#{ args.join('-') }"
    
    output_file = template_file.sub('_meta','').sub('new_post', basename)
    title = args.map {|e| e.capitalize}.join(' ')
    result = string_from_template(template_file, :title=>title)
    output_file = create_output_file(output_file, result)
    
    system(ENV['EDITOR'], output_file) if options['editor']
  end

  ################# helpers for dealing with erb
  no_tasks do
    def string_from_template(file, variables)
      variables.each {|k,v| instance_variable_set("@#{k}", v) }
      translated_string = ::ERB.new(File.read(file)).result(binding)
    end
  
    def create_output_file(relative_file, output, local=false)
      destination_dir = options['local'] ? '_site' : root_dir
      FileUtils.mkdir_p(destination_dir)
      destination_file = File.join(destination_dir, relative_file)
      FileUtils.mkdir_p File.dirname(destination_file)
      puts "Created file: #{destination_file}" if options['verbose']
      File.open(destination_file, 'w') {|f| f.write(output) }
      destination_file
    end
  
    def root_dir
      File.expand_path(File.join(File.dirname(__FILE__)))
    end
  end
end
