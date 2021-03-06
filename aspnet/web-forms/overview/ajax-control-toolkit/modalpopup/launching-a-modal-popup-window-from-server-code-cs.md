---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Avviando una finestra Popup modale dal codice Server (c#) | Documenti Microsoft
author: wenz
description: Il controllo ModalPopup AJAX Control Toolkit offre un modo semplice per creare un popup modale tramite mezzi sul lato client. Tuttavia, alcuni scenari richiedono che t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: cc2ccf8153de4f2633cc46ebbee2da199ba9d06e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
<a name="launching-a-modal-popup-window-from-server-code-c"></a>Avviando una finestra Popup modale dal codice Server (c#)
====================
da [Christian Wenz](https://github.com/wenz)

[Scaricare codice](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) o [Scarica il PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> Il controllo ModalPopup AJAX Control Toolkit offre un modo semplice per creare un popup modale tramite mezzi sul lato client. Tuttavia alcuni scenari richiedono che l'apertura della finestra popup modale viene attivata sul lato server.


## <a name="overview"></a>Panoramica

Il controllo ModalPopup AJAX Control Toolkit offre un modo semplice per creare un popup modale tramite mezzi sul lato client. Tuttavia alcuni scenari richiedono che l'apertura della finestra popup modale viene attivata sul lato server.

## <a name="steps"></a>Passaggi

Controllo pulsante di ASP.NET web prima di tutto, è necessario per illustrare il funzionamento di controllo ModalPopup. Aggiungere questi pulsanti all'interno di &lt;modulo&gt; elemento in una nuova pagina:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

Quindi, è necessario il markup per il popup in cui che si desidera creare. Come definire un `<asp:Panel>` controllo e assicurarsi che include un controllo pulsante. Il controllo ModalPopup offre le funzionalità per rendere tali un pulsante per chiudere la finestra popup; in caso contrario non è facile per lasciare scompaiono.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

Aggiungere il controllo ModalPopup di ASP.NET AJAX Toolkit alla pagina. Impostare le proprietà per il pulsante che consente di caricare il controllo pulsante che rende scompaiono e l'ID del popup effettivo.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

Come con tutte le pagine web basate su ASP.NET AJAX; il gestore di Script è necessaria per caricare le librerie JavaScript necessari per i browser di destinazione diverso:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

Eseguire l'esempio nel browser. Quando si fa clic sul pulsante, viene visualizzata il finestra popup modale. Per ottenere lo stesso effetto utilizzando codice lato server, è necessario un nuovo pulsante:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

Come si può notare, un clic sul pulsante genera un postback ed esegue il `ServerButton_Click()` metodo sul server. In questo metodo, è stata chiamata una funzione JavaScript `launchModal()` viene eseguita per essere esatto, la funzione JavaScript verrà eseguita dopo che è stata caricata la pagina:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

Il processo di `launchModal()` viene visualizzato il ModalPopup. Il `launchModal()` funzione viene eseguita una volta caricata nella pagina HTML. In quel momento, tuttavia, il framework ASP.NET AJAX non è stato caricato completamente ancora. Pertanto, il `launchModal()` funzione si limita a impostare una variabile che il controllo ModalPopup deve essere visualizzato in un secondo momento:

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

Il `pageLoad()` JavaScript è una funzione speciale che viene eseguita una volta ASP.NET AJAX è stato caricato completamente. Pertanto è aggiungere il codice a questa funzione per visualizzare il controllo ModalPopup, ma solo se `launchModal()` è stato chiamato prima di:

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

Il `$find()` funzione esegue la ricerca di un elemento denominato nella pagina e non prevede l'ID lato server come parametro. Pertanto, `$find("mpe")` restituisce la rappresentazione di client del controllo ModalPopup; relativo `show()` metodo consente la finestra popup visualizzata.


[![Il popup modale viene visualizzato quando si fa clic su uno dei pulsanti](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

Il popup modale viene visualizzato quando si fa clic su uno dei pulsanti ([fare clic per visualizzare l'immagine ingrandita](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))

>[!div class="step-by-step"]
[Successivo](using-modalpopup-with-a-repeater-control-cs.md)
