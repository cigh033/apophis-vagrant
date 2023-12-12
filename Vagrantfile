$script = <<-'SCRIPT'
pacman -Sy
ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
hwclock --systohc
pacman --noconfirm -R virtualbox-guest-utils-nox && pacman --noconfirm -S virtualbox-guest-utils
pacman --noconfirm -S networkmanager vim fish zsh chezmoi
systemctl enable NetworkManager
systemctl enable vboxservice
echo KEYMAP=de > /etc/vconsole.conf
echo apophis > /etc/hostname
sudo -u vagrant mkdir -p /home/vagrant/.config/chezmoi/
sudo -u vagrant echo '[data]' > /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'email = "simon@burgr.io"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'name = "sb"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'shell = "fish"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'isServer = "false"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'isWorkMachine = "true"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'manualSetup = "false"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'isVirtual = "true"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant echo 'isMobile = "false"' >> /home/vagrant/.config/chezmoi/chezmoi.toml
sudo -u vagrant chezmoi init cigh033 --apply
reboot
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"
  config.vm.provider "virtualbox" do |v|
    # https://www.vagrantup.com/docs/providers/virtualbox/configuration
    v.gui = true
    v.name = "apophis_vagrant"
    v.linked_clone = true
    v.check_guest_additions = true
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
    v.customize ["modifyvm", :id, "--vram", "64"] #video ram in MB
    v.memory = 2048
    v.cpus = 2
  end
  config.vm.provision "shell", inline: $script
end
