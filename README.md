# KonfigurasiUML
config UML

SURABAYA (router)
MALANG (dns server)
TUBAN (dhcp server)
MOJOKERTO (proxy server)

- IP Kelas 
  
  ```
  10.151.36.203
  ```

- NID **TUNTAP**
  
  ```
  10.151.76.64
  ```
  
- NID **DMZ**

  ```
  10.151.77.128
  ```
  
- IP_**eth0_SURABAYA**_tiap_kelompok = NID_tuntap_tiap_kelompok + 2

  ```
  10.151.76.66
  ```

- **IP_tuntap**_tiap_kelompok = NID_tuntap_tiap_kelompok + 1

  ```
  10.151.76.65
  ```

- IP_**eth1_SURABAYA**_tiap_kelompok = NID_DMZ_tiap_kelompok + 1

  ```
  10.151.77.129
  ```

- **IP_MALANG**_tiap_kelompok = NID_DMZ_tiap_kelompok + 2

  ```
  10.151.77.130
  ```

- **IP_MOJOKERTO**_tiap_kelompok = NID_DMZ_tiap_kelompok + 3


  ```
  10.151.77.131
  ```

- **IP_TUBAN**_tiap_kelompok = NID_DMZ_tiap_kelompok + 4

  ```
  10.151.77.132
  ```

- **iptables.sh**

  ```
  iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16
  ```

- **/etc/apt/sources.list**

  ```
  deb http://boyo.its.ac.id/debian stretch main contrib non-free
  ```

- TOPOLOGI.SH **modul4**

```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &
uml_switch -unix switch7 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.65 eth1=daemon,,,switch5 eth2=daemon,,,switch6 mem=256M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch0 eth1=daemon,,,switch4 mem=96M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch5 eth1=daemon,,,switch1 eth2=daemon,,,switch4 mem=96M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch7 eth1=daemon,,,switch6 mem=96M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch3 eth1=daemon,,,switch2 eth2=daemon,,,switch7 mem=96M &

# Server switch 2
#xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=168M &
#xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
#xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien 1
xterm -T 100 Komputer -e linux ubd0=100 Komputer,jarkom umid=100 Komputer eth0=daemon,,,switch0 mem=64M &
xterm -T 50 Komputer -e linux ubd0=50 Komputer,jarkom umid=50 Komputer eth0=daemon,,,switch1 mem=64M &
xterm -T 10 Komputer -e linux ubd0=10 Komputer,jarkom umid=10 Komputer eth0=daemon,,,switch2 mem=64M &
xterm -T 20 Komputer -e linux ubd0=20 Komputer,jarkom umid=20 Komputer eth0=daemon,,,switch3 mem=64M &
```
