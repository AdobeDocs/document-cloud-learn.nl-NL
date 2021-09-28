---
title: Documentautomatisering met Adobe Sign for Microsoft Power Platform
description: Leer hoe u de Adobe Sign- en Adobe PDF Tools-connectors voor Microsoft Power Apps activeert en gebruikt. Bouw workflows waarmee je snel en veilig processen voor bedrijfsgoedkeuring en -ondertekening kunt automatiseren zonder code te schrijven
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---

# Documentautomatisering met Adobe Sign for Microsoft Power Platform

Leer hoe u de Adobe Sign- en Adobe PDF Tools-connectors voor Microsoft Power Apps activeert en gebruikt. Bouw workflows waarmee je snel en veilig bedrijfsgoedkeurings- en ondertekeningsprocessen kunt automatiseren zonder code te schrijven. Deze zelfstudie bevat vier onderdelen die in de onderstaande koppelingen worden beschreven:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Deel 1: Ondertekende overeenkomst opslaan in SharePoint met Adobe Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Deel 1: Ondertekende overeenkomst opslaan in SharePoint met Adobe Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Deel 2: Geautomatiseerd goedkeuringsproces voor elektronische ondertekening met Adobe Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Deel 2: Geautomatiseerd goedkeuringsproces voor elektronische ondertekening met Adobe Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Deel 3: Geautomatiseerde OCR van documenten met Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Deel 3: Geautomatiseerde OCR van documenten met Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Deel 4: Geautomatiseerde documentverzameling met Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Deel 4: Geautomatiseerde documentverzameling met Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Vereisten

* Microsoft 365 en Power Automate vertrouwdheid
* Adobe Sign-kennis
* Microsoft 365-account met toegang tot SharePoint en Power Automate (basis voor Adobe Sign, Premium voor Adobe PDF Tools)
* Adobe Sign for enterprise of Adobe Sign developer account

**Oefeningen 1 en 2**

* Adobe Sign-account met toegang tot de API. Een ontwikkelaarsaccount of een Enterprise-account.
* SharePoint-site toegankelijk via Power Automate waarop u bewerkingsmachtigingen hebt. Volledige beheertoegang wordt aanbevolen.
* Voorbeelddocument voor het goedkeuringsverzoek en de ondertekening van de handtekening.

**Oefeningen 3 en 4**

Materialen [hier](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial) downloaden

## Deel 1: Ondertekende overeenkomst opslaan in SharePoint met Adobe Sign {#part1}

In deel één gebruikt u een Power Automate Flow-sjabloon om een geautomatiseerde workflow in te stellen waarmee alle ondertekende overeenkomsten op uw SharePoint-site worden opgeslagen.

1. Navigeer naar Power Automate.
1. Zoek naar Adobe Sign.

   ![Screenshot van navigatie naar Power Automate](assets/documentautomation/automation_1.png)

1. Kies **Een Adobe Sign voltooide overeenkomst opslaan in de SharePoint-bibliotheek**.

   ![Screenshot van handeling Adobe Sign voltooid opslaan in SharePoint-bibliotheek](assets/documentautomation/automation_2.png)

1. Bekijk het scherm en configureer eventuele benodigde verbindingen. Schakel de Adobe Sign-verbinding in.
1. Klik op het blauwe symbool `+`.

   ![Screenshot van Adobe Sign- en SharePoint-flowverbinding](assets/documentautomation/automation_3.png)

1. Voer de e-mail naar uw Adobe Sign-account in en klik op het wachtwoordveld in het nieuwe venster.

   ![Schermafbeelding van Adobe Sign-aanmeldingsscherm](assets/documentautomation/automation_4.png)

   Wacht even totdat Adobe uw account heeft gecontroleerd.

   >[!NOTE]
   >
   >Deze controle leidt u naar de juiste aanmelding als u een Adobe ID of onze SSO gebruikt.

1. Voltooi de aanmelding.
1. Klik op **Doorgaan** om naar het Flow-bewerkingsscherm te gaan.
1. Geef de trigger een naam.

   ![Screenshot van de naam van de trigger](assets/documentautomation/automation_5.png)

