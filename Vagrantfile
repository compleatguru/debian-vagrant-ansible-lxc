# -*- mode: ruby -*-
# vi: set ft=ruby :

# Notes
# Install Vagrant Cachier
# vagrant plugin install vagrant-cachier

# TODO
# - rename mydev.dev to your app host name
# - change IP Address
# - add/replace the synced folder as needed

#If your Vagrant version is lower than 1.5, you can still use this provisioning
#by commenting or removing the line below and providing the config.vm.box_url parameter,
#if it's not already defined in this Vagrantfile. Keep in mind that you won't be able
#to use the Vagrant Cloud and other newer Vagrant features.
Vagrant.require_version ">= 1.5"

# Check to determine whether we're on a windows or linux/os-x host,
# later on we use this to launch ansible in the supported way
# source: https://stackoverflow.com/questions/2108727/which-in-ruby-checking-if-program-exists-in-path-from-ruby
def which(cmd)
    exts = ENV['PATHEXT'] ? ENV['PATHEXT'].split(';') : ['']
    ENV['PATH'].split(File::PATH_SEPARATOR).each do |path|
        exts.each { |ext|
            exe = File.join(path, "#{cmd}#{ext}")
            return exe if File.executable? exe
        }
    end
    return nil
end

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "debian/wheezy64"

  config.vm.hostname = 'mydev.dev'

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false


  config.ssh.forward_agent = true
  
  # Vagrant Cachier
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box

    config.cache.synced_folder_opts = {}
  end

  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL

  # lxc configuration
  config.vm.provider :lxc do |lxc|
    # IPv4 Address
    # lxc.customize 'network.ipv4', '10.0.3.10/24'

    # Memory
    # lxc.customize 'cgroup.memory.limit_in_bytes', '128M'
  end


#  config.vm.provision "shell", inline: <<-SHELL
#    sudo apt-get update
#    sudo apt-get upgrade
#  SHELL


  # Synced Folders
  config.vm.synced_folder "./", "/vagrant"
  config.vm.synced_folder "./app", "/var/www/html/app"
end
