# Ontwerp

Door de ASD project methode is de applicatie gaande tijd veranderd. Dit is omdat de requirements vanuit de klant aanpasde. De eerste iteratie was alleen met Slack ondersteuning en directe communicatie met de Blockchain. Daarna kwam de vraag voor ondersteuning voor andere chat services; er was gekozen voor Facebook. Het moest wel zo opgezet worden dat het uitbreidbaar was voor eventueel andere chat services, dit was iteratie 2. Na deze realisatie heb ik feedback gevraagd aan mede collega's en kwam ik tot de conclusie om een micro service architectuur te implementeren. Dit is zodat elke chat service een aparte service + stack heeft (zelf gekozen programmeer taal en chat implementatie). Op deze manier is alles helemaal los van elkaar. De chat service implementaties weten niks van de blockchain, alleen van het `core` project. Hier zijn verschillende endpoints op om data op te halen of te versturen.

## Eerste iteratie

Dit was de eerste iteratie. Het was een `Controller` met een endpoint voor de Slack webhook. Deze functie riep dan functies aan op de Blockchain waardoor er problemen waren met de time-out's. Een van de randvoorwaardes van Slack is dat er binnen 3 seconde een reactie verstuurd moet worden. Deze reactie wordt dan naar de gene gestuurd die het commando heeft aangeroepen. Omdat de Blockchain langer doet over verwerken van data door de decentralized nature moet dit dus asynchroon opgelost worden. Dit voegde al snel veel complexiteit toe aan de applicatie. In deze iteratie was hier nog geen rekening mee gehouden.

## Tweede iteratie

Abstractie laag voor generieke implementatie van een chat service - Facebook

## Derde iteratie

Micro services

<!-- Ontwerp
•	Vorm en inhoud passend bij opdracht en context
•	Aansluitend bij analyse en advies en voldoende uitgewerkt voor realisatie
Extra uitleg
•	De belangrijkste ontwerpbesluiten zijn onderbouwd.
  -->
