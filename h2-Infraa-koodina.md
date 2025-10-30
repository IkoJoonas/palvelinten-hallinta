# h2 Infraa koodina

## Laitteisto

Host: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikoneena: Debian GNU/Linux 13.1.0 ”Trixie”

Ram: 4GB

Levytila: 60GB

CPU: 1 

## x) Lue ja tiivistä

Karvinen 2014: https://terokarvinen.com/2024/hello-salt-infra-as-code/ 

-Komento: $ sudo salt-call --local state.apply, suorittaa paikallisesti.

Salt contributors: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml

-Sisennys tapahtuu kahdella välilyönnillä tai lisäämällä kaksi lisää edelliseen.

Salt contributors: https://docs.saltproject.io/en/latest/ref/states/top.html

-Saltissa koneryhmien hallintaan käytetään top file-tiedostoa

## a)

Salt-moduuleja varten loin niille hakemiston ja samalla lisäsin sinne moduulin "moi" komennolla:

$ sudo mkdir -p /srv/salt/moi/

Polun sisälle loin tiedoston init.sls komennolla:

$ sudoedit init.sls

Tämän sisälle kirjoitin seuraavan:

<img width="1280" height="800" alt="sudoedit" src="https://github.com/user-attachments/assets/0cd25747-a3d4-457f-998e-ed0147494fcf" />

Suoritin moduulin paikallisesti komennolla:

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

Top.sls pystyy suorittamaan komennolla:

$ sudo salt-call --local state.apply

<img width="1280" height="800" alt="b) kohta tehtävän lopussa" src="https://github.com/user-attachments/assets/667c1506-358c-4f7b-b13b-0b51f2ed8639" />

## c)

Loin kaikille omat moduulit:

<img width="1280" height="800" alt="viisikko tiedostossa" src="https://github.com/user-attachments/assets/31cfc42c-c47e-44c1-84f0-0f18b9a9bd31" />

Jokaiselle omat .sls tiedostot ja sisältö niihin:

Pkg:

<img width="1280" height="800" alt="moipkg sisältö" src="https://github.com/user-attachments/assets/892d6d74-4c23-44ee-9edc-07a2947e41c5" />

File:

<img width="1280" height="800" alt="file sisältö" src="https://github.com/user-attachments/assets/4c80ee29-763f-4469-9fcf-e05c0c7bbfc3" />

Service:

<img width="1280" height="800" alt="moiservice sisältö" src="https://github.com/user-attachments/assets/ba06f978-9ffe-4f88-aa76-987a5748a217" />

User:

<img width="1280" height="800" alt="moiuser sisältö" src="https://github.com/user-attachments/assets/019ea327-efa2-4c8b-86f2-f642282aaaa0" />

Cmd:

<img width="1280" height="800" alt="cmd sisältö" src="https://github.com/user-attachments/assets/9f4dbb5e-a5d8-47a5-aa31-d83a954e7348" />

Varmistin, että kaikki toimii odotetusti:

<img width="1280" height="800" alt="c) kohdan loppu" src="https://github.com/user-attachments/assets/fc96b14f-3d5d-4338-af0a-9a981e28b222" />

## d)

Loin uuden testi moduulin ja sen sisälle .sls tiedoston, joka käyttää tilafunktioita user ja service:

<img width="1280" height="800" alt="d) demo käyttäjän luonti lyonti" src="https://github.com/user-attachments/assets/c21c8cc4-986c-4f35-ae65-30e96912c4cd" />

Tarkistin, että sls-tiedosto on idempotentti:

<img width="1280" height="800" alt="d) idempotentti" src="https://github.com/user-attachments/assets/74a38ff9-d948-41e0-b445-175e10a8c7af" />

## Lähteet

Karvinen 2014: https://terokarvinen.com/2024/hello-salt-infra-as-code/

Salt contributors: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml, kohdat

Rules of YAML

YAML simple structure

Lists and dictionaries - YAML block structures

Salt contributors: https://docs.saltproject.io/en/latest/ref/states/top.html, kohdat

Introduction

A basic example

Copilot: kohtien c) ja d) sls-tiedostojen sisällön luontiin
