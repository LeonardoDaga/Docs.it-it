---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Preimpostazione delle voci di elenco con CascadingDropDown (VB) del | Microsoft Docs
author: wenz
description: Il controllo CascadingDropDown in AJAX Control Toolkit estende un controllo DropDownList in modo che le modifiche in un controllo DropDownList carichi associati i valori in anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 3816ce9d5b148ec9c18eef64d963c4465c219674
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823949"
---
<a name="presetting-list-entries-with-cascadingdropdown-vb"></a>Preimpostazione delle voci dell'elenco con CascadingDropDown (VB)
====================
da [Christian Wenz](https://github.com/wenz)

[Scaricare il codice](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) o [Scarica il PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> Il controllo CascadingDropDown in AJAX Control Toolkit estende un controllo DropDownList in modo che le modifiche in un controllo DropDownList Carica valori in un altro controllo DropDownList associati. Con un po' di codice è possibile che un elemento di elenco è preselezionata l'opzione quando i dati sono stati caricati in modo dinamico.


## <a name="overview"></a>Panoramica

Il controllo CascadingDropDown in AJAX Control Toolkit estende un controllo DropDownList in modo che le modifiche in un controllo DropDownList Carica valori in un altro controllo DropDownList associati. (Ad esempio, un unico elenco fornisce un elenco di stati degli Stati Uniti e il successivo elenco viene riempito con città più importanti di tale stato.) Con un po' di codice è possibile che un elemento di elenco è preselezionata l'opzione quando i dati sono stati caricati in modo dinamico.

## <a name="steps"></a>Passaggi

Per attivare la funzionalità di ASP.NET AJAX e il Toolkit di controllo, il `ScriptManager` controllo deve essere inserito in un punto qualsiasi della pagina (ma entro la `<form>` elemento):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

Quindi, è necessario un controllo DropDownList:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

Per questo elenco, viene aggiunto un controllo extender CascadingDropDown, che fornisce informazioni di URL e il metodo di servizio web:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

Il dispositivo extender CascadingDropDown chiama quindi in modo asincrono un servizio web con la firma del metodo seguente:

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

Il metodo restituisce una matrice di tipo valore CascadingDropDown. Il costruttore del tipo prevede innanzitutto la didascalia della voce di elenco e quindi il valore (HTML `value` attributo). Se il terzo argomento è impostato su true, l'elenco viene automaticamente selezionato nel browser.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

Il caricamento della pagina nel browser riempirà l'elenco a discesa con i fornitori di tre, il secondo viene preselezionato.


[![L'elenco viene compilato e preselezionata automaticamente](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

L'elenco viene compilato e preselezionata automaticamente ([fare clic per visualizzare l'immagine con dimensioni normali](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Precedente](using-cascadingdropdown-with-a-database-vb.md)
> [Successivo](using-auto-postback-with-cascadingdropdown-vb.md)
