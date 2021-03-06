require 'rake'
require 'rake/rdoctask' 
require 'rspec/core/rake_task'

desc 'Default: run spec tests.'
task :default => :rspec
task :test    => :rspec

desc "Run all specs"
RSpec::Core::RakeTask.new(:rspec) do |t|
  t.pattern = 'spec/**/*_spec.rb'
  t.rspec_opts = ["-c", "-f progress"]
end

desc "Run all specs with RCov"
RSpec::Core::RakeTask.new(:rcov) do |t|
  t.pattern = 'spec/**/*_spec.rb'
  t.rcov = true          
  t.rspec_opts = ["-c", "-f progress"]
  t.rcov_opts = %w{--exclude spec\/}
end   

desc 'Generate documentation for the acts_as_textcaptcha plugin.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'doc'
  rdoc.title    = 'acts_as_textcaptcha'
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README.rdoc', 'LICENSE')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gemspec|
    gemspec.name = "acts_as_textcaptcha"
    gemspec.summary = "Spam protection for your models via logic questions and the excellent textcaptcha.com api"
    gemspec.description = "Spam protection for your ActiveRecord models using logic questions and the excellent textcaptcha api. See textcaptcha.com for more details and to get your api key.
  The logic questions are aimed at a child's age of 7, so can be solved easily by all but the most cognitively impaired users. As they involve human logic, such questions cannot be solved by a robot.
  For more reasons on why logic questions are useful, see here; http://textcaptcha.com/why"
    gemspec.email = "matt@hiddenloop.com"
    gemspec.homepage = "http://github.com/matthutchinson/acts_as_textcaptcha"
    gemspec.authors = ["Matthew Hutchinson"]
    gemspec.files   = [Dir.glob("{lib}/**/*"), Dir.glob("{config}/*")]
    gemspec.add_dependency('bcrypt-ruby', '~> 2.1.2')
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
end

begin
  require 'metric_fu'
  MetricFu::Configuration.run do |config|
    config.metrics  = [ :churn, :saikuro, :flog, :flay, :reek, :roodi, :rcov ]
    config.graphs   = [ :flog, :flay, :reek, :roodi, :rcov ]
    config.flay     = { :dirs_to_flay => ['lib'],
                        :minimum_score => 75  }
    config.flog     = { :dirs_to_flog => ['lib']  }
    config.reek     = { :dirs_to_reek => ['lib']  }
    config.roodi    = { :dirs_to_roodi => ['lib'] }
    config.saikuro  = { :output_directory => 'tmp/metric_fu/scratch/saikuro',
                        :input_directory => ['lib'],
                        :cyclo => "",
                        :filter_cyclo => "0",
                        :warn_cyclo => "5",
                        :error_cyclo => "7",
                        :formater => "text" }
    config.churn    = { :start_date => "1 year ago", :minimum_churn_count => 10 }
    config.rcov     = { :environment => 'test',
                        :test_files => ['spec/*_spec.rb'],
                        :rcov_opts => ["--sort coverage",
                                       "--no-html",
                                       "--text-coverage",
                                       "--no-color",
                                       "--profile",
                                       "--rails",
                                       "--exclude spec"]}
    config.graph_engine = :bluff
  end
rescue LoadError
  puts "Metric Fu not available. Install it with: sudo gem install metric_fu reek roodi flay googlecharts"
end
