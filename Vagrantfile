# encoding: utf-8

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian-6.0.6-mrtn-v2"
  config.vm.box_url = "~/Downloads/debian-6.0.6-mrtn-v2.box"
  config.ssh.forward_agent = true
  config.vm.synced_folder "~/code", "/code"

  config.vm.network :forwarded_port, guest: 4000, host: 4000
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 4567, host: 4567
  config.vm.network :forwarded_port, guest: 5432, host: 5432
  config.vm.network :forwarded_port, guest: 9292, host: 9292

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe "apt"
    chef.add_recipe 'git'
    chef.add_recipe 'postgresql'
    chef.add_recipe 'ruby_build'
    chef.add_recipe 'rbenv::user'
    chef.add_recipe 'redis'
    chef.json = {
      'rbenv' => {
        'user_installs' => [
          { 'user' => 'vagrant',
            'rubies' => ['1.9.3-p392'],
            'global' => '1.9.3-p392',
            'gems' => {
              '1.9.3-p392' => [
                { 'name'    => 'bundler' },
                { 'name'    => 'pg' }
              ]
            }
          }
        ]
      }
    }
  end
end
