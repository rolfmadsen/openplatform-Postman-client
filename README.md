# openplatform-Postman-client

[Den åbne platform (Openplatform](https://openplatform.dbc.dk/), udstiller et API bestående af en række REST services, som er beskrevet i "Open platform" dokumentationen under https://openplatform.dbc.dk/v1/.

API'et kan tilgås fra https://openplatform.dbc.dk/, men det forudsætter generering af en access_token fra https://auth.dbc.dk/ via en kommando-prompt som beskrevet under https://github.com/dbcdk/smaug/, hvilket gør indlæringskurven forholdsvis høj for ikke teknisk personale.

Hensigten med dette Github repository er at:
* Give biblioteksmedarbejdere mulighed for at se de data via Openplatform API'et uden det forudsætter programmeringskompetencer.
* Dele en Postman collection bestående af et antal foruddefinerede forespørgsler til Openplatform.
* Beskrive hvordan man installerer postman.
* Beskrive hvordan man importerer FBS Postman collectionen.
* Beskrive hvordan man benytter environment variables til at autentificere Postman for at benytte Openplatform, foretage kald mv.

Målgruppen er webmastere der ønsker at se de data FBS udleverer til f. eks. DDB CMS.

Openplatform Postman collection giver mulighed for at hente følgende oplysninger fra Openplatform:

* Order (Endnu ikke tilføjet)
* CMS (Endnu ikke tilføjet)
* Search (Delvist tilføjet)
* Libraries (Endnu ikke tilføjet)
* Recommend (Endnu ikke tilføjet)
* Status (Endnu ikke tilføjet)
* Suggest (Endnu ikke tilføjet)

## Installér Postman klienten

Postman er gratis værktøj med en grafisk brugergrænseflade, der kan installeres på Windows, Mac og Linux computere, og den egner sig derfor godt til brugere, som undertegnede, der ikke færdes hjemmevant i en kommandoprompt og ikke kan programmere op imod et API.

Postman kan downloades fra https://www.getpostman.com/ og installeres som ethvert andet program.

## Importér FBS.postman_collection

"Openplatform postman collection" er en samling af REST service kald som er defineret under https://openplatform.dbc.dk/.

Samlingen består primært af et POST kald der autentificerer "Postman klienten" og potentielt også Låneren og en række POST/GET kald der henter forskellige typer af information ud af systemet. 

1. Tryk på linket [Openplatform Postman collection](https://raw.githubusercontent.com/rolfmadsen/openplatform-Postman-client/master/Openplatform.postman_collection.json).
2. Tryk CTRL+S for at downloade filen, og gem den på dit skrivebord.
3. Åben Postman
4. Tryk på "Import" knappen i den øverste grå menu linje og tryk på "Choose Files" knappen i det Import vindue der dukker op midt på skærmen.
5. Dobbelt-klik på "FBS postman collection" filen på dit skrivebord for at importere den.

## Importér Environment variables

Postman giver mulighed for at benytte Environment variables, der er variabler gør det lettere at tilpasse kaldene til Openplatform.

Variabler fremgår som {{variabel}} i Postman brugergrænsefladen.

Ikke alle variablerne kan deles da nogle af dem indeholder brugernavne og passwords mv. til Openplatform systemet.
Derfor kan jeg kun dele et environment hvor de følsomme oplysninger er udskiftet med * og vise hvilke variabler der er indsat i kaldene og hvordan de oprettes.

1. Tryk på linket [Openplatform Postman environment](https://raw.githubusercontent.com/rolfmadsen/openplatform-Postman-client/master/Openplatform.postman_environment.json)
2. Tryk CTRL+S for at downloade filen, og gem filen på dit skrivebord
3. Åben Postman
4. Tryk på tandhjulet i øverste højre hjørne
5. Tryk på "Manage environments"
6. Tryk på "Import" knap nederst i "Manage environment" vinduet.
7. Tryk på Vælg filer knappen "Manage environment vindue der dukker op midt på skærmen.
8. Dobbelt-klik på Open platform environment filen du har downloadet til dit skrivebord for at importere den.
10. Udskift de dele af teksten der er markeret med \*'ner med følgende oplysninger 
  * "client_id" med de client ID du kan få udleveret ved henvendelse til DBC
  * "client_secret" med den client secret du kan få udleveret ved henvendelse til DBC
  * "user_id:" OBS. Er udfyldt med "@" som er default for en anonym bruger, men et CPR-nummer eller Biblioteksnummer kan indsættes hvis der skal laves opslag i Openplatform der forudsætter en autentificeret (indlogget) bruger.
  * "user_password" OBS. Er udfyldt med "@" som er default for en anonym bruger, men et CPR-nummer eller Biblioteksnummer kan indsættes hvis der skal laves opslag i Openplatform der forudsætter en autentificeret (indlogget) bruger.

### access_token

"access_token" er variabler der leveres af Openplatform og udfyldes når kaldene laves.

```
var data = JSON.parse(responseBody);
postman.setEnvironmentVariable("access_token", data.access_token);
```

### Sådan laver du kald til FBS

For at lave et kald til Openplatform skal Postman klienten og låneren først autentificeres. 

Det gør man ved at vælge:
1. "Client authenticate" og trykke på den blå "Send" knap.

Herefter kan man vælge de kald man ønsker at udføre og trykke på den blå "Send" knap.
