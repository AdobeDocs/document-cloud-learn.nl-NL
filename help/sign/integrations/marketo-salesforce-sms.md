---
title: Meldingen verzenden met Acrobat Sign for Salesforce en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Meldingen verzenden met Acrobat Sign for [!DNL Salesforce] en [!DNL Marketo]

Leer hoe u een tekstbericht, e-mail of pushmelding verstuurt om de ondertekenaar te laten weten dat er een overeenkomst gaande is met Acrobat Sign, Acrobat Sign for Salesforce, Marketo en de Marketo Salesforce Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [&#x200B; Twilio SMS &#x200B;](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar andere oplossingen van Marketo SMS zijn beschikbaar.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   De informatie en de recentste stop in voor de Synchronisatie van Salesforce zijn beschikbaar [&#x200B; hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html?lang=nl-NL)

1. Installeer Acrobat Sign voor Salesforce.

   De informatie over deze stop is beschikbaar [&#x200B; hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce-synchronisatie en Acrobat Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![&#x200B; Admin &#x200B;](assets/adminTab.png)

![&#x200B; de Synchronisatie van Objecten &#x200B;](assets/salesforceAdmin.png)

1. Klik **Schema van de Synchronisatie** als dit uw eerste keer is. Anders, verfrist de klik **Schema**.

   ![&#x200B; verfrissen zich &#x200B;](assets/refreshSchema1.png)

1. Als de globale synchronisatie loopt, maak onbruikbaar door **Globale Synchronisatie** onbruikbaar te klikken.

   ![&#x200B; onbruikbaar maken &#x200B;](assets/disableGlobal.png)

1. Klik **vernieuwen Schema**.

   ![&#x200B; vernieuw 2 &#x200B;](assets/refreshSchema2.png)

## Aangepaste objecten synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**laat Synchronisatie** voor de voorwerpen onder Lood toe als u wilt teweegbrengen wanneer een Lood aan een overeenkomst in Salesforce wordt toegevoegd.

**laat Synchronisatie** voor de voorwerpen onder Contact toe als u wilt teweegbrengen wanneer een Contact aan een overeenkomst in Salesforce wordt toegevoegd.

**laat Synchronisatie** voor de voorwerpen onder Rekening toe als u wilt teweegbrengen wanneer een Rekening aan een overeenkomst in Salesforce wordt toegevoegd.

1. **laat Synchronisatie** voor de douanevoorwerpen toe die onder de gewenste Ouder (Lood, Contact, of Rekening) worden getoond.

   ![&#x200B; de Objecten van de Douane &#x200B;](assets/customObjects.png)

1. De volgende activa tonen hoe te **toelaten Synchronisatie**.

   ![&#x200B; Synchronisatie van de Douane 1 &#x200B;](assets/customObjectSync1.png)

   ![&#x200B; Synchronisatie van de Douane 2 &#x200B;](assets/customObjectSync2.png)

1. Als u klaar bent met synchroniseren op de aangepaste objecten, activeert u de synchronisatie opnieuw.

   ![&#x200B; laat Globale &#x200B;](assets/enableGlobal.png) toe

## Het programma maken

1. In de sectie van de Activiteiten van de Marketing van Marketo, klik op **Activiteiten van de Marketing** op de linkerbar met de rechtermuisknop aan, selecteer **Nieuwe Omslag van de Campagne**, en geef het een naam.

   ![&#x200B; Nieuwe Omslag &#x200B;](assets/newFolder.png)

1. Klik op de gecreeerde omslag met de rechtermuisknop aan, selecteer **Nieuw Programma**, en geef het een naam. Laat alles anders als gebrek, dan klik **creëren**.

   ![&#x200B; Nieuw Programma 1 &#x200B;](assets/newProgram1.png)

   ![&#x200B; Nieuw Programma 2 &#x200B;](assets/newProgram2.png)

## Twilio SMS instellen

Zorg er eerst voor dat u een actief Twilio-account hebt en de gewenste SMS-functies hebt aangeschaft.

Voor het instellen van de Marketo - Twilio SMS-webhook hebt u drie Twilio-parameters van uw account nodig.

- Account SID
- Accounttoken
- Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik op **Admin** in het hoogste recht.

   ![&#x200B; Admin &#x200B;](assets/adminTab.png)

1. Klik op **Webhooks**, dan **Nieuwe Webhook**.

   ![Webhooks](assets/webhooks.png)

1. Ga de Naam van a **Webhook** en **Beschrijving** in.

1. Ga volgende URL in en ben zeker om **[ACCOUNT_SID]** en **[AUTH_TOKEN]** met uw geloofsbrieven van Twilio te vervangen.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteer **POST** als uw type van Verzoek.

1. Ga het volgende **Malplaatje** in en ben zeker om **[MY_TWILIO_NUMBER]** met uw Twilio telefoonaantal en **[UW_MESSAGE]** met een bericht van uw het kiezen te vervangen.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Stel de aanvraagtoken-codering in op formulier/URL.

1. Plaats het type van Reactie aan JSON dan klik **sparen**.

## Trigger voor slimme campagnes instellen

1. In de sectie van de Activiteiten van de Marketing, klik op het programma met de rechtermuisknop u creeerde, dan selecteer **Nieuwe Slimme Campagne**.

   ![&#x200B; Slimme Campaign 1 &#x200B;](assets/smartCampaign1.png)

1. Noem het, dan klik **creeer**.

   ![&#x200B; Slimme Campaign 2 &#x200B;](assets/smartCampaign3.png)

   Als de configuratie voor de aangepaste objectsynchronisatie correct is voltooid, ziet u de volgende triggers die beschikbaar zijn voor gebruik in de Salesforce-map.

1. Klik en sleep Toegevoegd aan overeenkomst aan de slimme lijst. Voeg eventuele beperkingen toe die u op de trigger wilt hebben.

   ![&#x200B; Toegevoegd aan Overeenkomst 2 &#x200B;](assets/addedToAgreement2.png)

## De slimme-campagnestroom instellen

1. Klik op het **Stroom** lusje in de Slimme Campagne. Zoek naar en sleep de **stroom van het Web van de Vraag** op het canvas en selecteer webhook u in de vorige sectie creeerde.

   ![&#x200B; Webhook van de Vraag &#x200B;](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.
