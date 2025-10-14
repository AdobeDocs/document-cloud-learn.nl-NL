---
title: Herinneringen verzenden met Acrobat Sign voor Microsoft Dynamics 365 en Marketo
description: Leer hoe u een e-mailherinnering kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Herinneringen verzenden met Acrobat Sign voor Microsoft Dynamics 365 en Marketo

Leer hoe u een e-mailherinnering kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend. Deze integratie maakt gebruik van Acrobat Sign, Acrobat Sign voor Microsoft Dynamics, Marketo en de Marketo Microsoft Dynamics Sync.

## Vereisten

1. Installeer de Marketo Microsoft Dynamics Sync.

   De informatie en de recentste stop in voor de Synchronisatie van de Dynamiek van Microsoft zijn beschikbaar [&#x200B; hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html?lang=nl-NL)

1. Installeer [&#x200B; Acrobat Sign voor de Dynamica van Microsoft &#x200B;](https://appsource.microsoft.com/nl-nl/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   De informatie over deze stop is beschikbaar [&#x200B; hier.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Microsoft Dynamics Sync en Acrobat Sign for Dynamics zijn geconfigureerd, verschijnen er twee nieuwe opties in de Marketo Admin Terminal.

![&#x200B; Admin &#x200B;](assets/adminTerminal.png)

1. Klik **[!UICONTROL de Synchronisatie van de Entiteiten van de Dynamics]**.

   Synchronisatie moet worden uitgeschakeld voordat u aangepaste entiteiten synchroniseert. Klik **Schema van de Synchronisatie** als dit uw eerste keer is. Anders, verfrist de klik **Schema**.

   ![&#x200B; verfrissen zich &#x200B;](assets/refreshSchema.png)

## Het aangepaste object synchroniseren

1. Op de rechterkant, bepaal de plaats van [!UICONTROL &#x200B; Lead &#x200B;], [!UICONTROL &#x200B; Contact &#x200B;], en [!UICONTROL &#x200B; rekening &#x200B;] - gebaseerde douanevoorwerpen.

   * **laat Synchronisatie** voor de voorwerpen onder **[!UICONTROL leiden]** toe als u een herinnering wilt verzenden wanneer a [!UICONTROL &#x200B; leiden &#x200B;] geen overeenkomst in Dynamiek heeft ondertekend.

   * **laat Synchronisatie** voor de voorwerpen onder **[!UICONTROL Contact]** toe als u een herinnering wilt verzenden wanneer het a [!UICONTROL &#x200B; Contact &#x200B;] geen overeenkomst in Dynamics heeft ondertekend.

   * **laat Synchronisatie** voor de voorwerpen onder **[!UICONTROL Rekening]** toe als u een herinnering wilt verzenden wanneer een [!UICONTROL &#x200B; Rekening &#x200B;] geen overeenkomst in Dynamics heeft ondertekend.

   * **laat Synchronisatie** voor het overeenkomstvoorwerp onder de gewenste **[!UICONTROL Ouder]** toe ([!UICONTROL &#x200B; Lood &#x200B;], [!UICONTROL &#x200B; Contact &#x200B;], of [!UICONTROL &#x200B; Rekening &#x200B;]).

   ![&#x200B; de Objecten van de Douane &#x200B;](assets/enableSyncDynamics.png)

1. In het nieuwe venster, selecteer de eigenschappen u onder Overeenkomst wilt, dan toelaten de dozen onder **Beperking** en **Trekker** om hen aan uw Activiteiten van de Marketing bloot te stellen.

   ![&#x200B; Synchronisatie van de Douane 1 &#x200B;](assets/entitySync1.png)

   ![&#x200B; Synchronisatie van de Douane 2 &#x200B;](assets/entitySync2.png)

1. Activeer de synchronisatie opnieuw nadat u synchronisatie voor de aangepaste objecten hebt ingeschakeld.

   Ga terug naar de Terminal Admin, klik **Dynamiek van Microsoft**, dan klik op **toelaten Synchronisatie**.

   ![&#x200B; Dynamica van Microsoft &#x200B;](assets/microsoftDynamics.png)

   ![&#x200B; laat Globale &#x200B;](assets/enableGlobalDynamics.png) toe

## Het programma en de token maken

1. In de sectie van de Activiteiten van de Marketing van Marketo, klik op **Activiteiten van de Marketing** op de linkerbar met de rechtermuisknop aan.

   Selecteer **Nieuwe Omslag van de Campagne**, en geef het een naam.

   ![&#x200B; Nieuwe Omslag &#x200B;](assets/newFolder.png)

1. Klik op de gecreeerde omslag met de rechtermuisknop aan, selecteer **Nieuw Programma**, en geef het een naam.

   Laat alles anders als gebrek, dan klik **creëren**.

   ![&#x200B; Nieuw Programma 1 &#x200B;](assets/newProgram1.png)

   ![&#x200B; Nieuw Programma 2 &#x200B;](assets/newProgram2.png)

1. Klik op **Mijn Tokens**, dan sleep **E-mailManuscript** over aan het canvas.

   ![&#x200B; E-mailManuscript &#x200B;](assets/emailScript.png)

1. Geef het een naam, dan klik op **klik om uit te geven**.

   ![&#x200B; Naam en geef &#x200B;](assets/nameAndSave.png) uit

1. Breid **[!UICONTROL de Objecten van de Douane]** op de rechterkant uit, dan breid het **[!UICONTROL voorwerp van de Overeenkomst]** uit.

   Vind en sleep [!UICONTROL &#x200B; Naam &#x200B;], de Status van de Overeenkomst, Verzonden op, en Huidige URL van de Ondertekenaar op het canvas.

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

Voorbeelden van personalisatie zijn: de naam van de ondertekenaar, de naam van de overeenkomst, een koppeling naar de overeenkomst, enzovoort.

1. Klik op het programma met de rechtermuisknop u creeerde en klik **[!UICONTROL Nieuwe Lokale Activa]**, dan uitgezocht **[!UICONTROL E-mail]**.

   ![&#x200B; Nieuwe E-mail &#x200B;](assets/createNewEmail.png)

1. In het nieuwe lusje, ga a **[!UICONTROL Naam]** en **[!UICONTROL Beschrijving]** voor e-mail in en selecteer een malplaatje van de malplaatjeplukker.

   ![&#x200B; de Plukker van het Malplaatje &#x200B;](assets/templatePicker.png)

1. Klik op **[!UICONTROL Maken]**.

1. Plaats **[!UICONTROL van Naam]** en **[!UICONTROL van Adres]**.

   ![&#x200B; E-mail van de Herinnering &#x200B;](assets/reminderEmail.png)

1. Klik op de berichttekst om de Editor te activeren.

   Klik op het **[!UICONTROL Symbolische]** knoop van het Tussenvoegsel, vind het symbolische van de douaneOvereenkomst URL u creeerde, dan klik **[!UICONTROL Tussenvoegsel]**. Voltooi het aanpassen van uw e-mail, en klik **[!UICONTROL sparen]**.

   ![&#x200B; Symbolisch van het Tussenvoegsel &#x200B;](assets/insertToken.png)

1. Voorvertonen met een profiel waaraan een overeenkomst is toegewezen.

   Er wordt een koppeling naar de URL weergegeven met de overeenkomstnaam als label.

   ![&#x200B; E-mailverbinding &#x200B;](assets/emailLink.png)

## Het filter Slimme campagne instellen

1. Klik op het programma met de rechtermuisknop u creeerde, dan klik **[!UICONTROL Nieuwe Slimme Campagne]**.

   ![&#x200B; Slimme Campaign 1 &#x200B;](assets/smartCampaign1.png)

1. Geef het een naam van uw het kiezen, dan klik **[!UICONTROL creeer]**.

   ![&#x200B; Slimme Campaign 2 &#x200B;](assets/smartCampaign2.png)

1. Het onderzoek naar, dan klikt en sleept **[!UICONTROL heeft Overeenkomst]** aan de Slimme Lijst.

   ![&#x200B; heeft overeenkomst &#x200B;](assets/hasAgreementDynamics1.png)

   De gebieden u aan de trekker blootstelde zouden in **[!UICONTROL moeten beschikbaar zijn voeg Beperking]** toe.

1. Selecteer **[!UICONTROL Status van de Overeenkomst]** en om het even welke andere gebieden u wilt filtreren door.

   Definieer voor elk toegevoegd veld de waarden waarop u wilt filteren. In dit geval, brengt het slechts teweeg wanneer de **[!UICONTROL Status van de Overeenkomst]** *uit voor Ondertekening* is en **[!UICONTROL Verzonden op]** is *in het verleden vóór 1 week*.

   ![&#x200B; Status van de Overeenkomst &#x200B;](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Voeg een uniek herkenningsteken aan de beperkingen, zoals **Naam** toe, als u deze campagne voor bepaalde overeenkomsten slechts wilt lopen.

1. Bevestig het campagnepubliek en bekijk op het tabblad Planning wie hiervoor in aanmerking komt.

   ![&#x200B; Kwalificatoren &#x200B;](assets/qualifiers.png)

## De slimme-campagnestroom instellen

Omdat de campagnefilter **Dagen tot Verloopt** werd gebruikt, kunt u een geplande herhaling voor de campagne gebruiken.

1. Klik het **[!UICONTROL lusje van de Stroom]** in de [!UICONTROL &#x200B; Slimme Campagne &#x200B;].

   Zoek naar en sleep **verzendt e-mail** stroom naar het canvas en selecteer de herinnerings e-mail u in de vorige sectie creeerde.

   ![&#x200B; verzend e-mail &#x200B;](assets/sendEmail.png)

1. Klik het **[!UICONTROL lusje van het Programma]** in de Slimme Campagne. Zorg ervoor dat de campagnestroom wordt beperkt tot slechts eenmaal per persoon in de **Slimme Montages van de Campagne**. Dan, klik op de **Terugkeer van het Programma** tabel.

   ![&#x200B; het Lusje van het Programma &#x200B;](assets/scheduleTab.png)

1. Plaats het **Programma** aan _Dagelijkse_. Kies zo nodig een startdag en een tijd en einddatum voor de campagne.

   ![&#x200B; Montages van het Plan &#x200B;](assets/scheduleSettings.png)
