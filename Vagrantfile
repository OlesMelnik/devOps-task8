
Vagrant.configure("2") do |config|
  config.vm.define "vm1" do |vm1|
    config.vm.box = "centos/7"
    config.vm.provision "file", source: "index.html", destination: "/home/vagrant/index.html"

    config.vm.network "forwarded_port", guest: 80, host: 8888, host_ip: "127.0.0.1"
    config.vm.network "forwarded_port", guest: 443, host: 8443, host_ip: "127.0.0.1"
    
    config.vm.provision "shell", inline: <<-SHELL
     yum install -y httpd mod_ssl openssl
     openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -subj "/C=UA/ST=Lviv/L=Lviv/O=MEL, LLC/CN=MEL" -keyout /etc/pki/tls/private/localhost.key -out /etc/pki/tls/certs/localhost.crt
     cp /home/vagrant/index.html /var/www/html
     systemctl start httpd
     systemctl enable httpd
     SHELL
  end
end
