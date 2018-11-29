# Beheer

## Agile

## Azure DevOps

Azure DevOps is een omgeving waar alle tooling bij elkaar komt voor je project beheer.

### Git

Het versiebeheersysteem wat gebruikt is heet Git. Dit is een decentrelized manier van versiebeheer. In Azure DevOps heb je verschillende repositories (BBB - Hoofd applicatie en proof of concepts).

De repository heeft een `master` branch, deze heeft een volledig werkende versie ten aller tijden. Elke feature wordt een nieuwe branch gebaseerd op de `master`. Uiteindelijk wordt er een pull request (`PR`) gemaakt. Deze PR wordt gecontroleerd en gemerged in de `master`. Deze wordt dan automatisch gebuild. Zie Pipelines/Build.

### Dashboard

Om het inzichtelijk te maken naar andere mensen toe wat ik aan het doen ben heb ik een dashboard ingericht. Dit dashboard bestaat uit verschillende blokjes. De blokjes die ik heb ingericht zijn:

- Taak overzicht, welke taken ik daadwerkelijk mee bezig ben
- Build statussen (gefaald of niet)
- Release statussen (Welke release er nu live is)
- Een lijst van commando's en waar je de Swagger kan vinden
- Hoe de applicatie opgebouwd is en in elkaar steekt met uitleg.

### Readme

Er is een `README.md` in de repository waar benodigde informatie in staat van de applicatie. Welke configuratie er allemaal is, of de build lukt en hoe je hem moet starten.

### Pipelines

Een pipeline is een groep taken die uitgevoerd moet worden om een doel te behalen. De 2 doelen die ik heb binnen mijn project zijn het bouwen van de applicatie en het releasen (deployen) van de applicatie in de Azure Cloud. Hier zijn dus 2 pipelines voor opgezet.

#### Build

De build pipeline doet een 4-tal taken.

1. Source code ophalen (een git checkout)
2. Gradle wrapper starten met de taak `bootWar`, deze bouwt een `war` archief die gebruikt wordt in Azure.
3. De files kopieren die `/build/libs/*.*` en `src/main/resources/*.sql` matchen, dit is de `ROOT.war` en de `schema.sql`. Deze worden als artifact gezien.
4. De artifacts zippen en publishen, zo heb je aan het einde van de build een `drop.zip` die gebruikt kan worden in de releae pipeline.

#### Release

## Swagger

## Actuator
