---
title: Meldingen verzenden met Adobe Sign for Microsoft Dynamics 365 en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Meldingen verzenden met Adobe Sign for Microsoft Dynamics 365 en Marketo

Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is met Adobe Sign, Adobe Sign for Microsoft Dynamic, Marketo en de Marketo Microsoft Dynamics Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar andere oplossingen van Marketo SMS zijn beschikbaar.

## Vereisten

1. Installeer de Marketo Microsoft Dynamics Sync.

   [Hier is informatie en de nieuwste plug-in voor Microsoft Dynamics Sync beschikbaar.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installeer Adobe Sign voor Microsoft Dynamics.

   [Hier is informatie over deze plug-in beschikbaar.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Microsoft Dynamics Sync en Adobe Sign for Dynamics zijn geconfigureerd, verschijnen er twee nieuwe opties in de Marketo Admin Terminal.

![Beheerder](assets/adminTerminal.png)

* Klik op **[!UICONTROL Dynamics Entities Sync]**.

   Synchronisatie moet worden uitgeschakeld voordat u aangepaste entiteiten synchroniseert. Klik **[!UICONTROL Schema synchroniseren]** als dit uw eerste keer is. Klik anders op **[!UICONTROL Schema vernieuwen]**.

   ![Vernieuwen](assets/refreshSchema.png)

## Het aangepaste object synchroniseren

1. Zoek aan de rechterkant de op [!UICONTROL Lead], [!UICONTROL Contact] en [!UICONTROL Account] gebaseerde aangepaste objecten.

   * **[!UICONTROL Schakel]** Synchroniseren voor de objecten onder Lead in als u wilt activeren wanneer een lead in Dynamics aan een overeenkomst wordt toegevoegd.

   * **[!UICONTROL Schakel]** Synchroniseren voor de objecten onder Contactpersoon in als u wilt activeren wanneer een Contactpersoon aan een overeenkomst wordt toegevoegd in Dynamics.

   * **[!UICONTROL Schakel]** Synchroniseren voor de objecten onder Account in als u wilt activeren wanneer een Account in Dynamics wordt toegevoegd aan een overeenkomst.

   * **Schakel** Syncfor het overeenkomstobject in onder de gewenste bovenliggende element (lead, contact of account).

   ![Aangepaste objecten](assets/enableSyncDynamics.png)

1. Selecteer in het nieuwe venster de eigenschappen die u onder Overeenkomst wilt gebruiken.

   Schakel de selectievakjes onder **[!UICONTROL Restrictie]** en **[!UICONTROL Trigger]** in om deze zichtbaar te maken voor uw marketingactiviteiten.

   ![Aangepaste synchronisatie 1](assets/entitySync1.png)

   ![Aangepaste synchronisatie 2](assets/entitySync2.png)

1. Activeer de synchronisatie opnieuw nadat u synchronisatie voor de aangepaste objecten hebt ingeschakeld.

   Ga terug naar [!UICONTROL Admin Terminal], klik vervolgens op **[!UICONTROL Microsoft Dynamics]** en klik vervolgens op **[!UICONTROL Synchronisatie inschakelen]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Algemeen inschakelen](assets/enableGlobalDynamics.png)

## Het programma maken

1. Klik in [!UICONTROL Marketingactiviteiten] met de rechtermuisknop op **[!UICONTROL Marketingactiviteiten]** op de linkerbalk, selecteer **[!UICONTROL Nieuwe campagnemap]** en geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map, selecteer **[!UICONTROL Nieuw programma]** en geef deze een naam.

   Laat alle andere elementen standaard staan en klik op **[!UICONTROL Maken]**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

## [!DNL Twilio] SMS instellen

Zorg er eerst voor dat u een actieve [!DNL Twilio]-account hebt en kocht de SMS-functies die u nodig hebt.

Voor het instellen van de Marketo - [!DNL Twilio] SMS-webhook hebt u drie [!DNL Twilio] parameters van uw account nodig.

* Account SID
* Accounttoken
* Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klik op **[!UICONTROL Beheer]** rechtsboven.

   ![Beheerder](assets/adminTab.png)

1. Klik op **[!UICONTROL Webhooks]** en klik vervolgens op **[!UICONTROL Nieuwe webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Voer een **[!UICONTROL Webhooknaam]** en **[!UICONTROL Beschrijving]** in.

1. Voer de volgende URL in en vervang `ACCOUNT_SID` en `AUTH_TOKEN` door uw [!DNL Twilio]-referenties.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteer **[!UICONTROL POST]** als uw type verzoek.

1. Voer de volgende **Sjabloon** in en vervang `MY_TWILIO_NUMBER` door uw [!DNL Twilio]-telefoonnummer en `YOUR_MESSAGE` door een door u gekozen bericht.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Stel **[!UICONTROL Tokencodering aanvragen]** in op *Formulier/URL*.

1. Stel het reactietype in op *JSON* en klik vervolgens op **[!UICONTROL Opslaan]**.

## Trigger voor slimme campagnes instellen

1. Klik in de sectie Marketingactiviteiten met de rechtermuisknop op het programma dat u hebt gemaakt en selecteer **[!UICONTROL Nieuwe slimme campagne]**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef de naam op en klik op **[!UICONTROL Maken]**.

   ![Slimme campagne 2](assets/smartCampaign3.png)

   Er zijn verschillende triggers beschikbaar voor gebruik in de Microsoft-map.

1. Klik op **[!UICONTROL Toegevoegd aan overeenkomst]** en sleep deze naar de **[!UICONTROL Slimme lijst]**. Voeg vervolgens de gewenste beperkingen toe aan de trigger.

   ![Toegevoegd aan overeenkomst](assets/addedToAgreementDynamics.png)

## De slimme-campagnestroom instellen

1. Klik op het tabblad **[!UICONTROL Flow]** in de [!UICONTROL Slimme campagne].

   Zoek en sleep de **Stroom Webhook** naar het canvas en selecteer de webhook die u in de vorige sectie hebt gemaakt.

   ![Bel webhook](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.
>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Adobe Sign for Microsoft Dynamics en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) die gratis beschikbaar is op Experience League!