---
title: Meldingen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo
description: Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Meldingen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo

Leer hoe u een tekstbericht, e-mail of pushmelding verzendt om de ondertekenaar te laten weten dat een overeenkomst onderweg is met Acrobat Sign, Acrobat Sign for Microsoft Dynamic, Marketo en Marketo Microsoft Dynamics Sync. Als u berichten wilt verzenden vanuit Marketo, moet u eerst een Marketo SMS-beheerfunctie aanschaffen of configureren. Deze analyse gebruikt [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), maar er zijn andere Marketo SMS-oplossingen beschikbaar.

## Vereisten

1. Installeer de Marketo Microsoft Dynamics Sync.

   Informatie en de nieuwste insteekmodule voor Microsoft Dynamics Sync zijn beschikbaar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installeer Acrobat Sign for Microsoft Dynamics.

   Informatie over deze plug-in is beschikbaar [hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Microsoft Dynamics Sync en Acrobat Sign for Dynamics zijn geconfigureerd, verschijnen er twee nieuwe opties in de Marketo Admin Terminal.

![Beheer](assets/adminTerminal.png)

* Klikken **[!UICONTROL Dynamics-entiteiten synchroniseren]**.

  Synchronisatie moet worden uitgeschakeld voordat u aangepaste entiteiten synchroniseert. Klikken **[!UICONTROL Schema synchroniseren]** als dit uw eerste keer is. Anders klikt u op **[!UICONTROL Schema vernieuwen]**.

  ![Vernieuwen](assets/refreshSchema.png)

## Het aangepaste object synchroniseren

1. Aan de rechterkant kunt u de [!UICONTROL Lead], [!UICONTROL Contact], en [!UICONTROL Account]op -gebaseerde aangepaste objecten.

   * **[!UICONTROL Synchronisatie inschakelen]** voor de objecten onder Lead als u wilt activeren wanneer een lead in Dynamics aan een overeenkomst wordt toegevoegd.

   * **[!UICONTROL Synchronisatie inschakelen]** voor de objecten onder Contactpersoon als u wilt activeren wanneer een Contactpersoon wordt toegevoegd aan een overeenkomst in Dynamics.

   * **[!UICONTROL Synchronisatie inschakelen]** voor de objecten onder Account als u wilt activeren wanneer een Account wordt toegevoegd aan een overeenkomst in Dynamics.

   * **Synchronisatie inschakelen** voor het overeenkomstobject onder de gewenste bovenliggende element (lead, contact of account).

   ![Aangepaste objecten](assets/enableSyncDynamics.png)

1. Selecteer in het nieuwe venster de eigenschappen die u onder Overeenkomst wilt gebruiken.

   De vakken inschakelen onder **[!UICONTROL Restrictie]** en **[!UICONTROL Trigger]** om ze beschikbaar te maken voor je marketingactiviteiten.

   ![Aangepaste synchronisatie 1](assets/entitySync1.png)

   ![Aangepaste synchronisatie 2](assets/entitySync2.png)

1. Activeer de synchronisatie opnieuw nadat u synchronisatie voor de aangepaste objecten hebt ingeschakeld.

   Ga terug naar de [!UICONTROL Admin Terminal]en klik vervolgens op **[!UICONTROL Microsoft Dynamics]** en klik vervolgens op **[!UICONTROL Synchronisatie inschakelen]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Algemeen inschakelen](assets/enableGlobalDynamics.png)

## Het programma maken

1. In [!UICONTROL Marketingactiviteiten], met de rechtermuisknop klikken **[!UICONTROL Marketingactiviteiten]** op de linkerbalk selecteert u **[!UICONTROL Nieuwe campagnemap]** en geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map en selecteer **[!UICONTROL Nieuw programma]** en geef deze een naam.

   Laat alle andere elementen standaard staan en klik op **[!UICONTROL Maken]**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

## Instellen [!DNL Twilio] SMS

Zorg er eerst voor dat u een actieve [!DNL Twilio] en hebt u de gewenste SMS-functies aangeschaft.

Marketo instellen - [!DNL Twilio] Voor SMS-webhook zijn drie [!DNL Twilio] parameters van uw account.

* Account SID
* Accounttoken
* Twilio-telefoonnummer

Haal deze parameters van uw account op en open nu uw Marketo-exemplaar.

1. Klikken **[!UICONTROL Beheerder]** rechtsboven.

   ![Beheer](assets/adminTab.png)

1. Klikken **[!UICONTROL Webhooks]** en klik vervolgens op **[!UICONTROL Nieuwe webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Voer een **[!UICONTROL Webhook-naam]** en **[!UICONTROL Beschrijving]**.

1. Voer de volgende URL in en vervang de URL `ACCOUNT_SID` en `AUTH_TOKEN` met uw [!DNL Twilio] referenties.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecteren **[!UICONTROL POST]** als uw type verzoek.

1. Voer het volgende in **Sjabloon** en zorg ervoor dat u `MY_TWILIO_NUMBER` met uw [!DNL Twilio] telefoonnummer en `YOUR_MESSAGE` met een bericht van uw keuze.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Stel de **[!UICONTROL Tokencodering aanvragen]** aan *Formulier/URL*.

1. Stel het reactietype in op *JSON* klik vervolgens op **[!UICONTROL Opslaan]**.

## Trigger voor slimme campagnes instellen

1. Klik in de sectie Marketingactiviteiten met de rechtermuisknop op het programma dat u hebt gemaakt en selecteer vervolgens **[!UICONTROL Nieuwe slimme campagne]**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef de naam op en klik vervolgens op **[!UICONTROL Maken]**.

   ![Slimme campagne 2](assets/smartCampaign3.png)

   Er zijn verschillende triggers beschikbaar voor gebruik in de Microsoft-map.

1. Klikken en slepen **[!UICONTROL Toegevoegd aan overeenkomst]** aan de **[!UICONTROL Slimme lijst]** en voeg vervolgens eventuele beperkingen toe die u voor de trigger wilt hebben.

   ![Toegevoegd aan overeenkomst](assets/addedToAgreementDynamics.png)

## De slimme-campagnestroom instellen

1. Klik op de knop **[!UICONTROL Stroom]** in de [!UICONTROL Slimme campagne].

   Zoek en sleep de **Bel webhook** Ga naar het canvas en selecteer de webhook die u in de vorige sectie hebt gemaakt.

   ![Bel webhook](assets/callWebhook.png)

1. Je SMS-meldingscampagne voor leads die aan een overeenkomst worden toegevoegd, is nu ingesteld.
>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Acrobat Sign voor Microsoft Dynamics en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) dat is gratis beschikbaar op Experience League !