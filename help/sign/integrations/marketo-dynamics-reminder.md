---
title: Herinneringen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo
description: Leer hoe u een e-mailherinnering kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Herinneringen verzenden met Acrobat Sign for Microsoft Dynamics 365 en Marketo

Leer hoe u een e-mailherinnering kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend. Deze integratie maakt gebruik van Acrobat Sign, Acrobat Sign voor Microsoft Dynamics, Marketo en de Marketo Microsoft Dynamics Sync.

## Vereisten

1. Installeer de Marketo Microsoft Dynamics Sync.

   Informatie en de nieuwste insteekmodule voor Microsoft Dynamics Sync zijn beschikbaar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installeren [Acrobat Sign voor Microsoft Dynamics](https://appsource.microsoft.com/nl-nl/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Informatie over deze plug-in is beschikbaar [hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Microsoft Dynamics Sync en Acrobat Sign for Dynamics zijn geconfigureerd, verschijnen er twee nieuwe opties in de Marketo Admin Terminal.

![Beheer](assets/adminTerminal.png)

1. Klikken **[!UICONTROL Dynamics-entiteiten synchroniseren]**.

   Synchronisatie moet worden uitgeschakeld voordat u aangepaste entiteiten synchroniseert. Klikken **Schema synchroniseren** als dit uw eerste keer is. Anders klikt u op **Schema vernieuwen**.

   ![Vernieuwen](assets/refreshSchema.png)

## Het aangepaste object synchroniseren

1. Aan de rechterkant kunt u de [!UICONTROL Lead], [!UICONTROL Contact], en [!UICONTROL Account]op -gebaseerde aangepaste objecten.

   * **Synchronisatie inschakelen** voor de objecten onder **[!UICONTROL Lead]** als u een herinnering wilt verzenden wanneer een [!UICONTROL Lead] heeft geen overeenkomst ondertekend in Dynamics.

   * **Synchronisatie inschakelen** voor de objecten onder **[!UICONTROL Contact]** als u een herinnering wilt verzenden wanneer een [!UICONTROL Contact] heeft geen overeenkomst ondertekend in Dynamics.

   * **Synchronisatie inschakelen** voor de objecten onder **[!UICONTROL Account]** als u een herinnering wilt verzenden wanneer een [!UICONTROL Account] heeft geen overeenkomst ondertekend in Dynamics.

   * **Synchronisatie inschakelen** voor het overeenkomstobject onder de gewenste **[!UICONTROL Bovenliggend]** ([!UICONTROL Lead], [!UICONTROL Contact], of [!UICONTROL Account]).

   ![Aangepaste objecten](assets/enableSyncDynamics.png)

1. Selecteer in het nieuwe venster de eigenschappen die u onder Overeenkomst wilt gebruiken en schakel vervolgens de vakken onder **Restrictie** en **Trigger** om ze beschikbaar te maken voor je marketingactiviteiten.

   ![Aangepaste synchronisatie 1](assets/entitySync1.png)

   ![Aangepaste synchronisatie 2](assets/entitySync2.png)

1. Activeer de synchronisatie opnieuw nadat u synchronisatie voor de aangepaste objecten hebt ingeschakeld.

   Ga terug naar de beheerterminal en klik op **Microsoft Dynamics** en klik op **Synchronisatie inschakelen**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Algemeen inschakelen](assets/enableGlobalDynamics.png)

## Het programma en de token maken

1. Klik in de sectie Marketingactiviteiten van Marketo met de rechtermuisknop op **Marketingactiviteiten** op de linkerbalk.

   Selecteren **Nieuwe campagnemap** en geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map en selecteer **Nieuw programma** en geef deze een naam.

   Laat alle andere elementen standaard staan en klik op **Maken**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

1. Klik op **Mijn tokens** en sleep **E-mailscript** naar het canvas.

   ![E-mailscript](assets/emailScript.png)

1. Geef het een naam, en klik dan op **Klik om te bewerken**.

   ![Naam en bewerking](assets/nameAndSave.png)

1. Uitbreiden **[!UICONTROL Aangepaste objecten]** aan de rechterkant, en vervolgens de **[!UICONTROL Overeenkomst]** -object.

   Zoeken en slepen [!UICONTROL Naam], Overeenkomststatus, Verzonden op en Huidige URL ondertekenaar op het canvas.

