require 'active_record'
require 'pry'

task :environment do
  ENV["ACTIVE_RECORD_ENV"] ||= "development"
  require_relative './config/environment'
end

include ActiveRecord::Tasks
DatabaseTasks.db_dir = 'db'
DatabaseTasks.migrations_paths = 'db/migrate'
seed_loader = Class.new do
  def load_seed
    load "#{ActiveRecord::Tasks::DatabaseTasks.db_dir}/seeds.rb"
  end
end

DatabaseTasks.seed_loader = seed_loader.new
load 'active_record/railties/databases.rake'

desc 'starts a console'
task :console => :environment do
  ActiveRecord::Base.logger = Logger.new(STDOUT)
  Pry.start
end

desc 'runs run.rb'
task :run do
  ActiveRecord::Base.logger = Logger.new(STDOUT)
  load "./bin/run.rb"
end
