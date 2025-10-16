2 máquinas virtuales - kali y xubuntu
Incluir ambas en misma red NAT
https://github.com/krabelize/icmpdoor
from xubuntu:
- sudo apt update && sudo apt install git && sudo apt install python3-pip
- python3 icmpdoor.py -i enp0s3 -d ip_kali
al probar una máquina en red NAT y otra en adaptador puente: capturar pings de gateway