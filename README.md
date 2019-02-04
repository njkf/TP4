# B1 Réseau 2018 - TP4

## Mise en place du routage statique

### sur routeur1

`ip route show`  
10.1.0.0/24 dev enp0s8 proto kernel scope link src 10.1.0.254 metric 100 

10.2.0.0/24 dev enp0s9 proto kernel scope link src 10.2.0.254 metric 101

### sur client1 et serveur1

`sudo nano route-enp0s8`

Dans etc/sysconfig/network-scripts :  
10.2.0.0/24 via 10.1.0.254 dev enp0s8
 
## Spéologie réseau
 
### ARP
 
#### Manip 1
 
client1: 
`ip neigh show`
10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:46 REACHABLE 
 
On a qu'une seule ligne car on a vidé la table ARP et qu'aucun ping n'a été fait donc aucune adresse MAC a été ajouté.

serveur1: 
`ip neigh show`
10.2.0.1 dev enp0s8 lladdr 0a:00:27:00:00:4b REACHABLE
 
Comme pour le client, le server n'a pas fait de ping et donc n'a pas les autres adresses dans sa table ARP.

client1 apres le ping sur serveur1 : 
 
`ip neigh show`

10.1.0.254 dev enp0s8 lladdr 08:00:27:55:69:2b REACHABLE

10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:46 REACHABLE

serveur1 apres le ping sur client1:
 
`ip neigh show` 

10.2.0.254 dev enp0s8 lladdr 08:00:27:9c:42:37 STALE

10.2.0.1 dev enp0s8 lladdr 0a:00:27:00:00:4b DELAY

On peut voir que suite au ping le serveur enregistre l'adresse MAC pingé. 

#### Manip 2

routeur1: une seule ligne sur la table ARP car il n'a communoiqué avec aucune autre adresse MAC

routeur1 apres le ping de serveur1 sur client1:3 lignes, les adresses MAC de client1 et serveur1 ont été ajouté

#### Manip 3

#### Manip 4

### Wireshark


