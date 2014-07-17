Vagrant.configure("2") do |config|

  config.vm.define "dev-vagrant-docker"
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :forwarded_port, host: 4243, guest: 4243
  config.vm.network :forwarded_port, host: 8080, guest: 8080
  config.vm.network :forwarded_port, host: 6379, guest: 6379

  config.vm.provider :virtualbox do |v, override|
    v.customize ["modifyvm", :id, "--memory", "2048"]
    v.customize ["modifyvm", :id, "--cpus", "4"]
  end

  config.vm.provision "docker" do |d|
    redis = "dockerfile/redis"
    d.pull_images redis
    d.run redis,
      args: "-p 6379:6379 -d"

    nginx = "dockerfile/nginx"
    d.pull_images nginx
    d.run nginx,
      args: "-p 8080:80 -d"
  end

end
