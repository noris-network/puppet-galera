require 'rake'
require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
require 'json'

PuppetSyntax.exclude_paths ||= []
PuppetSyntax.exclude_paths << "spec/fixtures/**/*"
PuppetSyntax.exclude_paths << "pkg/**/*"
PuppetSyntax.exclude_paths << "vendor/**/*"

Rake::Task[:lint].clear
PuppetLint::RakeTask.new :lint do |config|
  config.ignore_paths = ["spec/**/*.pp", "vendor/**/*.pp"]
  config.fail_on_warnings = true
  config.log_format = '%{path}:%{linenumber}:%{KIND}: %{message}'
  config.disable_checks = ["80chars", "class_inherits_from_params_class",]
end

desc "Run acceptance tests"
RSpec::Core::RakeTask.new(:acceptance) do |t|
  t.pattern = 'spec/acceptance'
end

task :default => [:spec, :lint]
