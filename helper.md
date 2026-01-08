### Check the batter status : 
 - upower -e  -> get all the information about power details
 - upower -i <battery device> -> get the information about the battery


 ❯ upower -i /org/freedesktop/UPower/devices/battery_BAT1
  native-path:          BAT1
  vendor:               SMP
  model:                AP18E7M
  serial:               29497
  power supply:         yes
  updated:              Thu 04 Dec 2025 09:52:33 AM IST (22 seconds ago)
  has history:          yes
  has statistics:       yes
  battery
    present:             yes
    rechargeable:        yes
    state:               fully-charged
    warning-level:       none
    energy:              36.575 Wh
    energy-empty:        0 Wh
    energy-full:         36.575 Wh
    energy-full-design:  58.751 Wh
    voltage-min-design:  15.4 V
    capacity-level:      Full
    energy-rate:         0 W
    voltage:             16.388 V
    charge-cycles:       N/A
    percentage:          100%
    capacity:            62.2543%
    technology:          lithium-ion
    icon-name:          'battery-full-charged-symbolic'



###  Setting the hyprland to run on GPU
 lspci -d ::03xx -> to get the GPUs and the PCIs
       00:02.0 VGA compatible controller: Intel Corporation CometLake-H GT2 [UHD Graphics] (rev 05)
       01:00.0 VGA compatible controller: NVIDIA Corporation GA106M [GeForce RTX 3060 Mobile / Max-Q] (rev a1)
       
 ls -l /dev/dri/by-path -> this will get the path for the graphic cards availabe
      lrwxrwxrwx     - root 18 Dec 19:39   pci-0000:00:02.0-card -> ../card2
      lrwxrwxrwx     - root 18 Dec 19:39   pci-0000:00:02.0-render -> ../renderD129
      lrwxrwxrwx     - root 18 Dec 19:39   pci-0000:01:00.0-card -> ../card1
      lrwxrwxrwx     - root 18 Dec 19:39   pci-0000:01:00.0-render -> ../renderD128


to configure which GPU to use, we need to setup AQ_DRM_DEVICES key (which will be avaiable in /home/srujan/.config/uwsm/env)
- export AQ_DRM_DEVICES="/dev/dri/card1:/dev/dri/card2"  -> This will allow the hyprland to run on card1 if present (Nvidia) else card2 (dedicted)

reference : https://wiki.hypr.land/Configuring/Multi-GPU/



### fix the corrupt drive 
sudo ntfsfix -d  /dev/sda1
