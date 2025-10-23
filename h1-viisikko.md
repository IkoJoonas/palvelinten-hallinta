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
