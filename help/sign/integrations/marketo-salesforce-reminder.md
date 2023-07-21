---
title: Herinneringen verzenden met Acrobat Sign for Salesforce en Marketo Configuration Guide
description: Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: ad54f7afa78b0fbb31eccf455723a8890cb92355
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Herinneringen verzenden met Acrobat Sign for Salesforce en Marketo Configuration Guide

Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend. Deze integratie maakt gebruik van Acrobat Sign, Acrobat Sign voor Salesforce, Marketo en de Marketo- en Salesforce-synchronisatie.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   Informatie en de nieuwste insteekmodule voor Salesforce Sync zijn beschikbaar [hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installeer Acrobat Sign voor Salesforce.

   Informatie over deze plug-in is beschikbaar [hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce Sync en Acrobat Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![Beheer](assets/adminTab.png)

![Objectsynchronisatie](assets/salesforceAdmin.png)

1. Klikken **Schema synchroniseren** als dit uw eerste keer is. Anders klikt u op **Schema vernieuwen**.

   ![Vernieuwen](assets/refreshSchema1.png)

1. Als globale synchronisatie wordt uitgevoerd, schakelt u deze uit door op **Globale synchronisatie uitschakelen**.

   ![Uitschakelen](assets/disableGlobal.png)

1. Klikken **Schema vernieuwen**.

   ![Vernieuwen 2](assets/refreshSchema2.png)

## Het aangepaste object synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**Synchronisatie inschakelen** voor objecten onder Lead als u een herinnering wilt verzenden wanneer een lead geen overeenkomst in Salesforce heeft ondertekend.

**Synchronisatie inschakelen** voor de objecten onder Contact als u een herinnering wilt verzenden wanneer een contactpersoon geen overeenkomst heeft ondertekend in Salesforce.

**Synchronisatie inschakelen** voor de objecten onder Account als u een herinnering wilt verzenden wanneer een Account geen overeenkomst in Salesforce heeft ondertekend.

1. **Synchronisatie inschakelen** voor de **Overeenkomst** object weergegeven onder de gewenste bovenliggende element (lead, contact of account). Doe dit voor alle andere aangepaste objecten die u wilt synchroniseren.

   ![Object Overeenkomst](assets/agreementObject.png)

1. De volgende elementen laten zien hoe **Synchronisatie inschakelen**.

   ![Aangepaste synchronisatie 1](assets/customObjectSync1.png)

   ![Aangepaste synchronisatie 2](assets/customObjectSync2.png)

## De aangepaste objectvelden beschikbaar maken voor triggers

1. Terwijl de globale synchronisatie is gedeactiveerd, selecteert u het aangepaste overeenkomstobject waarvoor u synchronisatie hebt ingeschakeld, en **Zichtbare velden bewerken**.

1. Schakel het veld Overeenkomstnaam in de triggerkolom in om het veld beschikbaar te maken voor je Campaign Action Triggers. Controleer alle andere velden waarop u wilt filteren, en klik vervolgens op **Opslaan**.

   ![Zichtbare velden 1 bewerken](assets/editVisible1.png)

   ![Zichtbare velden 2 bewerken](assets/editVisible2.png)

1. Wanneer u klaar bent met het inschakelen van synchronisatie op de aangepaste objecten en het beschikbaar maken van de triggerwaarden, vergeet dan niet de synchronisatie opnieuw te activeren:

   ![Algemeen inschakelen](assets/enableGlobal.png)

## Het programma en de token maken

1. Klik in de sectie Marketingactiviteiten van Marketo met de rechtermuisknop op **Marketingactiviteiten** op de linkerbalk selecteert u **Nieuwe campagnemap** en geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map en selecteer **Nieuw programma** en geef deze een naam. Laat alle andere elementen standaard staan en klik op **Maken**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

1. Klik op **Mijn tokens** en sleep  **E-mailscript** naar het canvas.

   ![E-mailscript](assets/emailScript.png)

1. Geef het een naam, en klik dan op **Klik om te bewerken**.

   ![Naam en bewerking](assets/nameAndSave.png)

1. Uitbreiden **Aangepaste objecten** aan de rechterkant, en vervolgens de **Overeenkomst** -object. Zoek de overeenkomstnaam, de overeenkomststatus, de datum van ondertekening en de URL voor ondertekening naar het canvas en sleep deze.

1. Schrijf een snelheidsscript met deze tokens om de overeenkomst-URL weer te geven van een overeenkomst die een week lang niet is ondertekend. In het volgende voorbeeld wordt de huidige datum vergeleken met de verzonden datum:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. Klik op **Opslaan**.

## Maak een herinnering en voeg personalisatie toe

Voorbeelden van personalisatie zijn: de naam van de ondertekenaar, de naam van de overeenkomst, een koppeling naar de overeenkomst, enz.

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik op **Nieuw lokaal element** selecteert u vervolgens **E-mail**.

   ![Nieuwe e-mail](assets/createNewEmail.png)

1. Voer op het nieuwe tabblad een **Naam** en **Beschrijving** voor de e-mail en selecteer een sjabloon in de sjabloonkiezer. Klik op **Maken**.

   ![Sjabloonkiezer](assets/templatePicker.png)

1. Stel de **Van naam** en **Van adres**.

   ![E-mailherinnering](assets/reminderEmail.png)

1. Klik op de berichttekst om de Editor te activeren. Klik op de knop **Token invoegen** te zoeken naar het aangepaste URL-token voor de overeenkomst dat u hebt gemaakt, en vervolgens op **Invoegen**. Voltooi het aanpassen van uw e-mail en klik op **Opslaan**.

   ![Token invoegen](assets/insertToken.png)

1. Voorvertonen met een profiel waaraan een overeenkomst is toegewezen. Er wordt een koppeling naar de URL weergegeven met de overeenkomstnaam als label.

   ![E-mailkoppeling](assets/emailLink.png)

## Het filter Slimme campagne instellen

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik vervolgens op **Nieuwe slimme campagne**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef het een door u gekozen naam en klik vervolgens op **Maken**.

   ![Slimme campagne 2](assets/smartCampaign2.png)

1. Zoeken naar, vervolgens klikken en slepen **Heeft overeenkomst** naar de slimme lijst.

   ![Heeft overeenkomst](assets/hasAgreement.png)

1. De velden die u aan de trigger blootstelt, moeten nu beschikbaar zijn in **Restrictie toevoegen**. Selecteren **Overeenkomststatus** en andere velden waarop u wilt filteren. Definieer voor elk toegevoegd veld de waarden waarop u wilt filteren. In dit geval wordt het alleen geactiveerd wanneer de opdracht **Overeenkomststatus** is verzonden ter ondertekening en **Datum van verzending** is ouder dan 7 dagen.

   ![Overeenkomststatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d een unieke id voor de beperkingen, zoals **Naam overeenkomst**, als je wilt dat deze campagne alleen wordt uitgevoerd voor bepaalde overeenkomsten.

1. Bevestig het campagnepubliek en bekijk op het tabblad Planning wie hiervoor in aanmerking komt.

   ![Kwalificatoren](assets/qualifiers.png)

## De slimme-campagnestroom instellen

Omdat het campagnefilter **Dagen niet ondertekend** is gebruikt, kunt u een geplande herhaling voor de campagne gebruiken.

1. Klik op de knop **Stroom** in de slimme campagne. Zoek en sleep de **E-mail verzenden** ga naar het canvas en selecteer de herinnerings-e-mail die u in de vorige sectie hebt gemaakt.

   ![E-mail verzenden](assets/sendEmail.png)

1. Klik op de knop **Planning** in de slimme campagne. Zorg ervoor dat de flow van de campagne beperkt is tot één keer per persoon in de **Instellingen voor slimme campagnes**. Klik vervolgens op de knop **Herhaling plannen** tabblad.

   ![Tabblad Planning](assets/scheduleTab.png)

1. Stel de **Planning** voor Daily kiest u een startdag en -tijd en indien nodig een einddatum voor de campagne.

   ![Planningsinstellingen](assets/scheduleSettings.png)

>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Acrobat Sign voor Salesforce en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) dat is gratis beschikbaar op Experience League !
