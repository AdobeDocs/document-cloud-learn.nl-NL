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

Leer hoe u een tekstbericht, e-mail of pushmelding verstuurt om de ondertekenaar te laten weten dat er een overeenkomst gaande is met Acrobat Sign, Acrobat Sign for Salesforce, Marketo en de Marketo Salesforce Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [ Twilio SMS ](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar andere oplossingen van Marketo SMS zijn beschikbaar.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   De informatie en de recentste stop in voor de Synchronisatie van Salesforce zijn beschikbaar [ hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installeer Acrobat Sign voor Salesforce.

   De informatie over deze stop is beschikbaar [ hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce-synchronisatie en Acrobat Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![ Admin ](assets/adminTab.png)

![ de Synchronisatie van Objecten ](assets/salesforceAdmin.png)

1. Klik **Schema van de Synchronisatie** als dit uw eerste keer is. Anders, verfrist de klik **Schema**.

   ![ verfrissen zich ](assets/refreshSchema1.png)

1. Als de globale synchronisatie loopt, maak onbruikbaar door **Globale Synchronisatie** onbruikbaar te klikken.

   ![ onbruikbaar maken ](assets/disableGlobal.png)

1. Klik **vernieuwen Schema**.

   ![ vernieuw 2 ](assets/refreshSchema2.png)

## Aangepaste objecten synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**laat Synchronisatie** voor de voorwerpen onder Lood toe als u wilt teweegbrengen wanneer een Lood aan een overeenkomst in Salesforce wordt toegevoegd.

**laat Synchronisatie** voor de voorwerpen onder Contact toe als u wilt teweegbrengen wanneer een Contact aan een overeenkomst in Salesforce wordt toegevoegd.

**laat Synchronisatie** voor de voorwerpen onder Rekening toe als u wilt teweegbrengen wanneer een Rekening aan een overeenkomst in Salesforce wordt toegevoegd.

1. **laat Synchronisatie** voor de douanevoorwerpen toe die onder de gewenste Ouder (Lood, Contact, of Rekening) worden getoond.

   ![ de Objecten van de Douane ](assets/customObjects.png)

1. De volgende activa tonen hoe te **toelaten Synchronisatie**.

   ![ Synchronisatie van de Douane 1 ](assets/customObjectSync1.png)

   ![ Synchronisatie van de Douane 2 ](assets/customObjectSync2.png)

1. Als u klaar bent met synchroniseren op de aangepaste objecten, activeert u de synchronisatie opnieuw.

   ![ laat Globale ](assets/enableGlobal.png) toe

## Het programma maken

1. In de sectie van de Activiteiten van de Marketing van Marketo, klik op **Activiteiten van de Marketing** op de linkerbar met de rechtermuisknop aan, selecteer **Nieuwe Omslag van de Campagne**, en geef het een naam.

   ![ Nieuwe Omslag ](assets/newFolder.png)

1. Klik op de gecreeerde omslag met de rechtermuisknop aan, selecteer **Nieuw Programma**, en geef het een naam. Laat alles anders als gebrek, dan klik **creëren**.

   ![ Nieuw Programma 1 ](assets/newProgram1.png)

   ![ Nieuw Programma 2 ](assets/newProgram2.png)

## Twilio SMS instellen

Zorg er eerst voor dat u een actief Twilio-account hebt en de gewenste SMS-functies hebt aangeschaft.

Voor het instellen van de Marketo - Twilio SMS-webhook hebt u drie Twilio-parameters van uw account nodig.

- Account SID
- Accounttoken
- Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik op **Admin** in het hoogste recht.

   ![ Admin ](assets/adminTab.png)

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

   ![ Slimme Campaign 1 ](assets/smartCampaign1.png)

1. Noem het, dan klik **creeer**.

   ![ Slimme Campaign 2 ](assets/smartCampaign3.png)

   Als de configuratie voor de aangepaste objectsynchronisatie correct is voltooid, ziet u de volgende triggers die beschikbaar zijn voor gebruik in de Salesforce-map.

1. Klik en sleep Toegevoegd aan overeenkomst aan de slimme lijst. Voeg eventuele beperkingen toe die u op de trigger wilt hebben.

   ![ Toegevoegd aan Overeenkomst 2 ](assets/addedToAgreement2.png)

## De slimme-campagnestroom instellen

1. Klik op het **Stroom** lusje in de Slimme Campagne. Zoek naar en sleep de **stroom van het Web van de Vraag** op het canvas en selecteer webhook u in de vorige sectie creeerde.

   ![ Webhook van de Vraag ](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.
