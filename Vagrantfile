# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.ssh.insert_key = false
    config.vm.define "lein-nrepl"
    config.vm.network "forwarded_port", guest: 4343, host: 4343
    config.vm.provision "shell", inline: <<-SHELL
export DEBIAN_FRONTEND=noninteractive

echo "Installing Java"
apt-get update -qq
apt-get install -y -qq --no-install-recommends default-jre default-jdk >/dev/null 2>&1

echo "Installing Leiningen"
(
sudo -snu vagrant
mkdir -p /home/vagrant/bin
wget -qO /home/vagrant/bin/lein https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
chmod a+x /home/vagrant/bin/lein
)

echo <<EOT >/etc/init/nrepl.conf
description "Leiningen nREPL headless"
start on vagrant-mounted

expect fork

script
exec sudo -nu vagrant /home/vagrant/bin/lein repl :headless :host 0.0.0.0 :port 4343 &
end script
EOT

start nrepl
    SHELL
end
