# h1 Viisikko

x)

a)

b) Asenna Salt(salt-minion)
Saltin asennuksen saloittamiseksi tarvittiin wget-ohjelma tiedostojen lataamiseen, joka asennettiin seuraavasti:
$ sudo apt-get update

$ sudo apt-get install wget

Asennnuksen jälkeen luotiin uusi hakemista saltrepo/ ja siirryttiin sinne:
$ mkdir saltrepo/

$ cd saltrepo/

Ladattiin tarvittavat tiedostot:
$ wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public

$ wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources

Public tiedosto sisältää Salt Projectin julkisen PGP-avaimen, joka on salatussa muodossa, jota käytetään pakettien aitouden varmistamiseen:
<img width="1280" height="800" alt="1 Less public quits less" src="https://github.com/user-attachments/assets/919ca9c0-1822-4ec9-b3e7-33ab5bbe8beb" />
