Installing Yay package manager : 
    sudo pacman -S --needed base-devel git
    git clone https://aur.archlinux.org/yay-git.git
    cd yay-git
    makepkg -si
    cd .. && rm -rf yay-git

Installing chrome 
    yay -S google-chrome
