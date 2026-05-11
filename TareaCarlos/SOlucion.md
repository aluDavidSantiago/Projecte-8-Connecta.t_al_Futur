
#  **GUIA PRÀCTICA: EXPLORACIÓ DE XARXA AMB KALI LINUX**

***

## **1. Introducció**

En aquesta activitat s’ha realitzat una exploració de la xarxa local utilitzant Kali Linux i diferents eines de reconeixement com **Netdiscover** i **Nmap**.

L’objectiu ha estat:

*   Detectar dispositius connectats a la xarxa
*   Analitzar les diferències entre escaneig actiu i passiu
*   Identificar serveis i comportament dels hosts
*   Comprendre limitacions reals en entorns de xarxa

***

## **2. Configuració inicial**

Abans de començar, s’ha configurat la màquina virtual Kali en **mode adaptador pont (bridge)**, per tal de connectar-la a la mateixa xarxa que altres dispositius.

### **Comanda utilitzada per comprovar la IP:**

```
ip a
```

**Resultat:**

*   S’ha obtingut una IP dins de la xarxa (`192.168.2.X`)

📷 *(Captura: configuració IP de Kali)*

***

## **3. Exploració amb Netdiscover**

***

### **3.1 Mode actiu**

Comanda utilitzada:

```
sudo netdiscover -r 192.168.2.0/24
```

**Resultats obtinguts:**

*   S’han detectat diversos dispositius actius (aprox. 14 hosts)
*   S’han identificat adreces IP i MAC
*   S’han reconegut fabricants dels dispositius

📷 *(Captura: resultat Netdiscover mode actiu)*

**Conclusió:**

El mode actiu permet escanejar tota la xarxa enviant peticions ARP, fet que possibilita detectar un gran nombre de dispositius, encara que aquests no estiguin generant trànsit en aquell moment.

***

### **3.2 Mode passiu**

Comanda utilitzada:

```
sudo netdiscover -i eth0 -p
```

**Resultats obtinguts:**

*   S’han detectat menys dispositius (aprox. 10 hosts)

📷 *(Captura: resultat Netdiscover mode passiu)*

**Conclusió:**

El mode passiu no escaneja la xarxa, sinó que captura el trànsit existent. Això fa que només detecti dispositius que estan comunicant-se activament.

***

### **3.3 Comparativa mode actiu vs passiu**

| Mode   | Característiques                           |
| ------ | ------------------------------------------ |
| Actiu  | Escaneja tota la xarxa, detecta més hosts  |
| Passiu | Només escolta trànsit, detecta menys hosts |

**Conclusió general:**

El mode actiu és més complet, mentre que el mode passiu és més discret però menys efectiu en la detecció de dispositius.

***

## **4. Exploració amb Nmap**

***

### **4.1 Descobriment de hosts**

Comanda utilitzada:

```
nmap -sn 192.168.2.0/24
```

**Resultats obtinguts:**

*   S’han detectat 3–4 hosts actius

📷 *(Captura: resultat Nmap -sn)*

**Conclusió:**

Nmap detecta menys dispositius que Netdiscover perquè utilitza mètodes diferents (com ICMP), mentre que Netdiscover utilitza ARP a nivell local.

***

### **4.2 Escaneig de ports**

Comanda utilitzada:

```
nmap 192.168.2.X
```

**Resultats obtinguts:**

*   No s’han detectat ports oberts
*   Els ports analitzats es troben tancats

📷 *(Captura: escaneig de ports)*

**Conclusió:**

El dispositiu analitzat no presenta serveis accessibles o disposa de mesures de seguretat que bloquegen l’accés als ports.

***

### **4.3 Detecció de sistema operatiu**

Comanda utilitzada:

```
sudo nmap -O 192.168.2.X
```

**Resultats obtinguts:**

*   El sistema operatiu no s’ha pogut determinar amb exactitud

📷 *(Captura: detecció SO)*

**Conclusió:**

La manca d’informació pot deure’s a l’absència de serveis oberts o a configuracions de seguretat que dificulten la identificació.

***

### **4.4 Cas especial: hosts no detectats**

Durant l’activitat, s’ha observat que alguns dispositius detectats amb Netdiscover no han estat identificats posteriorment amb Nmap.

Per exemple:

*   Un host detectat inicialment (`192.168.2.14`)
*   No responia en escaneigs posteriors

**Conclusió:**

Aquest comportament és habitual en xarxes reals i pot ser degut a:

*   Dispositius apagats
*   Desconnexió de la xarxa
*   Bloqueig de peticions ICMP

***

## **5. Comparativa Netdiscover vs Nmap**

| Eina        | Característiques                               |
| ----------- | ---------------------------------------------- |
| Netdiscover | Utilitza ARP, detecta més dispositius          |
| Nmap        | Utilitza ICMP i altres mètodes, més restrictiu |

**Conclusió:**

Netdiscover és més efectiu per detectar dispositius en xarxes locals, mentre que Nmap és més potent per analitzar serveis i seguretat.

***

## **6. Conclusions finals**

A través d’aquesta activitat s’ha pogut:

*   Explorar una xarxa local real
*   Detectar dispositius actius i inactius
*   Analitzar diferències entre escaneig actiu i passiu
*   Identificar limitacions reals de les eines de xarxa
*   Comprendre el comportament dinàmic dels dispositius

En conjunt, l’activitat permet adquirir una visió pràctica i realista de l’anàlisi de xarxes, destacant la importància d’utilitzar diferents eines i interpretar correctament els resultats.

