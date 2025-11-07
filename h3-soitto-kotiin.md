## Laitteisto

Host: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

2x Virtuaalikonetta: Debian GNU/Linux 13.1.0 ”Trixie”

Ram: 4GB

Levytila: 60GB

CPU: 1 

## x) Lue ja tiivistä

Karvinen 2021: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

-Vagrantilla pystyy luomaan virtuaalikoneet automaattisesti

-Vagrantissa ei ole graafistakäyttöliittymään

Karvinen 2018: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

-Master-koneella pitää olla julkinen ip osoite

-Minion-koneen pitää tietää master-koneen osoite

-Masterin pitää hyväksyä minionin avain

Karvinen 2023: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

-Infraa koodina voidaan määrittää suoritettavat tilafunktiot

-Top file mitä tiloja suoritetaan millekin minionille

## Tausta

Tehtävä oli luoda Salti master-minion arkkitehtuuri Vagrantilla, joka luo kahden Linux virtuaalikoneen verkon. En löytänyt Hashicorpin sivuilta Debian 13 Trixie:tä joka olisi rakennettu toimimaan arm64 arkkitehtuuriin. Päätin kokeilla saanko toteutettua tehtävän ilman Vagrantia, luomalla virtuaalikoneet manuaalisesti.

## a)

<img width="576" height="378" alt="Näyttökuva 2025-10-28 kello 8 30 58" src="https://github.com/user-attachments/assets/79f201a9-74c3-464f-8b00-b7a2eef0003a" />

## b) 

Loin uuden virtuaalikoneen:

<img width="529" height="623" alt="Näyttökuva 2025-11-07 kello 14 16 18" src="https://github.com/user-attachments/assets/5a30cf73-79d5-48e6-a09a-7dd569644277" />

## c)

Tarkistin koneiden osoitteet:

Master

<img width="1280" height="800" alt="oikea h3" src="https://github.com/user-attachments/assets/638fae9e-5d8f-4ef7-ac2d-e910136161c0" />

Minion

<img width="1280" height="800" alt="VirtualBox_DebMin_06_11_2025_19_45_29" src="https://github.com/user-attachments/assets/285d5241-37d1-4c1b-8dd9-2964d0aa9b6c" />

Pingasin koneet toisiinsa:

Master pingaa minioniin

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_06_11_2025_19_46_11" src="https://github.com/user-attachments/assets/eb974ad0-4aa5-44bc-a4a9-266bd7de6214" />

Minion pingaa masteriin

<img width="1280" height="800" alt="VirtualBox_DebMin_06_11_2025_19_46_43" src="https://github.com/user-attachments/assets/ecdf0577-83e0-4c3e-aa96-c3b03be87d3f" />

## d)

Olin asentanut Saltin master-koneelle tehtävässä h1 viisikko.

Asensin minion-koneelle Saltin käyttäen komentoa:

sudo apt get -y install salt-minion

Seuraavaksi muokkasin /etc/salt/minion -tiedostoa ja lisäsin sinne masterin osoitteen ja minion id:n.

Komento: sudoedit /etc/salt/minion

<img width="1280" height="800" alt="VirtualBox_DebMin_06_11_2025_19_44_25" src="https://github.com/user-attachments/assets/82f19e60-5efa-4323-ae61-ae4d52c59875" />

Tämän jälkeen käynnistin minionin uudestaan komennolla:

sudo systemctl restart salt-minion

Kävin hyväksymässä master-koneella minionin avaimen.

sudo salt-key -A

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_06_11_2025_19_44_41" src="https://github.com/user-attachments/assets/07f47d00-bf82-4733-9afd-fad530381382" />

Varmistin, että master pystyy komentamaan minion-konetta.

Komennot:

sudo salt '*' cmd.run 'whoami'

sudo salt '*' cmd.run 'hostname -I'

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_06_11_2025_19_45_11" src="https://github.com/user-attachments/assets/e5b12d37-3e62-48cb-b5bc-d1040ecf1b4b" />

## e)

Kokeilin pkg ja file tiloja.

Pkg:

sudo salt '*' pkg.install httpie

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_06_11_2025_19_48_45" src="https://github.com/user-attachments/assets/94792367-0aab-473b-bf57-f0baf6814c83" />

File:

Ensimmäiseksi loin tekstitiedoston:

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_07_11_2025_14_56_47" src="https://github.com/user-attachments/assets/81ba286f-690b-4980-a7b9-32fb979628b9" />

Tämän jälkeen loin .sls tiedoston:

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_07_11_2025_14_54_36" src="https://github.com/user-attachments/assets/77a1b537-8dbe-4d13-afa9-d2d936e90745" />

Suoritin masterilla komennolla:

sudo salt '*' state.apply kokeilu

<img width="1280" height="800" alt="master minion file" src="https://github.com/user-attachments/assets/6ed90da7-8904-4016-8ea8-54bb1075cba3" />

Halusin vielä varmistua idempotentista, joten suoritin komennon uudestaan:

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_07_11_2025_14_57_36" src="https://github.com/user-attachments/assets/fb5f222b-746b-4856-beb9-ebc8e625063a" />

Tarkistin, että tiedosto on päivittynyt komennolla:

sudo salt '*' cmd.run 'cat /etc/kokeilu'

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_07_11_2025_14_57_52" src="https://github.com/user-attachments/assets/89704815-ac45-4276-a353-a626e640b435" />

Halusin olla täysin varma, että olin onnistunut tässä, niin kävin vielä tarkistamassa tiedoston minion-koneelta:

<img width="1280" height="800" alt="VirtualBox_DebMin_07_11_2025_14_59_56" src="https://github.com/user-attachments/assets/d0e7c639-8ff7-4324-bc4f-750f27dcb918" />
