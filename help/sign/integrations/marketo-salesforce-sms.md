---
title: Meldingen verzenden met Acrobat Sign voor Salesforce en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Meldingen verzenden met Acrobat Sign voor Salesforce en Marketo

Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst actief is met Acrobat Sign, Acrobat Sign voor Salesforce, Marketo en de Marketo Salesforce Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar er zijn andere Marketo SMS-oplossingen beschikbaar.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   Informatie en de nieuwste insteekmodule voor Salesforce Sync zijn beschikbaar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installeer Acrobat Sign voor Salesforce.

   Informatie over deze plug-in is beschikbaar [hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce-synchronisatie en Acrobat Sign voor Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![Beheerder](assets/adminTab.png)

![Objectsynchronisatie](assets/salesforceAdmin.png)

1. Klikken **Schema synchroniseren** als dit uw eerste keer is. Anders klikt u op **Schema vernieuwen**.

   ![Vernieuwen](assets/refreshSchema1.png)

1. Als globale synchronisatie wordt uitgevoerd, schakelt u deze uit door op **Globale synchronisatie uitschakelen**.

   ![Uitschakelen](assets/disableGlobal.png)

1. Klikken **Schema vernieuwen**.

   ![Vernieuwen 2](assets/refreshSchema2.png)

## Aangepaste objecten synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**Synchronisatie inschakelen** voor de objecten onder Lead als u wilt activeren wanneer een lead aan een overeenkomst in Salesforce wordt toegevoegd.

**Synchronisatie inschakelen** voor de objecten onder Contactpersoon als u wilt activeren wanneer een Contactpersoon wordt toegevoegd aan een overeenkomst in Salesforce.

**Synchronisatie inschakelen** voor de objecten onder Account als u wilt activeren wanneer een Account wordt toegevoegd aan een overeenkomst in Salesforce.

1. **Synchronisatie inschakelen** voor de aangepaste objecten die worden weergegeven onder de gewenste bovenliggende element (lead, contact of account).

   ![Aangepaste objecten](assets/customObjects.png)

1. De volgende elementen laten zien hoe **Synchronisatie inschakelen**.

   ![Aangepaste synchronisatie 1](assets/customObjectSync1.png)

   ![Aangepaste synchronisatie 2](assets/customObjectSync2.png)

1. Als u klaar bent met synchroniseren op de aangepaste objecten, activeert u de synchronisatie opnieuw.

   ![Algemeen inschakelen](assets/enableGlobal.png)

## Het programma maken

1. Klik in de sectie Marketingactiviteiten van Marketo met de rechtermuisknop op **Marketingactiviteiten** op de linkerbalk selecteert u **Nieuwe campagnemap** en geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map en selecteer **Nieuw programma** en geef deze een naam. Laat alle andere elementen standaard staan en klik op **Maken**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

## Twilio SMS instellen

Zorg er eerst voor dat je een actief Twilio-account hebt en de SMS-functies hebt aangeschaft die je nodig hebt.

Voor het instellen van de Marketo - Twilio SMS-webhook hebt u drie Twilio-parameters van uw account nodig.

- Account SID
- Accounttoken
- Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik op **Beheerder** rechtsboven.

   ![Beheerder](assets/adminTab.png)

1. Klik op **Webhooks** dan **Nieuwe webhook**.

   ![Webhooks](assets/webhooks.png)

1. Voer een **Webhook-naam** en **Beschrijving**.

1. Voer de volgende URL in en vervang de URL **[ACCOUNT_SID]** en **[AUTH_TOKEN]** met uw Twilio-referenties.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteren **POST** als uw type verzoek.

1. Voer het volgende in **Sjabloon** en zorg ervoor dat u **[MY_TWILIO_NUMBER]** met uw Twilio-telefoonnummer en **[UW_BERICHT]** met een bericht van uw keuze.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Stel de aanvraagtoken-codering in op Formulier/URL.

1. Stel het reactietype in op JSON en klik vervolgens op **Opslaan**.

## Trigger voor slimme campagnes instellen

1. Klik in de sectie Marketingactiviteiten met de rechtermuisknop op het programma dat u hebt gemaakt en selecteer vervolgens **Nieuwe slimme campagne**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef de naam op en klik op **Maken**.

   ![Slimme campagne 2](assets/smartCampaign3.png)

   Als de configuratie voor de aangepaste objectsynchronisatie correct is voltooid, ziet u de volgende triggers die beschikbaar zijn voor gebruik in de Salesforce-map.

1. Klik op Toegevoegd aan overeenkomst en sleep deze naar de slimme lijst. Voeg eventuele beperkingen toe die u op de trigger wilt hebben.

   ![Toegevoegd aan overeenkomst 2](assets/addedToAgreement2.png)

## De slimme-campagnestroom instellen

1. Klik op de knop **Stroom** in de slimme campagne. Zoek en sleep de **Bel webhook** Ga naar het canvas en selecteer de webhook die u in de vorige sectie hebt gemaakt.

   ![Bel webhook](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.

>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Acrobat Sign voor Salesforce en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) dat is gratis beschikbaar op Experience League !