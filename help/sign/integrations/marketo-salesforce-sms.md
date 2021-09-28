---
title: Meldingen verzenden met Adobe Sign for Salesforce en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Meldingen verzenden met Adobe Sign for Salesforce en Marketo

Leer hoe u een tekstbericht, e-mail of pushmelding verstuurt om de ondertekenaar te laten weten dat er een overeenkomst gaande is met Adobe Sign, Adobe Sign for Salesforce, Marketo en de Marketo Salesforce Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar andere oplossingen van Marketo SMS zijn beschikbaar.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   [Hier is informatie en de nieuwste insteekmodule voor Salesforce Sync beschikbaar.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installeer Adobe Sign voor Salesforce.

   [Hier is informatie over deze plug-in beschikbaar.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce-synchronisatie en Adobe Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![Beheerder](assets/adminTab.png)

![Objectsynchronisatie](assets/salesforceAdmin.png)

1. Klik **Schema synchroniseren** als dit uw eerste keer is. Klik anders op **Schema vernieuwen**.

   ![Vernieuwen](assets/refreshSchema1.png)

1. Als globale synchronisatie wordt uitgevoerd, kunt u deze uitschakelen door te klikken op **Globale synchronisatie uitschakelen**.

   ![Uitschakelen](assets/disableGlobal.png)

1. Klik op **Schema vernieuwen**.

   ![Vernieuwen 2](assets/refreshSchema2.png)

## Aangepaste objecten synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**Schakel** Synchroniseren voor de objecten onder Lead in als u wilt activeren wanneer een lead aan een overeenkomst in Salesforce wordt toegevoegd.

**Schakel** Synchroniseren voor de objecten onder Contactpersoon in als u wilt activeren wanneer een Contactpersoon aan een overeenkomst in Salesforce wordt toegevoegd.

**Schakel** Synchroniseren voor de objecten onder Account in als u wilt activeren wanneer een account wordt toegevoegd aan een overeenkomst in Salesforce.

1. **Schakel** Syncfor in voor de aangepaste objecten die worden weergegeven onder de gewenste bovenliggende element (lead, contact of account).

   ![Aangepaste objecten](assets/customObjects.png)

1. De volgende elementen tonen hoe u **Sync inschakelen**.

   ![Aangepaste synchronisatie 1](assets/customObjectSync1.png)

   ![Aangepaste synchronisatie 2](assets/customObjectSync2.png)

1. Als u klaar bent met synchroniseren op de aangepaste objecten, activeert u de synchronisatie opnieuw.

   ![Algemeen inschakelen](assets/enableGlobal.png)

## Het programma maken

1. Klik in de sectie Marketingactiviteiten van Marketo met de rechtermuisknop op **Marketingactiviteiten** op de linkerbalk en selecteer **Nieuwe campagnemap**. Geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map, selecteer **Nieuw programma** en geef deze een naam. Laat alle andere elementen standaard staan en klik op **Maken**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

## Twilio SMS instellen

Zorg er eerst voor dat je een actief Twilio-account hebt en de SMS-functies hebt aangeschaft die je nodig hebt.

Voor het instellen van de Marketo - Twilio SMS-webhook hebt u drie Twilio-parameters van uw account nodig.

- Account SID
- Accounttoken
- Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik op **Admin** rechtsboven.

   ![Beheerder](assets/adminTab.png)

1. Klik op **Webhooks**, dan **Nieuwe webhook**.

   ![Webhooks](assets/webhooks.png)

1. Voer een **Webhooknaam** en **Beschrijving** in.

1. Voer de volgende URL in en vervang **[ACCOUNT_SID]** en **[AUTH_TOKEN]** door uw Twilio-referenties.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteer **POST** als uw type verzoek.

1. Voer de volgende **Sjabloon** in en vervang **[MY_TWILIO_NUMBER]** door uw Twilio-telefoonnummer en **[UW_MESSAGE]** door een bericht van uw keuze.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Stel de aanvraagtoken-codering in op Formulier/URL.

1. Stel het reactietype in op JSON en klik op **Opslaan**.

## Trigger voor slimme campagnes instellen

1. Klik in de sectie Marketingactiviteiten met de rechtermuisknop op het programma dat u hebt gemaakt en selecteer **Nieuwe slimme campagne**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef de naam op en klik op **Maken**.

   ![Slimme campagne 2](assets/smartCampaign3.png)

   Als de configuratie voor de aangepaste objectsynchronisatie correct is voltooid, ziet u de volgende triggers die beschikbaar zijn voor gebruik in de Salesforce-map.

1. Klik op Toegevoegd aan overeenkomst en sleep deze naar de slimme lijst. Voeg eventuele beperkingen toe die u op de trigger wilt hebben.

   ![Toegevoegd aan overeenkomst 2](assets/addedToAgreement2.png)

## De slimme-campagnestroom instellen

1. Klik op het tabblad **Flow** in de slimme campagne. Zoek en sleep de **Stroom Webhook** naar het canvas en selecteer de webhook die u in de vorige sectie hebt gemaakt.

   ![Bel webhook](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.

>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Adobe Sign voor Salesforce en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) die gratis beschikbaar is op Experience League!