[BPMN](bpmn/recruitment_process.bpmn)


### Overzicht van de GitHub Actions Workflow

Deze repository maakt gebruik van een GitHub Actions workflow om automatisch een visuele representatie van het BPMN (Business Process Model and Notation) diagram te genereren en toe te voegen aan de `README.md`. Hierdoor blijft de documentatie up-to-date zonder handmatige tussenkomst.

#### Wat Doet de Workflow?

De workflow voert de volgende stappen uit telkens wanneer er een push of pull request naar de `main` branch wordt gedaan:

1. **Repository Checkout**:
   - Haalt de laatste versie van de repository binnen zodat de workflow toegang heeft tot de bestanden.

2. **Zoeken naar het BPMN-bestand**:
   - Parseert de `README.md` om het pad naar het BPMN-bestand te vinden. Dit wordt gedaan door te zoeken naar een Markdown-link naar een `.bpmn` bestand, bijvoorbeeld:
     ```markdown
     [BPMN Diagram](path/to/your/file.bpmn)
     ```

3. **Genereren van de SVG Afbeelding**:
   - Verstuurt het BPMN-bestand naar de [Kroki](https://kroki.io/) API om een SVG-afbeelding te genereren van het BPMN-diagram.
   - Slaat de gegenereerde `diagram.svg` op in de `images` directory van de repository.

4. **Bijwerken van de README.md**:
   - Controleert of de sectie "## BPMN Diagram" al bestaat in de `README.md`.
     - **Als de sectie bestaat**: Vervangt de bestaande afbeelding met de nieuw gegenereerde SVG.
     - **Als de sectie niet bestaat**: Voegt de sectie "## BPMN Diagram" toe aan het einde van de `README.md` met de gegenereerde SVG afbeelding.
   - De Markdown-syntaxis voor het toevoegen van de afbeelding wordt gebruikt:
     ```markdown
     ## BPMN Diagram

     ![BPMN Diagram](images/diagram.svg)
     ```

5. **Commit en Push van Wijzigingen**:
   - Commits de nieuwe `diagram.svg` en bijgewerkte `README.md` terug naar de `main` branch.
   - Zorgt ervoor dat de workflow zichzelf niet in een oneindige lus triggert door `[skip ci]` in het commit bericht te gebruiken.

#### Voordelen van deze Workflow

- **Automatisering**: Elimineert de noodzaak om handmatig afbeeldingen van BPMN-diagrammen te genereren en bij te werken.
- **Consistentie**: Zorgt ervoor dat de documentatie altijd de meest recente versie van het BPMN-diagram weergeeft.
- **Efficiëntie**: Bespaart tijd en vermindert de kans op menselijke fouten bij het updaten van documentatie.
- **Schaalbaarheid**: Kan eenvoudig worden uitgebreid om meerdere BPMN-diagrammen te ondersteunen of andere typen diagrammen toe te voegen.

#### Hoe Werkt Het?

1. **Initial Setup**:
   - Zorg ervoor dat je een BPMN-bestand hebt en dat het correct is gekoppeld in je `README.md` zoals hierboven beschreven.
   
2. **Wijzigingen Aanbrengen**:
   - Wanneer je het BPMN-bestand bijwerkt of wijzigt, commit en push je de wijzigingen naar de `main` branch.

3. **Automatische Generatie**:
   - De GitHub Actions workflow detecteert de push en voert de stappen uit om een nieuwe SVG te genereren en de `README.md` bij te werken.

4. **Resultaat**:
   - Na succesvolle uitvoering van de workflow, zie je de bijgewerkte BPMN-diagram in de `README.md`.

#### Troubleshooting

- **Workflow Foutmeldingen**:
  - Controleer de **Actions** tab in je repository om gedetailleerde logs te bekijken van de mislukte workflow runs.
  - Zorg ervoor dat de link naar het BPMN-bestand correct is en dat het bestand bestaat op de opgegeven locatie.

- **Kroki API Limieten**:
  - De publieke Kroki API heeft limieten op het aantal verzoeken. Als je veel diagrammen hebt of de workflow vaak draait, overweeg dan om een eigen Kroki-server te hosten.

- **Validatie van BPMN-bestand**:
  - Zorg ervoor dat je BPMN-bestand geldig is en geen fouten bevat die het renderen kunnen verhinderen.

#### Aanpassen van de Workflow

Indien nodig kun je de workflow aanpassen aan jouw specifieke behoeften. Enkele mogelijke aanpassingen zijn:

- **Ondersteuning voor Meerdere Diagrammen**:
  - Breid de workflow uit om meerdere BPMN-bestanden te ondersteunen en genereer afzonderlijke SVG-afbeeldingen voor elk diagram.
  
- **Optimalisatie van Afbeeldingsgrootte**:
  - Gebruik tools zoals [SVGO](https://github.com/svg/svgo) om de gegenereerde SVG-bestanden te optimaliseren en de bestandsgrootte te verkleinen.

- **Custom Styling**:
  - Pas de CSS in de gegenereerde HTML aan om de stijl van het BPMN-diagram te veranderen.

### Hoe de Workflow te Beheren

- **Toevoegen of Wijzigen van BPMN-bestanden**:
  - Voeg nieuwe BPMN-bestanden toe aan de repository en koppel ze in de `README.md` zoals eerder beschreven.
  
- **Monitoren van de Workflow**:
  - Houd de **Actions** tab in de gaten voor eventuele fouten of waarschuwingen die tijdens de workflow-uitvoering optreden.

- **Updaten van Dependencies**:
  - Indien de workflow afhankelijk is van externe tools of API's, zorg ervoor dat je deze regelmatig bijwerkt naar de nieuwste versies om compatibiliteit en beveiliging te waarborgen.

### Conclusie

Deze GitHub Actions workflow automatiseert het genereren en bijwerken van BPMN-diagrammen in je `README.md`. Door deze automatisering verbeter je de efficiëntie en nauwkeurigheid van je documentatie, wat bijdraagt aan een betere projectpresentatie en samenwerking.