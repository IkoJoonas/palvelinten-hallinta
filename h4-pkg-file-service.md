## Laitteisto

Host: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

2x Virtuaalikonetta: Debian GNU/Linux 13.1.0 ”Trixie”

Ram: 4GB

Levytila: 60GB

CPU: 1 

## x)

-Package-file-service ovat yleisimmät tilafunktiot.

-Asenna, muuta konfiguraatio tiedostoa, uudelleen käynnistä demoni.

## a)

Aloitin luomalla uuden hakemiston master-koneelle ja sen sisälle sls-tiedoston

Lisäsin seuraavat tiedot:

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_13_11_2025_19_25_24" src="https://github.com/user-attachments/assets/378b0b45-671c-41e3-9cde-5d882845d2b1" />

Loin master-koneelle tiedoston, jonka olin merkinnyt "- source" kohtaan.

Lisäsin tiedostoon oletustiedoston tekstit, mutta jätin suurimman osan kommenteista pois.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_13_11_2025_19_23_51" src="https://github.com/user-attachments/assets/b0caeaab-cf95-4433-a26b-3ff00e7e1c3d" />

Suoritin moduulin

<img width="1280" height="800" alt="h4alkaatasta" src="https://github.com/user-attachments/assets/d0e35c81-b5fc-43c4-9f6f-d8a53afa3f36" />

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_13_11_2025_19_23_43" src="https://github.com/user-attachments/assets/bf592ebc-e364-4c52-a6bf-2a67181b8894" />

Tämän jälkeen lisäsin vielä service-tilafunktion.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_17_44" src="https://github.com/user-attachments/assets/9e95b495-54f7-45d7-9a3e-368f8737af90" />

Suoritin moduulin.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_18_26" src="https://github.com/user-attachments/assets/340161d0-ddd5-4853-b887-fde1312d371e" />

Tarkistin, että minionilla oli portti 1234 kiinni.

<img width="1270" height="763" alt="Näyttökuva 2025-11-15 kello 13 02 55" src="https://github.com/user-attachments/assets/932b10ff-4bb0-41e6-b863-49914cb0afb8" />

Muokkasin master-koneen konfiguraatiotiedostoa, jotta saan demonin käynnistymään uudelleen. Otin portin 1234 pois ja suoritin moduulin.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_23_55" src="https://github.com/user-attachments/assets/c521b12a-77ce-474a-9ef7-cfe653e61891" />

Tämän jälkeen lisäsin portin takaisin ja suoritin moduulin uudestaan.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_24_54" src="https://github.com/user-attachments/assets/46394324-7dde-4a4c-93c4-d7f9120bb9bb" />

Muutoksia oli kaksi, mutta halusin vielä varmistaa minion-koneella, että demoni käynnistyi uudelleen.

<img width="1280" height="800" alt="VirtualBox_DebMin_15_11_2025_12_25_15" src="https://github.com/user-attachments/assets/724354e3-b8a6-4c3f-87d2-228d99cde786" />

Portti oli nyt auki.

Otin ssh-yhteyden masterilta minioniin.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_30_00" src="https://github.com/user-attachments/assets/c5e18e8a-dce2-47fd-9602-d0bde37d27b4" />

Nytkun olin saanut kaiken toimimaan käsin konfiguroimalla, poistin ssh-serverin kokonaan minion-koneelta.

<img width="1280" height="800" alt="VirtualBox_DebMin_15_11_2025_12_34_29" src="https://github.com/user-attachments/assets/033a9cba-31c2-4555-8486-839685ef801d" />

Poistamisen jälkeen ajoin moduulin master-koneella.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_36_27" src="https://github.com/user-attachments/assets/4ef20a03-8fa6-4180-9df2-2fc80145d38f" />

Kaikki näytti menneen onnistuneesti, joten kokeilin ottaa uudelleen ssh-yhteyden minioniin.

<img width="1280" height="800" alt="VirtualBox_DebianJoonasI_15_11_2025_12_42_30" src="https://github.com/user-attachments/assets/6b763f52-87c3-4cb3-a17f-f7fcc4e2681e" />

Yhteys onnistui.

## Lähteet

Karvinen 2018: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh

Aapo Tavio H4 Pkg-file-service: https://aapotavio.com/configuration-management-systems/h4-pkg-file-service/



