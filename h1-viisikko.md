# h1 Viisikko

## Laitteisto

Host: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikoneena: Debian GNU/Linux 13.1.0 ”Trixie”

Ram: 4GB

Levytila: 60GB

CPU: 1

## x) Lue ja tiivistä

Karvinen 2025: https://terokarvinen.com/install-salt-on-debian-13-trixie/

-Asenna wget
-Lataa ja kopioi Salt-projektin julkinen avain ja lähdelista tiedostot
-Testaa Salt:in asennus

Karvinen 2023: https://terokarvinen.com/2021/salt-run-command-locally/

-Linuxissa kaikki asetukset ovat vain tekstitiedostoja

Karvinen 2018: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

-Master-koneella pitää olla julkinen palvelin ja osoite
-Slave-koneelle on lisättävä master-koneen IP-osoite
-Master-koneella pitää hyväksyä slave-avain

Karvinen 2006: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

-Raportin on oltavat toistettava
-Helppolukuinen
-Lähdeviittaukset on oltava

## a) Asenna Debian 13-Trixie virtuaalikoneeseen

Ei ollut ongelmia

## b) Asenna Salt(salt-minion)

Saltin asennuksen aloittamiseksi tarvittiin wget-ohjelma tiedostojen lataamiseen, joka asennettiin seuraavasti:

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

Avaimen aitous ja sormenjäki tarkistettiin:

<img width="1280" height="800" alt="3 gpg show key" src="https://github.com/user-attachments/assets/d248fc06-4d0b-4067-9035-69cbb6a5a386" />

Seuraavaksi annoin luottamuksen Salt-projektille ja lisättiin avain ja lähdetiedosto järjestelmään:
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

Asensin Salt-minionin:
$ sudo apt-get update
$ sudo apt-get -y install salt-minion

Tarkistin asennetun version:
$ sudo salt-call --version
<img width="1280" height="800" alt="7 saltcall versio" src="https://github.com/user-attachments/assets/014f8a67-81b5-44ae-9ee3-c8f7eecf5dfd" />

## c) Viisi tärkeintä Salt tilafunkitoa

1. pkg

Komento: $ sudo salt-call --local -l info state.single pkg.installed tree
varmistaa, että tree paketti on asennettuna.
Result: True, onnistui


<img width="1280" height="800" alt="8 pkg installed tree" src="https://github.com/user-attachments/assets/36a80574-61ca-40bc-ad6e-ccd90ac10346" />

2. file

Komento: $ sudo salt-call --local -l info state.single file.managed /tmp/moitero contents="foo"
luo ja päivittää tiedoston sisällöksi tekstin "foo"
   
<img width="1280" height="800" alt="11 file managed foo" src="https://github.com/user-attachments/assets/9372fdaf-0e44-4fab-8ac6-f4cfbf8e75f1" />


3. service

Komento: $ sudo salt-call --local -l info state.single service.running apache2 enable=True
varmistaa, että Apache2 on käynnissä ja käynnistyy automaattisesti bootissa
Changed=1, ei ollut käynnissä ennen komennon ajoa

<img width="1280" height="800" alt="13 apahce 2 true" src="https://github.com/user-attachments/assets/3e780eb3-5733-4d36-a8b7-5ff017dad3bd" />


4. user

Komento: $ sudo salt-call --local -l info state.single user.present terote08
luo käyttäjän terote08
Ei tullut virheitä, joten käyttäjää ei ollut vielä luotuna

<img width="1280" height="800" alt="15 user present" src="https://github.com/user-attachments/assets/4d20090c-71d1-41ad-8a42-8aebf2a895df" />

5. cmd

Komento: $ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"
suorittaa komennon jos tiedostoa /tmp/foo ei ole vielä olemassa
Creates="/tmp/foo" tekee tästä idempotentin


<img width="1280" height="800" alt="17 running command" src="https://github.com/user-attachments/assets/9d4a1eca-0619-439e-8ba1-313429151be4" />

## d) Idempotentti

Komento: $ sudo salt-call --local -l info state.single file.managed /tmp/hellotero

Ensimmäisellä kerralla komento luo /tmp/hellotero ,mutta toisella ajo kerralla tulee komentti "file exists no changes made"
Tämä on idempotenssi, koska toistettu ajaminen ei muuttanut lopputulosta
<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_23_10_2025_10_00_40" src="https://github.com/user-attachments/assets/5fb81adf-acc7-4cbe-b614-12dab11aab24" />
<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_23_10_2025_10_01_08" src="https://github.com/user-attachments/assets/882ddd6e-deb3-4f90-b343-6942d37e0a6e" />

## Lähteet

Karvinen 2025: https://terokarvinen.com/install-salt-on-debian-13-trixie/

Karvinen 2023: https://terokarvinen.com/2021/salt-run-command-locally/

Karvinen 2018: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Karvinen 2006: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/