1. Schrijf een snelheidsscript met deze tokens om de overeenkomst-URL weer te geven van een overeenkomst die een week lang niet is ondertekend. Hier volgt een voorbeeld van de huidige datum die wordt vergeleken met Verzonden op:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Klik op **[!UICONTROL Opslaan]**.

## Maak een herinnering en voeg personalisatie toe

Voorbeelden van personalisatie zijn: de naam van de ondertekenaar, de naam van de overeenkomst, een koppeling naar de overeenkomst, enz.

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik op **[!UICONTROL Nieuw lokaal element]** selecteert u vervolgens **[!UICONTROL E-mail]**.

   ![Nieuwe e-mail](assets/createNewEmail.png)

1. Voer op het nieuwe tabblad een **[!UICONTROL Naam]** en **[!UICONTROL Beschrijving]** voor de e-mail en selecteer een sjabloon in de sjabloonkiezer.

   ![Sjabloonkiezer](assets/templatePicker.png)

1. Klik op **[!UICONTROL Maken]**.

1. Stel de **[!UICONTROL Van naam]** en **[!UICONTROL Van adres]**.

   ![E-mailherinnering](assets/reminderEmail.png)

1. Klik op de berichttekst om de Editor te activeren.

   Klik op de knop **[!UICONTROL Token invoegen]** te zoeken naar het aangepaste URL-token voor de overeenkomst dat u hebt gemaakt, en vervolgens op **[!UICONTROL Invoegen]**. Voltooi het aanpassen van uw e-mail en klik op **[!UICONTROL Opslaan]**.

   ![Token invoegen](assets/insertToken.png)

1. Voorvertonen met een profiel waaraan een overeenkomst is toegewezen.

   Er wordt een koppeling naar de URL weergegeven met de overeenkomstnaam als label.

   ![E-mailkoppeling](assets/emailLink.png)

## Het filter Slimme campagne instellen

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik vervolgens op **[!UICONTROL Nieuwe slimme campagne]**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef het een door u gekozen naam en klik vervolgens op **[!UICONTROL Maken]**.

   ![Slimme campagne 2](assets/smartCampaign2.png)

1. Zoeken naar, vervolgens klikken en slepen **[!UICONTROL Heeft overeenkomst]** naar de slimme lijst.

   ![Heeft overeenkomst](assets/hasAgreementDynamics1.png)

   De velden die u aan de trigger blootstelt, moeten beschikbaar zijn in **[!UICONTROL Restrictie toevoegen]**.

1. Selecteren **[!UICONTROL Overeenkomststatus]** en andere velden waarop u wilt filteren.

   Definieer voor elk toegevoegd veld de waarden waarop u wilt filteren. In dit geval wordt alleen getriggerd wanneer de **[!UICONTROL Overeenkomststatus]** is *Verzonden voor ondertekening* en **[!UICONTROL Verzonden op]** is *in het verleden vóór 1 week*.

   ![Overeenkomststatus](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Voeg een unieke id toe aan de beperkingen, zoals **Naam**, als je wilt dat deze campagne alleen wordt uitgevoerd voor bepaalde overeenkomsten.

1. Bevestig het campagnepubliek en bekijk op het tabblad Planning wie hiervoor in aanmerking komt.

   ![Kwalificatoren](assets/qualifiers.png)

## De slimme-campagnestroom instellen

Omdat het campagnefilter **Dagen tot vervaldatum** is gebruikt, kunt u een geplande herhaling voor de campagne gebruiken.

1. Klik op **[!UICONTROL Stroom]** in de [!UICONTROL Slimme campagne].

   Zoek en sleep de **E-mail verzenden** ga naar het canvas en selecteer de herinnerings-e-mail die u in de vorige sectie hebt gemaakt.

   ![E-mail verzenden](assets/sendEmail.png)

1. Klik op **[!UICONTROL Planning]** in de slimme campagne. Zorg ervoor dat de flow van de campagne beperkt is tot één keer per persoon in de **Instellingen voor slimme campagnes**. Klik vervolgens op de knop **Herhaling plannen** tabblad.

   ![Tabblad Planning](assets/scheduleTab.png)

1. Stel de **Planning** aan _Dagelijks_. Kies zo nodig een startdag en een tijd en einddatum voor de campagne.

   ![Planningsinstellingen](assets/scheduleSettings.png)

>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Acrobat Sign voor Microsoft Dynamics en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) dat is gratis beschikbaar op Experience League !