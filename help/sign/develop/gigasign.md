---
title: Hoog volume documenten verzamelen met GigaSign
description: Met Gigasign kun je documenten ter ondertekening verzenden, verzamelen en volgen aan duizenden mensen tegelijk
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: ba9931920ab3bfb6ea38a92cac4a35da1d0295cd
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Verzamel grote documenten met GigaSign

Met Gigasign kun je documenten ter ondertekening verzenden, verzamelen en volgen aan duizenden mensen tegelijk. Het wordt ontworpen voor hoog-volume communicatie met uw werknemers en klanten-ondersteunend tot 2.500 ontvangers met elke bulk verzendt. GigaSign gebruikt de Acrobat Sign API om dezelfde functionaliteit te bieden als MegaSign, en biedt ondersteuning voor meerdere ondertekenaars, groepen ontvangers, rollen van ontvangers, overeenkomstnamen, koolstofkopie en meer.

>[!IMPORTANT]
>
>GigaSign wordt niet meer bijgewerkt naar de nieuwste versie van Java of Acrobat Sign en biedt slechts beperkte ondersteuning. De functies van GigaSign worden toegevoegd aan het product onder de [In bulk verzenden](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?lang=nl-NL&) functionaliteit. Gebruik Verzenden in bulk voor alle gevallen waarin het gebruik van GigaSign niet expliciet is vereist.

>[!VIDEO](https://video.tv.adobe.com/v/3453516?quality=12&learn=on&hidetitle=true&captions=dut)

## Download en installeer de GigaSign-app

[GigaSign Zip-bestand downloaden](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Java 1.8-downloadkoppeling (alleen indien nodig)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html){target="_blank"} 

[IP-adressen naar witte lijst (alleen indien nodig)](https://helpx.adobe.com/nl/sign/system-requirements.html#IPs){target="_blank"}

## Basisinstallatie-instructies

1. Meld u aan bij uw Acrobat Sign-account.

1. Klikken **[!UICONTROL Groep]** of **[!UICONTROL Account]**, al wat je bovenaan ziet.

1. Typ &quot;Toegangstokens&quot; in het zoekveld links in het scherm.

1. Druk op het pictogram &quot;+&quot; aan de rechterkant.

1. Maak een sleutel met het vereiste bereik (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Dubbelklik op de sleutel die u hebt gemaakt en kopieer de VOLLEDIGE tekst (deze gaat van het scherm naar rechts, zodat u zeker weet dat u alles krijgt).

1. Open GigaSign.

1. Klik op de knop **[!UICONTROL Instellingen]** aan de rechterbovenhoek.

1. Plak de integratiesleutel in de eerste regel.

1. Voer in de tweede regel het e-mailadres in van het account waarmee de sleutel is gemaakt.

1. Klik op **[!UICONTROL Verzenden]**.
