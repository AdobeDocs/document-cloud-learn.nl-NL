---
title: Meldingen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Meldingen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo

Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is met Acrobat Sign, Acrobat Sign for Microsoft Dynamic, Marketo en Marketo Microsoft Dynamics Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [&#x200B; Twilio SMS &#x200B;](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar andere oplossingen van Marketo SMS zijn beschikbaar.

## Vereisten

1. Installeer de Marketo Microsoft Dynamics Sync.

   De informatie en de recentste stop in voor de Synchronisatie van de Dynamiek van Microsoft zijn beschikbaar [&#x200B; hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html?lang=nl-NL)

1. Installeer Acrobat Sign voor Microsoft Dynamics.

   De informatie over deze stop is beschikbaar [&#x200B; hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Microsoft Dynamics Sync en Acrobat Sign for Dynamics zijn geconfigureerd, verschijnen er twee nieuwe opties in de Marketo Admin Terminal.

![&#x200B; Admin &#x200B;](assets/adminTerminal.png)

* Klik **[!UICONTROL de Synchronisatie van de Entiteiten van de Dynamics]**.

  Synchronisatie moet worden uitgeschakeld voordat u aangepaste entiteiten synchroniseert. Klik **[!UICONTROL Schema van de Synchronisatie]** als dit uw eerste keer is. Anders, verfrist de klik **[!UICONTROL Schema]**.

  ![&#x200B; verfrissen zich &#x200B;](assets/refreshSchema.png)

## Het aangepaste object synchroniseren

1. Op de rechterkant, bepaal de plaats van [!UICONTROL &#x200B; Lead &#x200B;], [!UICONTROL &#x200B; Contact &#x200B;], en [!UICONTROL &#x200B; rekening &#x200B;] - gebaseerde douanevoorwerpen.

   * **[!UICONTROL laat Synchronisatie]** voor de voorwerpen onder Lood toe als u wilt teweegbrengen wanneer een Lood aan een overeenkomst in Dynamiek wordt toegevoegd.

   * **[!UICONTROL laat Synchronisatie]** voor de voorwerpen onder Contact toe als u wilt teweegbrengen wanneer een Contact aan een overeenkomst in Dynamics wordt toegevoegd.

   * **[!UICONTROL laat Synchronisatie]** voor de voorwerpen onder Rekening toe als u wilt teweegbrengen wanneer een Rekening aan een overeenkomst in Dynamics wordt toegevoegd.

   * **laat Synchronisatie** voor het voorwerp van de Overeenkomst onder de gewenste Ouder toe (Lead, Contact, of Rekening).

   ![&#x200B; de Objecten van de Douane &#x200B;](assets/enableSyncDynamics.png)

1. Selecteer in het nieuwe venster de eigenschappen die u onder Overeenkomst wilt gebruiken.

   Laat de dozen onder **[!UICONTROL Beperking]** en **[!UICONTROL Trekker]** toe om hen aan uw Activiteiten van de Marketing bloot te stellen.

   ![&#x200B; Synchronisatie van de Douane 1 &#x200B;](assets/entitySync1.png)

   ![&#x200B; Synchronisatie van de Douane 2 &#x200B;](assets/entitySync2.png)

1. Activeer de synchronisatie opnieuw nadat u synchronisatie voor de aangepaste objecten hebt ingeschakeld.

   Ga terug naar de [!UICONTROL &#x200B; Terminal Admin &#x200B;], dan klik **[!UICONTROL Dynamiek van Microsoft]**, dan klik op **[!UICONTROL toelaten Synchronisatie]**.

   ![&#x200B; Dynamica van Microsoft &#x200B;](assets/microsoftDynamics.png)

   ![&#x200B; laat Globale &#x200B;](assets/enableGlobalDynamics.png) toe

## Het programma maken

1. In [!UICONTROL &#x200B; Activiteiten van de Marketing &#x200B;], klik **[!UICONTROL de Activiteiten van de Marketing]** op de linkerbar met de rechtermuisknop aan, selecteer **[!UICONTROL Nieuwe Omslag van de Campagne]**, en noem het.

   ![&#x200B; Nieuwe Omslag &#x200B;](assets/newFolder.png)

1. Klik op de gecreeerde omslag met de rechtermuisknop aan, selecteer **[!UICONTROL Nieuw Programma]**, en geef het een naam.

   Laat alles anders als gebrek, dan klik **[!UICONTROL creëren]**.

   ![&#x200B; Nieuw Programma 1 &#x200B;](assets/newProgram1.png)

   ![&#x200B; Nieuw Programma 2 &#x200B;](assets/newProgram2.png)

## [!DNL Twilio] SMS instellen

Zorg er eerst voor dat u een actieve [!DNL Twilio] -account hebt en schaf de gewenste SMS-functies aan.

Voor het instellen van de Marketo - [!DNL Twilio] SMS-webhook hebt u drie [!DNL Twilio] -parameters nodig van uw account.

* Account SID
* Accounttoken
* Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik **[!UICONTROL Admin]** in het hoogste recht.

   ![&#x200B; Admin &#x200B;](assets/adminTab.png)

1. Klik **[!UICONTROL Webhooks]**, dan klik **[!UICONTROL Nieuwe Webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Ga de Naam van a **[!UICONTROL Webhook]** en **[!UICONTROL Beschrijving]** in.

1. Voer de volgende URL in en vervang `ACCOUNT_SID` en `AUTH_TOKEN` door uw [!DNL Twilio] referenties.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteer **[!UICONTROL POST]** als uw type van Verzoek.

1. Ga het volgende **Malplaatje** in en ben zeker om `MY_TWILIO_NUMBER` met uw [!DNL Twilio] telefoonaantal en `YOUR_MESSAGE` met een bericht van uw het kiezen te vervangen.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Plaats de **[!UICONTROL Token Codering van het Verzoek]** aan *Vorm/URL*.

1. Plaats het type van Reactie aan *JSON* dan klik **[!UICONTROL sparen]**.

## Trigger voor slimme campagnes instellen

1. In de sectie van de Activiteiten van de Marketing, klik op het programma met de rechtermuisknop u creeerde, dan selecteer **[!UICONTROL Nieuwe Slimme Campagne]**.

   ![&#x200B; Slimme Campaign 1 &#x200B;](assets/smartCampaign1.png)

1. Noem het, dan klik **[!UICONTROL creeer]**.

   ![&#x200B; Slimme Campaign 2 &#x200B;](assets/smartCampaign3.png)

   Er zijn verschillende triggers beschikbaar voor gebruik in de Microsoft-map.

1. Klik en sleep **[!UICONTROL Toegevoegd aan Overeenkomst]** aan de **[!UICONTROL Slimme Lijst]**, dan voeg om het even welke beperkingen toe u wenst om op de trekker te hebben.

   ![&#x200B; Toegevoegd aan Overeenkomst &#x200B;](assets/addedToAgreementDynamics.png)

## De slimme-campagnestroom instellen

1. Klik het **[!UICONTROL lusje van de Stroom]** in de [!UICONTROL &#x200B; Slimme Campagne &#x200B;].

   Zoek naar en sleep de **stroom van het Web van de Vraag** op het canvas en selecteer webhook u in de vorige sectie creeerde.

   ![&#x200B; Webhook van de Vraag &#x200B;](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.
