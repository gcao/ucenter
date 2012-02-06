load 'deploy' if respond_to?(:namespace) # cap2 differentiator

raise "Environment variable CHEF_SERVER is not set." unless ENV["CHEF_SERVER"]
raise "Environment variable CHEF_USER is not set." unless ENV["CHEF_USER"]

set :application, "ucenter"
set :deploy_to, "/data/apps/#{application}"
 
set :scm, :git
set :repository, "git://github.com/gcao/#{application}.git"

set :normalize_asset_timestamps, false

set :user, ENV["CHEF_USER"]
set :use_sudo, ENV["CHEF_USER"] != 'root'

server ENV["CHEF_SERVER"], :app, :web, :db, :primary => true

after "deploy:update_code", :copy_over_config_files

task :copy_over_config_files do
  run "cp -rf #{deploy_to}/#{shared_dir}/config/* #{release_path}/"
end

