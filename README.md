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
