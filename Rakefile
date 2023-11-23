require "logstash/devutils/rake"

task :vendor => "gradle.properties" do
  sh "#{File.join(Dir.pwd, 'gradlew')} clean vendor"
end

file "gradle.properties" do
  root_dir = File.dirname(__FILE__)
  gradle_properties_file = "#{root_dir}/gradle.properties"
  # Use same JRuby that launched this Rake
  current_ruby_path = RbConfig::CONFIG['prefix']
  lsc_path = `#{current_ruby_path}/bin/jruby -S bundle show logstash-core`
  FileUtils.rm_f(gradle_properties_file)
  File.open(gradle_properties_file, "w") do |f|
    f.puts "logstashCoreGemPath=#{lsc_path}"
  end
  puts "-------------------> Wrote #{gradle_properties_file}"
  puts File.read(gradle_properties_file)
end
