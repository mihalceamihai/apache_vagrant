Vagrant.configure("2") do |apache|
  ENV['LC_ALL']='en_US.UTF-8'
  
  apache.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
     vb.cpus = "2"
     vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end

  apache.vm.box = "maier/alpine-3.6-x86_64"
  apache.vm.network "forwarded_port", guest: 80, host: 8080
  #apache.vm.network "private_network", ip: "10.0.0.10", auto_config: false

  apache.vm.provision :shell do |shell|
      shell.inline = <<-SHELL
        sudo su
	apk update && apk upgrade
	apk add apache2 
	#apk-add-repository ppa:ondrej/php
        apk add php7 php7-fpm php7-opcache
	apk add php7-gd php7-mysqli php7-zlib php7-curl php7-session 
        apk add php7-apache2
	rc-update add apache2 default
	rc-update add php-fpm7 default
	rc-service apache2 restart
	rc-service php-fpm7 restart
	rm /var/www/localhost/htdocs/index.html
        cp -dr /vagrant/tema_web /var/www/localhost/htdocs/	
      SHELL
  end
end
