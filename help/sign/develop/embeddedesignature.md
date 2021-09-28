---
title: Ingesloten e-handtekeningen en documentervaringen maken
description: Leer hoe u Adobe Sign API's kunt gebruiken om ervaringen voor elektronische handtekeningen en documenten in te sluiten in uw webplatforms en content- en documentbeheersystemen
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f015bd7ea1a25772a12cd0852d452d120f205a5c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Ingesloten ervaringen voor elektronische handtekeningen en documenten creëren

Leer hoe u Adobe Sign API&#39;s kunt gebruiken om ervaringen voor elektronische ondertekening en documenten in te sluiten in uw webplatforms en content- en documentbeheersystemen. Deze zelfstudie bevat vier onderdelen die in de onderstaande koppelingen worden beschreven:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Wat je nodig hebt" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Deel 1: Wat je nodig hebt</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Deel 2: Low/No Code — de kracht van webformulieren" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Deel 2: Low/No Code — de kracht van webformulieren</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Deel 3: Overeenkomst verzenden met een formulier, gegevens samenvoegen" src="assets/embeddedesignature/EmbedPart3_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Deel 3: Overeenkomst verzenden met een formulier en gegevens samenvoegen</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Deel 4: Ondertekeningservaring, omleidingen en meer insluiten" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Deel 4: Ondertekeningservaring, omleidingen en meer insluiten</strong></a>
    </div>
  </td>
</tr>
</table>

## Deel 1: Wat je nodig hebt {#part1}

In deel 1 leert u aan de slag te gaan met alles wat u nodig hebt voor de onderdelen 2-4. Laten we beginnen met het ophalen van API-referenties.

