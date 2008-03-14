require 'capistrano/version'
load 'deploy' if respond_to?(:namespace) # cap2 differentiator
Dir['vendor/plugins/*/recipes/*.rb'].each { |plugin| load(plugin) }

# =============================================================

# General configuration settings, required for all recipes!
set :application, "patnakajima.com"
set :domain, "patnakajima.com"
# set :extra_domains, %w(www.project-domain.com)
role :app, domain
role :web, domain
role :db,  domain, :primary => true

set :user, "deploy"
set :group, "deploy"
default_run_options[:pty] = true
set :repository,  "git@github.com:nakajima/todo.git"
set :scm, "git"
set :branch, "origin/master"

# Deployment Settings
set :deploy_to, "/var/www/apps/#{application}"
set :config_files, %w(database.yml)

# SSH Keys for caching (you must generate these first.)
ssh_options[:keys] = %w(~/.ssh/id_dsa)

# =============================================================
# Thin Settings
# =============================================================
set :thin_servers, 1
set :thin_port, 8675
set :thin_environment, 'production'
set :thin_address, '127.0.0.1'
set :thin_conf, "#{shared_path}/config/thin.yml"

# =============================================================
# Nginx Settings
# =============================================================
set :nginx_sites_available, "/usr/local/nginx/sites-available"
set :nginx_sites_enabled, "/usr/local/nginx/sites-enabled"

# =============================================================
# Apache Settings
# =============================================================
set :apache_server_name, nil
set :apache_conf, "/usr/local/apache2/conf/apps/#{application}.conf"
# set :apache_default_vhost, false
# set :apache_default_vhost_conf, nil
set :apache_ctl, "/usr/local/apache2/bin/apachectl"
set :apache_server_aliases, []
set :apache_proxy_port, mongrel_port
set :apache_proxy_servers, mongrel_servers
set :apache_proxy_address, mongrel_address
# set :apache_ssl_enabled, false
# set :apache_ssl_ip, nil
# set :apache_ssl_forward_all, false
# set :apache_ssl_chainfile, false
set :local_apache_ctl_path, apache_ctl