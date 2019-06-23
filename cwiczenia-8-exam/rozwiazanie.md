Zadanie 1
---------

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
 
Rozwiązanie
-----------

PC0  
-------------------
|  interfejs   | adres  |
|:-------------| :------| 
| eth3 | usługodawca zapewnia komunikację z siecią internet  |
| eth8 | 172.22.128.1/23  |
| eth9 | 172.22.160.1/19  |

użyte komendy:
``ip addr add _ dev _ </br>
ip link set _ up </br>
echo 1 > /proc/sys/net/ipv4/ip_forward </br>
sysctl -w net.ipv4.ip_forward=1 (dla pewności właczyłem forwarding dwoma metodami, któraś z nich zadziałała) </br>
iptables -t nat -A POSTROUTING -s _ -o _ -j MASQUERADE (x2) ``

PC1  
----------------
|  interfejs   | adres  |
|:-------------| :------| 
|eth3|172.22.128.2/23|

użyte komendy: </br>
``ip addr add _ dev _ </br>
ip route add default via _ dev _``

PC2  
------------------
|  interfejs   | adres  |
|:-------------| :------| 
| eth3 | 172.22.160.2/19 |

użyte komendy: </br>
``ip addr add _ dev _ </br>
ip route add default via _ dev _ </br> </br>``

całość została przetestowana komendą ``ping google.pl`` wyegzekwowaną na PC1 i PC2