* [Adobe Sign-ontwikkelaarsaccount](https://acrobat.adobe.com/nl/nl/sign/developer-form.html)
* [Eenvoudige code](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS-code (of editor van uw keuze)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — Ingebouwd installatieprogramma
   * Windows — Chocolade
   * Alle — https://www.python.org/downloads/

## Deel 2: Low/No Code — de kracht van webformulieren {#part2}

In deel 2 gaat u de optie Low/no-code gebruiken bij het gebruik van webformulieren. Het is altijd een goed idee om te zien of je kunt voorkomen dat je eerst code schrijft.

1. Open Adobe Sign met uw ontwikkelaarsaccount.
1. Klik op **Een webformulier publiceren** op de startpagina.

   ![Schermafbeelding Adobe Sign-startpagina](assets/embeddedesignature/embed_1.png)

1. Maak uw overeenkomst.

   ![Screenshot van hoe u een webformulier kunt maken](assets/embeddedesignature/embed_2.png)

1. Sluit uw overeenkomst in op een platte HTML-pagina.
1. Experimenteer met het dynamisch toevoegen van queryparameters.

   ![Screenshot van het toevoegen van queryparameters](assets/embeddedesignature/embed_3.png)

## Deel 3: Overeenkomst verzenden met een formulier en gegevens samenvoegen {#part3}

In deel 3 gaat u dynamisch overeenkomsten maken.

Eerst, zult u toegang moeten vestigen. Met Adobe Sign kunt u op twee manieren verbinding maken via een API. OAuth-tokens en integratietoetsen. Tenzij u een zeer specifieke reden hebt om OAuth met uw toepassing te gebruiken, zult u eerst de Sleutels van de Integratie willen onderzoeken.

1. Selecteer **Integratiesleutel** in het menu **API-informatie** onder het tabblad **Account** in Adobe Sign.

   ![Screenshot van de integratiesleutel](assets/embeddedesignature/embed_4.png)

Nu u toegang hebt tot de API en deze kunt gebruiken, kunt u zien wat u kunt doen met de API.

1. Navigeer naar de [Adobe Sign REST API versie 6 Methods](http://adobesign.com/public/docs/restapi/v6).

   ![Screenshot van navigatie Adobe Sign REST API versie 6 Methods](assets/embeddedesignature/embed_5.png)

1. Gebruik het token als een &quot;toonder&quot;-waarde.

   ![Schermafbeelding van waarde toonder](assets/embeddedesignature/embed_6.png)

Om uw eerste overeenkomst te verzenden, is het beter om te begrijpen hoe u de API kunt gebruiken.

1. Maak een document van voorbijgaande aard en verzend het.

>[!NOTE]
>
>Op JSON gebaseerde aanvraagaanroepen hebben een optie &quot;Model&quot; en &quot;Minimaal Modelschema&quot;. Dit geeft specs en een minimumladingsreeks.

![Screenshot van het maken van een tijdelijk document](assets/embeddedesignature/embed_7.png)

Nadat u een overeenkomst voor de eerste keer hebt verzonden, kunt u de logica toevoegen. Het is altijd een goed idee om een aantal hulpstoffen in te stellen om herhaling te minimaliseren. Hier volgen een paar voorbeelden:

**Validatie**

![Screenshot van validatielogica](assets/embeddedesignature/embed_8.png)

**Kopteksten/auth**

![Schermafbeelding van kopteksten/auth-logica](assets/embeddedesignature/embed_9.png)

**Basis-URI**

![Screenshot van de Base URI-logica](assets/embeddedesignature/embed_10.png)

Houd rekening met de plaats waar overgangsdocs aankomen binnen het grootse schema van het Sign-ecosysteem.
Overgang -> Overeenkomst
Overgang -> Sjabloon -> Overeenkomst
Overgang -> Widget -> Overeenkomst

In dit voorbeeld wordt een sjabloon als documentbron gebruikt. Dit is meestal de beste manier, tenzij u een solide reden hebt om documenten dynamisch te genereren ter ondertekening (bijvoorbeeld het genereren van verouderde code of documenten).

De code is vrij eenvoudig; er wordt een bibliotheekdocument (sjabloon) gebruikt voor de documentbron. De eerste en tweede ondertekenaars worden dynamisch toegewezen. De status `IN_PROCESS` betekent dat het document direct wordt verzonden. `mergeFieldInfo` wordt ook gebruikt om velden dynamisch te vullen.

![Screenshot van code om handtekeningen dynamisch toe te voegen](assets/embeddedesignature/embed_11.png)

## Deel 4: Ondertekeningservaring, omleidingen en meer insluiten {#part4}

In veel gevallen kunt u de activerende deelnemer toestaan om onmiddellijk een overeenkomst te ondertekenen. Dit is handig voor klantgerichte toepassingen en kiosken.

Als u niet wilt dat de eerste verzendende e-mail wordt geactiveerd, kunt u het gedrag eenvoudig beheren door de API-aanroep aan te passen.

![Screenshot van code die het verzenden van e-mail niet activeert](assets/embeddedesignature/embed_12.png)

Hieronder wordt beschreven hoe u de omleiding na ondertekening kunt beheren:

![Screenshot van code voor controle over omleiding na ondertekening](assets/embeddedesignature/embed_13.png)

Na het bijwerken van het maken van de overeenkomst genereert de laatste stap de URL voor ondertekening. Deze aanroep is ook vrij eenvoudig en genereert een URL die een ondertekenaar kan gebruiken om toegang te krijgen tot zijn deel van het ondertekeningsproces.

![Screenshot van code om een ondertekenaar-URL te genereren](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>De aanroep van de overeenkomst is technisch asynchroon. Dit betekent dat er een &#39;POST&#39;-overeenkomstaanroep kan worden gedaan, maar dat de overeenkomst nog niet klaar is. De beste manier is om een herhalingslus tot stand te brengen. Gebruik opnieuw proberen of wat dan ook de beste werkwijze voor je omgeving is.

![Screenshot zegt dat het de beste manier is om een herhalingslus tot stand te brengen](assets/embeddedesignature/embed_15.png)

Als alles samengebracht is, is de oplossing vrij eenvoudig. U maakt een overeenkomst en genereert vervolgens een ondertekenings-URL waarmee de ondertekenaar op het ondertekeningsritueel kan klikken en beginnen.

### Aanvullende onderwerpen

* [JS-gebeurtenissen](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook-gebeurtenissen
   * [REST-API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks in Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Verzoek-e-mails opnieuw activeren (met gebeurtenissen)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Time-out vervangen door opnieuw proberen](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Aangepaste herinneringen
   * Met het eerste ontwerp

      ![Screenshot van navigatie naar Power Automate](assets/embeddedesignature/embed_16.png)

   * Of voeg een [in-flight](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant) toe

## Extra bronnen

http://bit.ly/Summit21-T126

Omvat:
* Adobe Sign-ontwikkelaarsaccount
* Adobe Sign API-documenten
* Voorbeeldcode
* Visual Studio Code
* Python
