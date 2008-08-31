$:.unshift(File.join(File.dirname(__FILE__), 'lib'))

require 'rake'
require 'spec/rake/spectask'
require 'roodi'

desc "Run all specs"
Spec::Rake::SpecTask.new('spec') do |t|
  t.spec_files = FileList['spec/**/*spec.rb']
end

desc "Run Roodi against all source files"
task :roodi do
  pattern = File.join(File.dirname(__FILE__), "**", "*.rb")
  roodi(Dir.glob(pattern))
end

task :roodi_runway do
  pattern = File.join("/Users/marty/Data/runway", "**", "*.rb")
  roodi(Dir.glob(pattern))
end

def roodi(ruby_files)
  roodi = Roodi::Core::Runner.new(Roodi::Checks::ClassNameCheck.new, 
                                  Roodi::Checks::CyclomaticComplexityBlockCheck.new,
                                  Roodi::Checks::CyclomaticComplexityMethodCheck.new,
                                  Roodi::Checks::EmptyRescueBodyCheck.new,
                                  Roodi::Checks::ForLoopCheck.new,
                                  # Roodi::Checks::MagicNumberCheck.new,
                                  Roodi::Checks::MethodNameCheck.new, 
                                  Roodi::Checks::MethodLineCountCheck.new)
  ruby_files.each { |file| roodi.check_file(file) }
  roodi.errors.each {|error| puts error}
  puts "\nFound #{roodi.errors.size} errors."
end