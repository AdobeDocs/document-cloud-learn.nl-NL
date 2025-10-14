---
title: Ingesloten functies voor elektronische handtekeningen en documenten maken
description: Leer hoe u Acrobat Sign API's kunt gebruiken om ervaringen voor elektronische handtekeningen en documenten in te sluiten in uw webplatforms en content- en documentbeheersystemen
feature: Integrations, Workflow
role: Developer
level: Intermediate
topic: Integrations
jira: KT-7489
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: 0a299592f0616988b6208fc98d3140f4ac22057e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Ingesloten ervaringen voor elektronische handtekeningen en documenten creëren

Leer hoe u Acrobat Sign API&#39;s kunt gebruiken om ervaringen voor elektronische ondertekening en documenten in te sluiten in uw webplatforms en content- en documentbeheersystemen. Deze praktische zelfstudie bevat vier onderdelen.

## Deel 1: Wat u nodig hebt

In deel 1 leert u hoe u aan de slag kunt gaan met alles wat u nodig hebt voor onderdelen 2-4. Laten we beginnen met het ophalen van API-aanmeldingsgegevens.

+++Meer informatie weergeven over het ophalen van API-aanmeldingsgegevens

* [Acrobat Sign-ontwikkelaarsaccount](https://www.adobe.com/acrobat/business/developer-form.html)
* [Startcode](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [&#x200B; de Code van VS (of redacteur van uw keus) &#x200B;](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — Ingebouwd installatieprogramma
   * Windows — Chocolade
   * Alle — https://www.python.org/downloads/

+++

## Deel 2: Weinig/Geen code — de kracht van webformulieren

In deel 2 verkent u de optie voor het gebruik van webformulieren met een lage of geen code. Het is altijd een goed idee om te zien of je kunt voorkomen dat je eerst code schrijft.

+++Bekijk details over het maken van een webformulier

1. Open Acrobat Sign met uw ontwikkelaarsaccount.

1. Selecteer **Een webformulier** publiceren op de startpagina.

   ![&#x200B; de homepage van Acrobat Sign van het Scherm &#x200B;](assets/embeddedesignature/embed_1.png)

1. Maak uw overeenkomst.

   ![&#x200B; Screenshot van hoe te om een Webvorm &#x200B;](assets/embeddedesignature/embed_2.png) te creëren

1. Sluit uw overeenkomst in op een platte HTML-pagina.

1. Experimenteer met het dynamisch toevoegen van queryparameters.

   ![&#x200B; Screenshot van het toevoegen van vraagparameters &#x200B;](assets/embeddedesignature/embed_3.png)

+++

## Deel 3: overeenkomst verzenden met een formulier en gegevens samenvoegen

In deel 3 maakt u dynamisch overeenkomsten.

+++Details weergeven over het dynamisch maken van overeenkomsten

Eerst moet u toegang instellen. Er zijn twee manieren om verbinding te maken met Acrobat Sign via API. OAuth-tokens en integratietoetsen. Tenzij u een zeer specifieke reden hebt om OAuth met uw toepassing te gebruiken, zou u de Sleutels van de Integratie eerst moeten onderzoeken.

1. Selecteer **Sleutel van de Integratie** op het **API menu van de Informatie** onder het **lusje van de Rekening** in Acrobat Sign.

   ![&#x200B; Screenshot van waar te om de integratiesleutel &#x200B;](assets/embeddedesignature/embed_4.png) te vinden

Nu u toegang hebt tot de API en deze kunt gebruiken, kunt u zien wat u kunt doen met de API.

1. Navigeer aan de [&#x200B; REST API Versie 6 Methoden van Acrobat Sign &#x200B;](http://adobesign.com/public/docs/restapi/v6).

   ![&#x200B; Screenshot van het navigeren Acrobat Sign REST API Versie 6 Methoden &#x200B;](assets/embeddedesignature/embed_5.png)

1. Gebruik het token als een &quot;toonder&quot;-waarde.

   ![&#x200B; Schermafbeelding van dragerwaarde &#x200B;](assets/embeddedesignature/embed_6.png)

Om uw eerste overeenkomst te verzenden, is het beter om te begrijpen hoe u de API kunt gebruiken.

1. Maak een document van voorbijgaande aard en verzend het.

>[!NOTE]
>
>Op JSON gebaseerde aanvraagaanroepen hebben een optie &quot;Model&quot; en &quot;Minimaal Modelschema&quot;. Dit geeft specs en een minimale ladingsreeks.

![&#x200B; Schermafbeelding van het creëren van een Voorbijgaande Doc &#x200B;](assets/embeddedesignature/embed_7.png)

Nadat u voor het eerst een overeenkomst hebt verzonden, kunt u de logica toevoegen. Het is altijd een goed idee om een aantal helpers op te zetten om herhaling te minimaliseren. Hier volgen enkele voorbeelden:

**Validering**

![Schermafbeelding van de validatielogica](assets/embeddedesignature/embed_8.png)

**Kopballen/Auth**

![&#x200B; Scherenshot van kopteksten/auth logica &#x200B;](assets/embeddedesignature/embed_9.png)

**Basis URI**

![&#x200B; Schermafbeelding van de logica van basis-URI &#x200B;](assets/embeddedesignature/embed_10.png)

Houd rekening met de plaats waar overgangsdocs aankomen binnen het grootse schema van het Sign-ecosysteem.
Overgang -> Overeenkomst
Overgang -> Sjabloon -> Overeenkomst
Overgang -> Widget -> Overeenkomst

In dit voorbeeld wordt een sjabloon als documentbron gebruikt. Dit is meestal de beste manier, tenzij u een solide reden hebt om documenten dynamisch te genereren ter ondertekening (bijvoorbeeld het genereren van verouderde code of documenten).

De code is vrij eenvoudig; er wordt een bibliotheekdocument (sjabloon) gebruikt voor de documentbron. De eerste en tweede ondertekenaars worden dynamisch toegewezen. De status `IN_PROCESS` betekent dat het document direct wordt verzonden. Daarnaast wordt `mergeFieldInfo` gebruikt om velden dynamisch te vullen.

![&#x200B; Screenshot van code om handtekeningen dynamisch toe te voegen &#x200B;](assets/embeddedesignature/embed_11.png)

+++

## Deel 4: ondertekenervaring, omleidingen en meer insluiten

In veel gevallen kunt u de activerende deelnemer toestaan om onmiddellijk een overeenkomst te ondertekenen. Dit is handig voor klantgerichte toepassingen en kiosken.

+++Bekijk details over het insluiten van de ondertekeningservaring

Als u niet wilt dat de eerste verzendende e-mail wordt geactiveerd, kunt u het gedrag eenvoudig beheren door de API-aanroep aan te passen.

![&#x200B; Schermafbeelding van code om het verzenden van e-mail niet te activeren &#x200B;](assets/embeddedesignature/embed_12.png)

Hieronder wordt beschreven hoe u de omleiding na ondertekening kunt beheren:

![Schermafbeelding van code voor omleiden na ondertekening](assets/embeddedesignature/embed_13.png)

Na het bijwerken van het proces voor het maken van de overeenkomst bestaat de laatste stap uit het genereren van de ondertekenings-URL. Deze aanroep is ook vrij eenvoudig en genereert een URL die een ondertekenaar kan gebruiken om toegang te krijgen tot zijn deel van het ondertekeningsproces.

![Schermafbeelding van code om een URL van de ondertekenaar te genereren](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>De aanroep om een overeenkomst te maken is technisch asynchroon. Dit betekent dat u een &#39;POST&#39;-overeenkomstoproep kunt maken, maar de overeenkomst nog niet klaar is. De beste manier is om een herhalingslus te creëren. Gebruik opnieuw proberen of wat dan ook de beste werkwijze voor je omgeving is.

![&#x200B; Screenshot die het beste praktijken zegt om een hertry lijn &#x200B;](assets/embeddedesignature/embed_15.png) te vestigen

Als alles samengebracht is, is de oplossing vrij eenvoudig. U maakt een overeenkomst en genereert vervolgens een ondertekenings-URL waarmee de ondertekenaar op het ondertekeningsritueel kan klikken en beginnen.

+++

## Aanvullende onderwerpen

* [&#x200B; Gebeurtenissen JS &#x200B;](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook-gebeurtenissen
   * [&#x200B; REST API &#x200B;](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [&#x200B; Webhooks in Acrobat Sign v6 &#x200B;](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [&#x200B; Reactivate de E-mails van het Verzoek (met gebeurtenissen) &#x200B;](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [&#x200B; vervang Onderbreking met opnieuw proberen &#x200B;](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* Aangepaste herinneringen
   * Met het eerste ontwerp

     ![&#x200B; Screenshot van het navigeren aan Macht automatiseren &#x200B;](assets/embeddedesignature/embed_16.png)

   * Of voeg één [&#x200B; in-vlucht &#x200B;](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant) toe
