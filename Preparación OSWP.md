# Preparación para el OSWP (by s4vitar)

![OSWP Image](https://funkyimg.com/i/2VTJW.jpg)
#### Offensive Security Wireless Attacks (WiFu) course and Offensive Security Wireless Professional (OSWP) Cheat Sheet

## Índice y Estructura Principal
- [Antecedentes - Experiencia Personal](#Antecedentes)
- [Estructura de los apuntes](#estructura-de-los-apuntes)
     * [Redes WPA](#redes-wpa)
       * [Conceptos básicos](#conceptos-básicos)
       * [Modo monitor](#modo-monitor)
       * [Configuración de la tarjeta de red + tips](#configuración-de-la-tarjeta-de-red-+-tips)
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

# Redes WPA
Testing