1. Configureer uw SharePoint-instellingen.

   ![Screenshot van het configureren van uw SharePoint-instellingen](assets/documentautomation/automation_6.png)

   **Siteadres:** uw SharePoint-site
   **Mappad:** pad naar de gedeelde documenten die u wilt gebruiken
   **Bestandsnaam:** Standaard accepteren
   **Bestandsinhoud:** Standaard accepteren

1. De workflow opslaan.

   ![Schermafbeelding van het pictogram Opslaan](assets/documentautomation/automation_7.png)

1. Navigeer met de blauwe pijl terug naar het scherm met het stroomoverzicht. U zult deze stroom in deel 2 testen.

   ![Screenshot van het flowoverzichtsscherm](assets/documentautomation/automation_8.png)

U zult deze stroom in het volgende deel testen.

## Deel 2: Geautomatiseerd goedkeuringsproces voor elektronische ondertekening met Adobe Sign {#part2}

In deel twee bouwen we het eerste deel af met een robuustere flow en testen we beide flows om ze in actie te zien.

1. Selecteer **Sjablonen** aan de linkerkant van de interface Power Automate.

   ![Screenshot van het selecteren van sjablonen](assets/documentautomation/automation_9.png)

1. Zoek naar &quot;managergoedkeuring&quot;.
1. Selecteer **Goedkeuring aanvragen voor een geselecteerd bestand**.

   ![Screenshot van het selecteren van goedkeuring van aanvraagmanager voor een geselecteerd bestand](assets/documentautomation/automation_10.png)

   Bekijk de verbindingen en voeg eventuele ontbrekende verbindingen toe.

   >[!NOTE]
   >
   >Als dit de eerste stroom is u met goedkeuringen doet, zullen zij volledig worden gevormd wanneer de stroom loopt.

1. Klik op **Doorgaan** om naar het flowbewerkingsscherm te gaan.

   Deze flow heeft veel vooraf geconfigureerde stappen, waaronder foutcontrole en geneste voorwaardelijke stappen.

1. Configureer **Voor een geselecteerd bestand** als volgt:
   **Siteadres:** uw SharePoint-site
   **bibliotheeknaam:** gegevensopslagruimte
1. Voeg als volgt een invoer toe:
   **Type**: E-mail
   **Naam**: E-mail ondertekenaar

   ![Screenshot van het configureren van de flow](assets/documentautomation/automation_11.png)

1. Configureer **Bestandseigenschappen ophalen:** als volgt:
   **Siteadres:** uw SharePoint-site
   **bibliotheeknaam:** gegevensopslagruimte

