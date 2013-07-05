# vagrant plugin install vagrant-berkshelf

Vagrant.configure("2") do |config|
  config.berkshelf.enabled = true

  config.vm.box = "quantal64"
  config.vm.box_url = "http://dl.dropbox.com/u/13510779/lxc-quantal-amd64-2013-05-08.box"

  #config.vm.define :web do |web|
    #web.vm.box = "nginx"
  #end

  config.vm.provider :lxc do |lxc|
    # Same effect as as 'customize ["modifyvm", :id, "--memory", "1024"]' for VirtualBox
    lxc.customize 'cgroup.memory.limit_in_bytes', '1024M'
  end

  #config.vm.network :hostonly, "33.33.33.10"  

  config.vm.provision :chef_solo do |chef|
    chef.log_level      = :debug
    chef.cookbooks_path = ["~/.berkshelf/cookbooks/"]

    # Рецепт устанавливает nginx, unicorn, rbenv, gem, bundle
    chef.add_recipe "rails-lastmile" 

    chef.json = {
      'rails-lastmile' => {
        # 'app_dir' => '/vagrant',
        'ruby_version' => '2.0.0-p195',
        'environment' => 'develomnet'

      }
    }
  end
end
