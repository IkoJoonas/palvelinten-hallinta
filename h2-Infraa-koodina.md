# h2 Infraa koodina

## Laitteisto

Host: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikoneena: Debian GNU/Linux 13.1.0 ”Trixie”

Ram: 4GB

Levytila: 60GB

CPU: 1 

## x)


## a)

Salt-moduuleja varten loin niille hakemiston ja samalla lisäsin sinne moduulin "moi" komennolla:

$ sudo mkdir -p /srv/salt/moi/

Polun sisälle loin tiedoston init.sls komennolla:

$ sudoedit init.sls

Tämän sisälle kirjoitin seuraavan:

<img width="1280" height="800" alt="sudoedit" src="https://github.com/user-attachments/assets/0cd25747-a3d4-457f-998e-ed0147494fcf" />

Ajoin moduulin paikallisesti komennolla:

$ sudo salt-call --local stato.apply moi

Ja tarkistin, että tiedosto luotiin onnistuneesti komennolla:

$ ls /tmp/moijoonas

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_28_10_2025_09_32_13" src="https://github.com/user-attachments/assets/ab520305-7235-4659-b83f-d73a071b2888" />

Tein vielä idempotentin varmennuksen, muutoksia ei ollut

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_29_10_2025_15_50_05" src="https://github.com/user-attachments/assets/bd79694f-c17d-4631-ae8b-c8c41befa5f0" />

## b)

Aloitin luomalla top-filen:

$ sudoedit /srv/salt/top.sls

Ja sen sisällöksi:

base:

  '*':
 
    - 

Tältä top.sls näytti kokonaisuudessaan tehtävän d) jälkeen:

<img width="1280" height="800" alt="b) kohta sisältö" src="https://github.com/user-attachments/assets/9c96746e-eac9-462f-be49-32d412cf95b5" />