1. Schuif omlaag en zoek **Indien ja**.

   ![Screenshot van de configuratie &#39;If yes&#39;](assets/documentautomation/automation_12.png)

1. Klik op **Een handeling toevoegen** in het vak **Indien ja** (niet de onderste) om de stappen toe te voegen die ter ondertekening moeten worden verzonden.

   ![Screenshot van het toevoegen van een handeling in het vak Indien ja](assets/documentautomation/automation_13.png)

1. Zoek naar **SharePoint krijg bestandsinhoud** en kies **Bestandsinhoud ophalen**.

   ![Screenshot van het zoekvak](assets/documentautomation/automation_14.png)

1. Configureer **Bestandsinhoud ophalen** als volgt:

   ![Schermafbeelding van de configuratie Bestandsinhoud ophalen](assets/documentautomation/automation_15.png)

   **Siteadres:** uw SharePoint-site.
   **Bestand-id:** zoek naar &#39;id&#39; en kies Id in de stap  **Bestandseigenschappen** ophalen.
1. Zoek naar &quot;Adobe&quot; en kies **Adobe Sign** om een andere handeling toe te voegen.

   ![Schermafbeelding van zoekmenu](assets/documentautomation/automation_16.png)

1. Typ &quot;upload&quot; in het zoekvak voor Adobe Sign en selecteer **Een document uploaden en een document-id ophalen**.
1. Zoek naar de dynamische variabele **Naam** om de naam op te halen van het item/document dat in de trigger is geselecteerd onder **Bestandsnaam**.
1. Klik **Expressie** in de variabele assistent onder **Bestandsinhoud**.

   ![Screenshot van een document uploaden en document-id ophalen scherm](assets/documentautomation/automation_17.png)

1. Voeg één apostrof toe, klik dan terug naar **Dynamische inhoud**, verwijder uw apostrof, selecteer **Bestandsinhoud** en klik vervolgens op **OK**.

   Zorg ervoor dat er geen extra apostroffen zijn en het lijkt op het onderstaande voorbeeld.

   ![Screenshot van hoe het scherm Dynamische inhoud eruit moet zien](assets/documentautomation/automation_18.png)

1. Zoek naar &quot;creëren&quot; in het zoekgebied van Adobe Sign om nog een Adobe Sign-actie toe te voegen.
1. Selecteer **Maken en overeenkomst van een geüpload document en verzenden voor ondertekening**.

   ![Schermafbeelding van zoeken naar maken](assets/documentautomation/automation_19.png)

1. Configureer de vereiste informatie:
Kies **Naam** in de assistent voor dynamische variabelen in **Naam overeenkomst**.
Kies **Document-id** in de assistent voor dynamische variabelen in **Document-id**.
Kies **E-mail ondertekenaar** van de assistent voor dynamische variabelen in **E-mail deelnemer**.
Voer &quot;1&quot; in **Deelnemervolgorde** in.
Kies **Ondertekenaar** uit vervolgkeuzelijst in **Deelnemerrol**.

   ![Screenshot van de vereiste informatie](assets/documentautomation/automation_20.png)

1. **** Sla de flow op.

### De stroom testen

Ga naar de documentenopslagplaats van uw SharePoint-site om deze uit te testen.

1. Selecteer het document en kies **Automate** en de **Flow** die u zojuist hebt gemaakt.

   ![Screenshot van het selecteren van het menu Automate en flow](assets/documentautomation/automation_21.png)

1. Start de flow om de verbindingen te valideren (alleen eerste flowrun).
1. Voer in **Message** een leuk bericht in voor de fiatteur.
1. Typ e-mail voor de documentondertekenaar in **E-mail ondertekenaar**.
1. Klik op **Stroom** uitvoeren.

De geconfigureerde fiatteur voor de gebruiker die de flow start, krijgt een goedkeuringsaanvraag. U kunt uw goedkeuring verlenen via e-mail of via het menu Power Automate Action Items.
Na goedkeuring ondertekent u uw document. Afhankelijk van uw gebruiker en als deze zijn aangemeld bij Sign, moet u de ondertekeningsvensters mogelijk openen in een privébrowservenster.

![Screenshot van het openen in privébrowservenster](assets/documentautomation/automation_22.png)

Voltooi de ondertekening en kijk terug in uw SharePoint-map.

![Screenshot van SharePoint-map](assets/documentautomation/automation_23.png)

## Deel 3: Geautomatiseerde OCR van documenten met Adobe PDF Tools {#part3}

In deel drie leert u hoe u OCR in PDF&#39;s automatiseert wanneer deze worden geïmporteerd in Microsoft SharePoint. Hiermee wordt een probleem opgelost dat optreedt met gescande PDF-documenten waarin niet kan worden gezocht in SharePoint.

![Screenshot van PDF-document in browser](assets/documentautomation/automation_24.png)

### Een map instellen in SharePoint

Ga naar Microsoft SharePoint waar u documenten wilt opslaan.

1. Klik op **+ Nieuw** om een nieuwe map met de naam &quot;Verwerkte contracten&quot; te maken.
1. Klik op **+ Nieuw** om een nieuwe map met de naam &quot;Oude contracten&quot; te maken.

   ![Screenshot van nieuwe mappen](assets/documentautomation/automation_25.png)

Naar deze mappen wordt nu verwezen als onderdeel van uw Power Automate-flow.

### Een flow maken van een sjabloon

1. Meld u aan bij https://flow.microsoft.com.
1. Klik op **Sjablonen** in de zijbalk.

   ![Screenshot van het selecteren van sjablonen](assets/documentautomation/automation_26.png)

1. Selecteer **Nieuwe toegevoegde bestanden converteren naar doorzoekbare tekst in SharePoint**.
1. Klik op het symbool **+** naast Adobe PDF Tools.

   ![Screenshot van het selecteren van het +-symbool](assets/documentautomation/automation_27.png)

1. Ga op een nieuw tabblad naar https://www.adobe.com/go/powerautomate_getstarted.
1. Klik op **Aan de slag**.

   ![Screenshot van de knop Aan de slag](assets/documentautomation/automation_28.png)

1. Meld u aan met uw Adobe ID.

   ![Schermafbeelding van het aanmeldingsscherm](assets/documentautomation/automation_29.png)

1. Voer Naam en beschrijving van referenties in en klik op **Referenties maken**.

   ![Screenshot van het scherm Create Credentials](assets/documentautomation/automation_30.png)

   Laat het venster met de referenties open. Je moet ze invoeren in Microsoft Power Automate.

   ![Screenshot van het browsertabblad om open te houden](assets/documentautomation/automation_31.png)

1. Voer de referenties in en klik op **Maken in Microsoft Power Automate**.

   ![Screenshot van het invoeren van de PDF Tools-referenties](assets/documentautomation/automation_32.png)

1. Klik op **Doorgaan**.

   ![Screenshot van waar te klikken op Doorgaan](assets/documentautomation/automation_33.png)

   Nu kun je een weergave van de workflow zien, en je moet deze configureren voor je omgeving.

1. Selecteer het veld Siteadres en kies welke SharePoint-site u gebruikt onder de trigger **Wanneer een bestand in een map wordt gemaakt.**

   ![Screenshot van het selecteren Wanneer een bestand wordt gemaakt in een mappentrigger](assets/documentautomation/automation_34.png)

1. Klik op het mappictogram om naar de map Oude contracten onder Map-id te navigeren.

   ![Screenshot van het selecteren van de map Oude contracten](assets/documentautomation/automation_35.png)

1. Bewerk de handeling **Bestand** maken onder aan de flow:

   Wijzig **Siteadres** in uw siteadres.
Geef de locatie van de map Verwerkte contracten op in het mappad.

1. Klik op **Opslaan** in de rechterbovenhoek.
1. Klik op **Testen**.
1. Selecteer **Handmatig**.
1. Klik op **Testen**.

   ![Screenshot van de testflow](assets/documentautomation/automation_36.png)

### Probeer de nieuwe flow

1. Navigeer naar de map Oude contracten in SharePoint.
1. Navigeer naar E03/Old Contracts in de oefenbestanden die u hebt gedownload.
1. Kopieer de bestanden ReleaseFormXX.pdf naar de map Old Contracts in SharePoint.

   ![Screenshot van het kopiëren van de bestanden](assets/documentautomation/automation_37.png)

Als u nu naar de map Verwerkte contracten navigeert, kunt u zien welke PDF&#39;s beschikbaar zijn nadat de stroom een paar minuten heeft geduurd. Als u de PDF&#39;s opent, ziet u dat de tekst selecteerbaar is.
Daarnaast indexeert SharePoint het document, zodat u de inhoud van uw documenten kunt doorzoeken vanuit de zoekbalk in SharePoint.

## Deel 4: Geautomatiseerde documentverzameling met Adobe PDF Tools {#part4}

In deel vier leert u hoe u een groot aantal documenten samenvoegt op basis van de informatie die wordt verstrekt tijdens het selecteren en starten van een flow vanuit Microsoft SharePoint. In dit scenario zal de flow:

* Vraag om informatie om te kiezen wat u in een pakket voor een klant wilt opnemen.
* Op basis van de verstrekte informatie worden veel documenten samengevoegd. Deze documenten bevatten een voorblad en optionele whitepapers.
* Het samengevoegde document wordt opgeslagen in SharePoint.

### oefenbestanden importeren in SharePoint

1. Open de map E04 in de oefenbestanden.
1. Importeer de mappen Voorstel, Sjablonen en Gegenereerd document in SharePoint.

   ![Schermafbeelding van importmappen](assets/documentautomation/automation_38.png)

Deze mappen worden ter referentie gebruikt. U zult met name het bestand Voorstel.docx gebruiken voor uw voorstel.

In de map Sjablonen vindt u een map Covers met daarin paginaomslagontwerpen voor verschillende steden. Er is ook een map Whitepapers met optionele extra whitepapers die aan het einde worden toegevoegd als deze is geselecteerd.

### Importeer de flow in Microsoft Power Automate

1. Meld u aan bij Microsoft Power Automate (https://flow.microsoft.com).
1. Klik op **Mijn stromen**.

   ![Screenshot van de locatie waar de Mijn flows moet worden geselecteerd](assets/documentautomation/automation_39.png)

1. Klik op **Importeren**.

   ![Schermafbeelding van importscherm](assets/documentautomation/automation_40.png)

1. Klik op **Uploaden** en kies de map GenerateVoorstel_20210311231623.zip in E04/Flows/.

   ![Screenshot van het selecteren van map](assets/documentautomation/automation_41.png)

1. Klik op **Importeren**.

1. Klik op het moersleutelpictogram onder Actie naast **Voorstel naar klant verzenden**.

   ![Screenshot van het moersleutelpictogram](assets/documentautomation/automation_42.png)

1. Selecteer **Maken als nieuw** onder Setup.
1. Stel de naam van de flow in onder Bronnaam.
1. Klik op **Opslaan**.

   Herhaal dit voor de andere gerelateerde bronnen en selecteer uw verbinding.

   ![Screenshot van het opslaan van het bestand](assets/documentautomation/automation_43.png)

1. Klik op **Importeren** nadat u al uw verbindingen hebt gemaakt.

### Instellen voor een geselecteerd bestand

Nu de flow is gemaakt, gaat u als volgt te werk:

1. Klik op **Bewerken**.

   ![Screenshot van de te selecteren bewerking](assets/documentautomation/automation_44.png)

1. Selecteer de trigger **Voor een geselecteerd bestand**.

   Voeg uw SharePoint-site toe aan het siteadres.
Voeg uw bibliotheek toe aan de bibliotheek.

   ![Screenshot van voltooide trigger](assets/documentautomation/automation_45.png)

### SjabloonMapPath instellen

1. Klik op de variabele templateFolderPath.
1. Stel het pad in naar de locatie van de map Sjablonen binnen de SharePoint-site die u hebt geïmporteerd.

### Omslag bestandsinhoud ophalen instellen

1. Klik op de handeling **Omslag** om het bereik uit te breiden.
1. **Omslag uitbreiden: Bestandsinhoud ophalen**.

   Stel het siteadres in op uw SharePoint-site.

   ![Schermafbeelding van uitgevouwen omslag](assets/documentautomation/automation_46.png)



### Geselecteerd bestand instellen

1. Vouw de bereikactie **Geselecteerd bestand** uit.

   Wijzig het siteadres en de bibliotheeknaam in respectievelijk uw SharePoint-site en -bibliotheek onder **Bestandseigenschappen ophalen**.
Wijzig het siteadres in uw SharePoint-site onder **Bestandsinhoud ophalen**.

   ![Schermafbeelding van uitgevouwen geselecteerd bestand, actie](assets/documentautomation/automation_47.png)

### Whitepapers instellen

1. Klik op de handeling **Whitepapers**.
1. **Voorwaarde uitbreiden: Whitepaper toevoegen**.

   ![Schermafbeelding van de uitgevouwen voorwaarde Whitepaper toevoegen](assets/documentautomation/automation_48.png)

1. **Whitepaper 1 uitvouwen: Bestandsinhoud ophalen met het pad**.
Bewerk het siteadres in uw opgegeven SharePoint-site.

Herhaal dezelfde stappen voor **Voorwaarde: Whitepaper 2** toevoegen.

### Bestand maken instellen

1. Vouw **Bestand maken** uit.

   Bewerk het siteadres en mappad naar de SharePoint-site en het pad waar de map met gegenereerde documenten zich bevindt.

1. Klik op **Opslaan**.

### Uw flow testen

1. Navigeer naar de map met het voorstel in SharePoint.
1. Selecteer de map Request.docx.

   ![Screenshot van het selecteren van de map met voorstellen](assets/documentautomation/automation_49.png)

1. Selecteer uw flow in het menu **Automatisch**.

   ![Screenshot van het menu Automatisch selecteren](assets/documentautomation/automation_50.png)

1. Klik op **Doorgaan** om met de flow te beginnen.

   ![Screenshot van de knop Doorgaan selecteren](assets/documentautomation/automation_51.png)

1. Kies de omslag en de whitepapers die u wilt toevoegen.
1. Klik op **Stroom** uitvoeren.

   ![Schermafbeelding van knop Stroom uitvoeren](assets/documentautomation/automation_52.png)

Navigeer naar de map Generate Docs. Nu wordt het gegenereerde PDF-bestand weergegeven.

![Screenshot van SharePoint-map met nieuw PDF-bestand](assets/documentautomation/automation_53.png)

### Protect en andere acties toevoegen aan flow

Nu u een flow hebt gemaakt, gaat u uw flow bewerken om het PDF-document te versleutelen met een wachtwoord. Dit doorloopt ook hoe u andere acties kunt gebruiken.

1. Ga terug naar het einde van de flow.
1. Klik op het symbool **+** tussen **PDF&#39;s samenvoegen** en **Bestand maken**.

   ![Screenshot van het te selecteren + symbool](assets/documentautomation/automation_54.png)

1. Selecteer **Een handeling toevoegen**.
1. Zoek naar &quot;Adobe PDF Tools&quot;.

   ![Screenshot van het zoeken naar Adobe PDF](assets/documentautomation/automation_55.png)

1. Selecteer **Protect PDF in weergave**.
1. Gebruik dynamische inhoud om het veld Bestandsnaam in te stellen op **PDF-bestandsnaam uit PDF samenvoegen**.

   ![Screenshot van dynamische inhoud](assets/documentautomation/automation_56.png)

   In de trigger is er een veld Wachtwoord dat deel uitmaakt van het initiëringsformulier. We kunnen dat hier gebruiken.

1. Zoek naar **Wachtwoordveld** met behulp van dynamische inhoud en plaats dit in het veld Wachtwoord.

   ![Schermafbeelding van zoeken naar wachtwoord](assets/documentautomation/automation_57.png)

1. Gebruik dynamische inhoud om deze in te stellen op **PDF-bestandsinhoud van PDF&#39;s samenvoegen** in het veld Bestandsinhoud.
1. Wijzig **Bestand maken** om de bestandsinhoud op te halen uit Protect PDF in plaats van PDF&#39;s samen te voegen.
1. Vouw **Bestand maken** uit.
1. Wis het veld Bestandsinhoud.
1. Gebruik dynamische inhoud om **PDF-bestandsinhoud** uit **Protect PDF te plaatsen vanuit Weergave**.

### Uw flow testen

1. Navigeer naar de map met het voorstel in SharePoint.
1. Selecteer Voorstel.docx.

   ![Screenshot van het selecteren van de map Voorstel](assets/documentautomation/automation_58.png)

1. Selecteer **Automatisch** om uw flow te kiezen.

   ![Screenshot van het selecteren Automatisch in het menu](assets/documentautomation/automation_59.png)

1. Klik op **Doorgaan** om met de flow te beginnen.

   ![Schermafbeelding van selecteren Doorgaan](assets/documentautomation/automation_60.png)

1. Kies de omslag en de whitepapers die u wilt toevoegen.
1. Stel het veld Wachtwoord in op het wachtwoord dat u wilt instellen.
1. Klik op **Stroom** uitvoeren.

   ![Schermafbeelding van geselecteerde bestanden en de knop Stroomset uitvoeren](assets/documentautomation/automation_61.png)

1. Navigeer naar de map Generate Docs.
Het gegenereerde PDF-bestand wordt weergegeven. Open het PDF-bestand en u wordt gevraagd uw PDF-wachtwoord in te voeren.

   ![Screenshot van gegenereerde PDF in SharePoint-directory](assets/documentautomation/automation_62.png)
