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
