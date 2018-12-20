# Realisatie

Er is uiteindelijk een werkend product opgeleverd. Er is een web interface, slack integratie, facebook integratie en een core gemaakt. Per project staat hieronder meer uitleg er over.

## Code

Alle code is terug te vinden in het [code](./code/) mapje. Hier zie je een gradle project. Om het te builden kan er gebruik gemaakt worden van de gradle wrapper. Het commando hieronder is om het te builden. De wars staan dan in `<sub-project>/build/libs/` map.

```bash
murf@Marvins-MacBook-Pro: [~/Projects/bbb (master)] $ ./gradlew bootWar
```

## Core

> Technieken: Kotlin, Spring, Web3, Blockchain, Solidity

De core heeft geen UI. Dit is de backbone service van alles, vandaar de naam core. De core is de enige die in contact staat met de block en het smart contract. Deze service heeft ook de wallet geconfigureerd. De core heeft een eigen database. Deze database heeft accounts die gekoppeld zijn (bijvoorbeeld een facebook account gekoppeld aan een slack account) en de geregistreerde clients.

## Web api + interface

> API: Kotlin, Spring, Azure Active Directory\
> UI: Typescript, React, RxJS, Redux

<!-- Screenshot web ui -->

De web interface kan de gebruiker op inloggen. Via deze interface is er een lijst van bonussen te zien. Ook kan hier de gebruiker een bonus aan een andere gebruiker geven. Hier kan je ook je eigen punten uitgeven aan beloningen.

## Slack integratie

> Technieken: Kotlin, Spring, Co-Routines

<!-- Screenshot slack ui -->

De vraag voor Slack integratie is ook waargemaakt. Doormiddel van een Slash Commando¹ kan er een bonus gegeven worden. Als de bonus verwerkt is zal de gebruiker een bericht krijgen dat het succesvol is afgewerkt.

Ook kan de gebruiker een lijst van de bonussen opvragen. Hier kan met een _next_ en _previous_ knop doorheen gebladerd worden.

¹ [Slash Commands | Slack](https://api.slack.com/slash-commands)

## Facebook integratie - Proof of concept

> Technieken: Kotlin, Spring, Co-Routines

<!-- Screenshot fb ui -->

Om aan te tonen dat de architectuur uitbreidbaar is is er een proof of concept gemaakt met ondersteuning voor Facebook. Deze kan mentions van andere gebruikers eruit halen en omzetten naar emails. Met die emails wordt dan een bonus gegeven met standaard tekst.
