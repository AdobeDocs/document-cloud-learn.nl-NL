---
title: Herinneringen verzenden met Acrobat Sign for Salesforce en Marketo Configuration Guide
description: Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Herinneringen verzenden met Acrobat Sign for Salesforce en Marketo Configuration Guide

Leer hoe u een e-mailherinnering van Marketo kunt verzenden als een overeenkomst na een bepaalde periode niet is ondertekend. Deze integratie maakt gebruik van Acrobat Sign, Acrobat Sign voor Salesforce, Marketo en de Marketo- en Salesforce-synchronisatie.

## Vereisten

1. Installeer de Marketo Salesforce-synchronisatie.

   De informatie en de recentste stop in voor de Synchronisatie van Salesforce zijn beschikbaar [&#x200B; hier.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html?lang=nl-NL)

1. Installeer Acrobat Sign voor Salesforce.

   De informatie over deze stop is beschikbaar [&#x200B; hier.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Het aangepaste object zoeken

Als de Marketo Salesforce Sync en Acrobat Sign for Salesforce-configuraties zijn voltooid, verschijnen er verschillende nieuwe opties in de Marketo Admin Terminal.

![&#x200B; Admin &#x200B;](assets/adminTab.png)

![&#x200B; de Synchronisatie van Objecten &#x200B;](assets/salesforceAdmin.png)

1. Klik **Schema van de Synchronisatie** als dit uw eerste keer is. Anders, verfrist de klik **Schema**.

   ![&#x200B; verfrissen zich &#x200B;](assets/refreshSchema1.png)

1. Als de globale synchronisatie loopt, maak onbruikbaar door **Globale Synchronisatie** onbruikbaar te klikken.

   ![&#x200B; onbruikbaar maken &#x200B;](assets/disableGlobal.png)

1. Klik **vernieuwen Schema**.

   ![&#x200B; vernieuw 2 &#x200B;](assets/refreshSchema2.png)

## Het aangepaste object synchroniseren

Aan de rechterkant zie Aangepaste objecten voor leads, Contactpersoon en Account.

**laat Synchronisatie** voor de voorwerpen onder Lood toe als u een herinnering wilt verzenden wanneer een Lood geen overeenkomst in Salesforce heeft ondertekend.

**laat Synchronisatie** voor de voorwerpen onder Contact toe als u een herinnering wilt verzenden wanneer een Contact geen overeenkomst in Salesforce heeft ondertekend.

**laat Synchronisatie** voor de voorwerpen onder Rekening toe als u een herinnering wilt verzenden wanneer een Rekening geen overeenkomst in Salesforce heeft ondertekend.

1. **laat Synchronisatie** voor het **voorwerp van de Overeenkomst** toe dat onder de gewenste ouder (Lead, Contact, of Rekening) wordt getoond. Doe dit voor alle andere aangepaste objecten die u wilt synchroniseren.

   ![&#x200B; Object van de Overeenkomst &#x200B;](assets/agreementObject.png)

1. De volgende activa tonen hoe te **toelaten Synchronisatie**.

   ![&#x200B; Synchronisatie van de Douane 1 &#x200B;](assets/customObjectSync1.png)

   ![&#x200B; Synchronisatie van de Douane 2 &#x200B;](assets/customObjectSync2.png)

## De aangepaste objectvelden beschikbaar maken voor triggers

1. Terwijl de Globale Synchronisatie wordt gedeactiveerd, selecteer het voorwerp van de douane van de Overeenkomst u synchronisatie voor, dan **uitgezocht Zichtbare Gebieden** toeliet.

1. Schakel het veld Overeenkomstnaam in de triggerkolom in om het veld beschikbaar te maken voor je Campaign Action Triggers. Controleer om het even welke andere gebieden u wilt filteren door, dan **sparen**.

   ![&#x200B; geef Zichtbare Gebieden 1 &#x200B;](assets/editVisible1.png) uit

   ![&#x200B; geef Zichtbare Gebieden 2 &#x200B;](assets/editVisible2.png) uit

1. Wanneer u klaar bent met het inschakelen van synchronisatie op de aangepaste objecten en het beschikbaar maken van de triggerwaarden, vergeet dan niet de synchronisatie opnieuw te activeren:

   ![&#x200B; laat Globale &#x200B;](assets/enableGlobal.png) toe

## Het programma en de token maken

1. In de sectie van de Activiteiten van de Marketing van Marketo, klik op **Activiteiten van de Marketing** op de linkerbar met de rechtermuisknop aan, selecteer **Nieuwe Omslag van de Campagne**, en geef het een naam.

   ![&#x200B; Nieuwe Omslag &#x200B;](assets/newFolder.png)

1. Klik op de gecreeerde omslag met de rechtermuisknop aan, selecteer **Nieuw Programma**, en geef het een naam. Laat alles anders als gebrek, dan klik **creëren**.

   ![&#x200B; Nieuw Programma 1 &#x200B;](assets/newProgram1.png)

   ![&#x200B; Nieuw Programma 2 &#x200B;](assets/newProgram2.png)

1. Klik op **Mijn Tokens**, dan sleep **E-mailManuscript** over aan het canvas.

   ![&#x200B; E-mailManuscript &#x200B;](assets/emailScript.png)

1. Geef het een naam, dan klik op **klik om uit te geven**.

   ![&#x200B; Naam en geef &#x200B;](assets/nameAndSave.png) uit

1. Breid **de Objecten van de Douane** op de rechterkant uit, dan breid het **voorwerp van de Overeenkomst** uit. Zoek de overeenkomstnaam, de overeenkomststatus, de datum van ondertekening en de URL voor ondertekening naar het canvas en sleep deze.

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

Voorbeelden van personalisatie zijn: de naam van de ondertekenaar, de naam van de overeenkomst, een koppeling naar de overeenkomst, enzovoort.

1. Klik op het programma met de rechtermuisknop u creeerde en klik **Nieuwe Lokale Activa**, dan uitgezocht **E-mail**.

   ![&#x200B; Nieuwe E-mail &#x200B;](assets/createNewEmail.png)

1. In het nieuwe lusje, ga a **Naam** en **Beschrijving** voor e-mail in en selecteer een malplaatje van de malplaatjeplukker. Klik op **Maken**.

   ![&#x200B; de Plukker van het Malplaatje &#x200B;](assets/templatePicker.png)

1. Plaats **van Naam** en **van Adres**.

   ![&#x200B; E-mail van de Herinnering &#x200B;](assets/reminderEmail.png)

1. Klik op de berichttekst om de Editor te activeren. Klik op het **Symbolische** knoop van het Tussenvoegsel, vind het symbolische van de douaneOvereenkomst URL u creeerde, dan klik **Tussenvoegsel**. Voltooi het aanpassen van uw e-mail, en klik **sparen**.

   ![&#x200B; Symbolisch van het Tussenvoegsel &#x200B;](assets/insertToken.png)

1. Voorvertonen met een profiel waaraan een overeenkomst is toegewezen. Er wordt een koppeling naar de URL weergegeven met de overeenkomstnaam als label.

   ![&#x200B; E-mailverbinding &#x200B;](assets/emailLink.png)

## Het filter Slimme campagne instellen

1. Klik op het programma met de rechtermuisknop u creeerde, dan klik **Nieuwe Slimme Campagne**.

   ![&#x200B; Slimme Campaign 1 &#x200B;](assets/smartCampaign1.png)

1. Geef het een naam van uw het kiezen, dan klik **creeer**.

   ![&#x200B; Slimme Campaign 2 &#x200B;](assets/smartCampaign2.png)

1. Het onderzoek naar, dan klikt en sleept **heeft Overeenkomst** aan de Slimme Lijst.

   ![&#x200B; heeft overeenkomst &#x200B;](assets/hasAgreement.png)

1. De gebieden u aan de trekker blootstelde zouden nu beschikbaar moeten zijn in **Add Restrictie**. Selecteer **Status van de Overeenkomst** en om het even welke andere gebieden u wilt filtreren door. Definieer voor elk toegevoegd veld de waarden waarop u wilt filteren. In dit geval, zal het slechts teweegbrengen wanneer de **Status van de Overeenkomst** uit voor Ondertekening is en **Verzonden Datum** is in het verleden vóór 7 dagen.

   ![&#x200B; Status van de Overeenkomst &#x200B;](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d een uniek herkenningsteken aan de beperkingen, zoals **Naam van de Overeenkomst**, als u deze campagne voor bepaalde overeenkomsten slechts wilt lopen.

1. Bevestig het campagnepubliek en bekijk op het tabblad Planning wie hiervoor in aanmerking komt.

   ![&#x200B; Kwalificatoren &#x200B;](assets/qualifiers.png)

## De slimme-campagnestroom instellen

Omdat het campagnefilter **Niet ondertekende Dagen** werd gebruikt, kunt u een geplande herhaling voor de campagne gebruiken.

1. Klik op het **Stroom** lusje in de Slimme Campagne. Zoek naar en sleep **verzendt e-mail** stroom naar het canvas en selecteer de herinnerings e-mail u in de vorige sectie creeerde.

   ![&#x200B; verzend e-mail &#x200B;](assets/sendEmail.png)

1. Klik op het **lusje van het Programma** in de Slimme Campagne. Zorg ervoor dat de campagnestroom wordt beperkt tot slechts eenmaal per persoon in de **Slimme Montages van de Campagne**. Dan, klik op de **Terugkeer van het Programma** tabel.

   ![&#x200B; het Lusje van het Programma &#x200B;](assets/scheduleTab.png)

1. Plaats het **Programma** aan Dagelijks, kies een begindag en tijd, en een einddatum voor de campagne indien nodig.

   ![&#x200B; Montages van het Plan &#x200B;](assets/scheduleSettings.png)

