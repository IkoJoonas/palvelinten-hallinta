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

