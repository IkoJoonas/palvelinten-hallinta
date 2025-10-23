# h1 Viisikko

x)

a)

## b) Asenna Salt(salt-minion)

Saltin asennuksen saloittamiseksi tarvittiin wget-ohjelma tiedostojen lataamiseen, joka asennettiin seuraavasti:
$ sudo apt-get update
$ sudo apt-get install wget

Asennnuksen jälkeen luotiin uusi hakemista saltrepo/ ja siirryttiin sinne:
$ mkdir saltrepo/
$ cd saltrepo/

Ladattiin tarvittavat tiedostot:
$ wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public

$ wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources

Public tiedosto sisältää Salt Projectin julkisen PGP-avaimen, joka on ASCII-muodossa oleva salattu avain, jota käytetään pakettien aitouden varmistamiseen:
<img width="1280" height="800" alt="1 Less public quits less" src="https://github.com/user-attachments/assets/919ca9c0-1822-4ec9-b3e7-33ab5bbe8beb" />

Salt.sources tiedostossa määritetään mistä osoitteesta paketit ladataan ja mihin PGP-avain tallentuu
<img width="1280" height="800" alt="2 less salt sources" src="https://github.com/user-attachments/assets/98964146-38e7-4e81-b173-cde5ef6dbf59" />

Avaimen aitouden ja sormenjäljen voidaan tarkastaa:

<img width="1280" height="800" alt="3 gpg show key" src="https://github.com/user-attachments/assets/d248fc06-4d0b-4067-9035-69cbb6a5a386" />

Seuraavaksi annettiin luottamus Salt-projektille ja lisättiin avain ja lähdetiedosto järjestelmään:
$ sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp
$ sudo cp salt.sources /etc/apt/sources.list.d/

<img width="1280" height="800" alt="4 trust and install repository" src="https://github.com/user-attachments/assets/a481b34a-4c38-49e6-a173-d48cf6df9402" />

Kun olin tarkistanut, että tiedostot varmasti löytyvät, asensin Salt-ohjelmistot:
$ sudo apt-get update
$ sudo apt-get install salt-minion salt-master

Komennolla: $ salt --version varmistin, että asennus on onnistunut
<img width="1280" height="800" alt="5 test salt" src="https://github.com/user-attachments/assets/15307bae-55b3-455c-aceb-a521710c8633" />

Kokeilin vielä salt-komennolla toimivuuden:
$ sudo salt-call --local state.single file.managed /tmp/hellotero
$ ls /tmp/hellotero 
<img width="1280" height="800" alt="6 is it really there" src="https://github.com/user-attachments/assets/478e6057-a6ba-4313-9334-cfef8b75d4cf" />
