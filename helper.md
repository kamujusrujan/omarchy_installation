Check the batter status : 
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
