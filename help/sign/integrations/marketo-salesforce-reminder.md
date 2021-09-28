---
title: Herinneringen verzenden met Adobe Sign for Salesforce en Marketo Configuration Guide
description: Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Herinneringen verzenden met Adobe Sign for Salesforce en Marketo Configuration Guide

Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend. Deze integratie maakt gebruik van Adobe Sign, Adobe Sign voor Salesforce, Marketo en de Marketo- en Salesforce-synchronisatie.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   [Hier is informatie en de nieuwste insteekmodule voor Salesforce Sync beschikbaar.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installeer Adobe Sign voor Salesforce.

   [Hier is informatie over deze plug-in beschikbaar.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce Sync en Adobe Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![Beheerder](assets/adminTab.png)

![Objectsynchronisatie](assets/salesforceAdmin.png)

1. Klik **Schema synchroniseren** als dit uw eerste keer is. Klik anders op **Schema vernieuwen**.

   ![Vernieuwen](assets/refreshSchema1.png)

1. Als globale synchronisatie wordt uitgevoerd, kunt u deze uitschakelen door te klikken op **Globale synchronisatie uitschakelen**.

   ![Uitschakelen](assets/disableGlobal.png)

1. Klik op **Schema vernieuwen**.

   ![Vernieuwen 2](assets/refreshSchema2.png)

## Het aangepaste object synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**Schakel** Synchroniseren voor de objecten onder Lead in als u een herinnering wilt verzenden wanneer een lead geen overeenkomst in Salesforce heeft ondertekend.

**Schakel** Synchroniseren voor de objecten onder Contactpersoon in als u een herinnering wilt verzenden wanneer een contactpersoon geen overeenkomst heeft ondertekend in Salesforce.

**Schakel** Synchroniseren voor de objecten onder Account in als u een herinnering wilt verzenden wanneer een Account geen overeenkomst in Salesforce heeft ondertekend.

1. **Schakel** Syncfor het  **** overeenkomstobject in dat wordt weergegeven onder de gewenste bovenliggende component (lead, contact of account). Doe dit voor alle andere aangepaste objecten die u wilt synchroniseren.

   ![Object Overeenkomst](assets/agreementObject.png)

1. De volgende elementen tonen hoe u **Sync inschakelen**.

   ![Aangepaste synchronisatie 1](assets/customObjectSync1.png)

   ![Aangepaste synchronisatie 2](assets/customObjectSync2.png)

## De aangepaste objectvelden beschikbaar maken voor triggers

1. Terwijl de globale synchronisatie is gedeactiveerd, selecteert u het aangepaste overeenkomstobject waarvoor u synchronisatie hebt ingeschakeld, en vervolgens **Zichtbare velden bewerken**.

1. Schakel het veld Overeenkomstnaam in de triggerkolom in om het veld beschikbaar te maken voor je Campaign Action Triggers. Controleer de andere velden waarop u wilt filteren, en **Save**.

   ![Zichtbare velden 1 bewerken](assets/editVisible1.png)

   ![Zichtbare velden 2 bewerken](assets/editVisible2.png)

1. Wanneer u klaar bent met het inschakelen van synchronisatie op de aangepaste objecten en het beschikbaar maken van de triggerwaarden, vergeet dan niet de synchronisatie opnieuw te activeren:

   ![Algemeen inschakelen](assets/enableGlobal.png)

## Het programma en de token maken

1. Klik in de sectie Marketingactiviteiten van Marketo met de rechtermuisknop op **Marketingactiviteiten** op de linkerbalk en selecteer **Nieuwe campagnemap**. Geef deze een naam.

   ![Nieuwe map](assets/newFolder.png)

1. Klik met de rechtermuisknop op de gemaakte map, selecteer **Nieuw programma** en geef deze een naam. Laat alle andere elementen standaard staan en klik op **Maken**.

   ![Nieuw programma 1](assets/newProgram1.png)

   ![Nieuw programma 2](assets/newProgram2.png)

1. Klik op **Mijn tokens** en sleep **E-mailscript** naar het canvas.

   ![E-mailscript](assets/emailScript.png)

1. Geef het een naam, dan klik op **Klik om uit te geven**.

   ![Naam en bewerking](assets/nameAndSave.png)

1. Vouw **Aangepaste objecten** aan de rechterkant uit en vouw vervolgens het object **Agreement** uit. Zoek de overeenkomstnaam, de overeenkomststatus, de datum van ondertekening en de URL voor ondertekening naar het canvas en sleep deze.

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

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik op **Nieuw lokaal element**. Selecteer vervolgens **E-mail**.

   ![Nieuwe e-mail](assets/createNewEmail.png)

1. Voer op het nieuwe tabblad een **Naam** en **Beschrijving** in voor de e-mail en selecteer een sjabloon in de sjabloonkiezer. Klik op **Maken**.

   ![Sjabloonkiezer](assets/templatePicker.png)

1. Stel de **Van naam** en **Van adres** in.

   ![E-mailherinnering](assets/reminderEmail.png)

1. Klik op de berichttekst om de Editor te activeren. Klik op de knop **Token invoegen**, zoek de aangepaste overeenkomst-URL-token die u hebt gemaakt en klik vervolgens op **Invoegen**. Voltooi het aanpassen van uw e-mail en klik op **Opslaan**.

   ![Token invoegen](assets/insertToken.png)

1. Voorvertonen met een profiel waaraan een overeenkomst is toegewezen. Er wordt een koppeling naar de URL weergegeven met de overeenkomstnaam als label.

   ![Koppeling e-mailen](assets/emailLink.png)

## Het filter Slimme campagne instellen

1. Klik met de rechtermuisknop op het programma dat u hebt gemaakt en klik vervolgens op **Nieuwe slimme campagne**.

   ![Slimme campagne 1](assets/smartCampaign1.png)

1. Geef het een naam van uw keuze en klik vervolgens op **Maken**.

   ![Slimme campagne 2](assets/smartCampaign2.png)

1. Zoek naar, klik en sleep **Heeft overeenkomst** naar de slimme lijst.

   ![Heeft overeenkomst](assets/hasAgreement.png)

1. De velden die beschikbaar zijn voor de trigger, moeten nu beschikbaar zijn in **Restrictie toevoegen**. Selecteer **Overeenkomststatus** en andere velden waarop u wilt filteren. Definieer voor elk toegevoegd veld de waarden waarop u wilt filteren. In dit geval wordt de gebeurtenis alleen geactiveerd wanneer de **Overeenkomststatus** is verzonden ter ondertekening en **Datum verzonden** zich in de afgelopen 7 dagen bevindt.

   ![Overeenkomststatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d een unieke id voor de beperkingen, zoals **Naam overeenkomst**, als u wilt dat deze campagne alleen voor bepaalde overeenkomsten wordt uitgevoerd.

1. Bevestig het campagnepubliek en bekijk op het tabblad Planning wie hiervoor in aanmerking komt.

   ![Kwalificatoren](assets/qualifiers.png)

## De slimme-campagnestroom instellen

Omdat het campagnefilter **Niet-ondertekende dagen** is gebruikt, kunt u een geplande herhaling voor de campagne gebruiken.

1. Klik op het tabblad **Flow** in de slimme campagne. Zoek en sleep de **E-mail verzenden** naar het canvas en selecteer de herinnering die u in de vorige sectie hebt gemaakt.

   ![E-mail verzenden](assets/sendEmail.png)

1. Klik op het tabblad **Planning** in de slimme campagne. Zorg ervoor dat de campagnestroom beperkt is tot één keer per persoon in de **Slimme campagne-instellingen**. Klik vervolgens op het tabblad **Herhaling plannen**.

   ![Tabblad Planning](assets/scheduleTab.png)

1. Stel de **Planning** in op Dagelijks, kies een startdag en -tijd en een einddatum voor de campagne indien nodig.

   ![Planningsinstellingen](assets/scheduleSettings.png)

>[!TIP]
>
>Deze zelfstudie maakt deel uit van de cursus [Versnel de verkoopcycli met Adobe Sign voor Salesforce en Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) die gratis beschikbaar is op Experience League!
