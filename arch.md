## 安装教程
- [https://archlinuxstudio.github.io/ArchLinuxTutorial](https://archlinuxstudio.github.io/ArchLinuxTutorial)
- [https://arch.icekylin.online/](https://arch.icekylin.online/)

## 安装系统
```shell
vim /etc/pacman.d/mirrorlist
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
```
```shell
pacstrap /mnt base base-devel linux linux-headers linux-firmware
```

```shell
# 添加用户
useradd -m -G wheel -s /bin/bash laughing
passwd laughing
EDITOR=vim visudo
# 去掉这一行的注释
#%wheel ALL=(ALL) ALL
```

<++>


## First
拔掉U盘之前需要安装的
```shell
pacman -S networkmanager openssh vim zsh git intel-ucode(amd-ucode)
systemctl enable NetworkManager sshd
```

## 代理(clash)
```shell
sudo su
mkdir /opt/clash && cd /opt/clash
wget https://dl3.ssrss.club/clash-linux-amd64-v1.8.0.gz  
wget -O /opt/clash/config.yaml "https://new.ssrss.de/sub?target=clash&new_name=true&url=https%3A%2F%2Fssrss.de%2Fs%2FPZDtd&udp=true&tfo=true&config=https%3A//ssrss.de/ssrss.ini"
wget https://dl3.ssrss.club/Country.mmdb
gunzip -c *.gz > clash && chmod +x clash
```
```shell
cat > /usr/lib/systemd/system/clash.service <<'EOF'
[Unit]
Description=clash
[Service]
TimeoutStartSec=0
ExecStart=/opt/clash/clash -d /opt/clash
[Install]
WantedBy=multi-user.target
EOF
```
```shell
systemctl enable clash
systemctl start clash
export ALL_PROXY=socks5://127.0.0.1:7890
```
## 配置文件
```shell
cd
touch ~/.zshrc
touch ~/.zprofile
chsh -s /usr/bin/zsh
zsh
git clone https://www.github.com/Laughing-q/zsh.git ~/.config/zsh
git clone https://www.github.com/Laughing-q/dotfiles-Q.git
cd dotfiles-Q
cp .zprofile ~/
./install.sh
sudo make install
```

## dwm
```shell
sudo pacman -S xorg xorg-server xorg-xinit xorg-apps
cd
git clone https://www.github.com/Laughing-q/dwm.git
cd dwm && sudo make install && cd ..
git clone https://www.github.com/Laughing-q/dwmblocks.git
cd dwmblocks && sudo make install && cd ..
git clone https://www.github.com/Laughing-q/dmenu.git
cd dmenu && sudo make install && cd ..
git clone https://www.github.com/Laughing-q/st.git
cd st && sudo make install && cd ..
git clone https://www.github.com/Laughing-q/dmscripts.git
cd dmscripts && sudo make install && mkdir -p ~/.config/dmscripts && cp ./config/config ~/.config/dmscripts
cd
```
## yay
```shell
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

## 软件
- tools
```shell
yay -S zathura zarhura zathura-pdf-mupdf unclutter sxiv mpv maim xwallpaper youtube-dl xsel mpd mpc ncmpcpp picom pamixer dunst light-git task-spooler ranger lf nodejs npm lazygit htop fzf fd
sudo npm install fanyi -g
mkdir -p ~/.config/picom
cp /etc/xdg/picom.conf ~/.config/picom/
git clone https://github.com/wting/autojump.git
cd autojump && ./install.
cd
```
- anaconda
```shell
yay -S anaconda
# 防止anaconda安装的curl干扰出问题
rm /opt/anaconda/bin/curl
```

## 字体
```shell
git clone https://github.com/ryanoasis/nerd-fonts.git
cd nerd-fonts && ./install.sh
# emoji font
yay -S ttf-joypixels noto-fonts-emoji
# 防止emoji出问题的补丁
yay -S libxft-bgra
# 或许需要额外安装中文字体
```

## 驱动
- inter显卡
```shell
sudo pacman -S mesa lib32-mesa vulkan-intel lib32-vulkan-intel
```
- nvidia显卡
```shell
sudo pacman -S nvidia nvidia-utils nvidia-settings
# 只有使用独显运行下面这一句生成配置文件，如果仅nvidia-smi则不需要
nvidia-sconfig
```

## nvidia
```shell
sudo pacman -S nvidia nvidia-utils nvidia-settings
sudo pacman -S cuda cudnn
```

## 壁纸
```shell
git clone https://github.com/Laughing-q/wallpapers.git
```

## nvim
```shell
yay -S nvim
pip install pynvim
git clone https://github.com/Laughing-q/nvim.git ~/.config/nvim
cd ~/.config/nvim
./install.sh
```

## Finally
```shell
reboot
```