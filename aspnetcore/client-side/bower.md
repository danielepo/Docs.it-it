---
title: Usando Bower in ASP.NET Core
author: rick-anderson
description: La gestione dei pacchetti sul lato client con Bower.
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/bower
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e3e936c81126b7ed01332565f997910a2886993
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2018
---
# <a name="manage-client-side-packages-with-bower-in-aspnet-core"></a>Gestire i pacchetti sul lato client con Bower in ASP.NET Core

Da [Rick Anderson](https://twitter.com/RickAndMSFT), [riso Noel](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), e [Scott Addie](https://scottaddie.com) 

> [!IMPORTANT]
> Mentre viene mantenuto Bower, si consiglia di utilizzare una soluzione diversa. Yarn con Webpack è una diffusa alternativa per il quale [istruzioni relative alla migrazione](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) sono disponibili.

[Bower](https://bower.io/) chiama se stessa "Gestione pacchetti per il web". All'interno dell'ecosistema di .NET, questa si riempie il vuoto lasciato dall'impossibilità di NuGet per recapitare i file di contenuto statico. Per i progetti ASP.NET Core, i file statici vengono svolte da librerie sul lato client come [jQuery](http://jquery.com/) e [Bootstrap](http://getbootstrap.com/). Per le librerie .NET, è comunque usare [NuGet](https://www.nuget.org/) Gestione pacchetti.

Processo di compilazione di nuovi progetti creati con i modelli di progetto ASP.NET Core impostare sul lato client. [jQuery](http://jquery.com/) e [Bootstrap](http://getbootstrap.com/) vengono installati e Bower è supportato.

Pacchetti sul lato client sono elencati nel *bower. JSON* file. Consente di configurare i modelli di progetto ASP.NET Core *bower. JSON* con Bootstrap, convalida jQuery e jQuery.

In questa esercitazione, verrà aggiunto il supporto per [carattere straordinario](http://fontawesome.io). Pacchetti bower possono essere installati con il **Gestisci pacchetti Bower** dell'interfaccia utente o manualmente nel *bower. JSON* file.

### <a name="installation-via-manage-bower-packages-ui"></a>Installazione tramite pacchetti Bower gestione dell'interfaccia utente

* Creare una nuova app Web di ASP.NET Core con il **applicazione Web di ASP.NET Core (Core .NET)** modello. Selezionare **applicazione Web** e **Nessuna autenticazione**.

* Fare clic sul progetto in Esplora soluzioni e selezionare **Gestisci pacchetti Bower** (in alternativa dal menu principale, **progetto** > **Gestisci pacchetti Bower**).

* Nel **Bower: \<nome progetto\>**  finestra, fare clic sulla scheda "Sfoglia" e quindi filtrare l'elenco di pacchetti immettendo `font-awesome` nella casella di ricerca:

 ![gestire i pacchetti bower](bower/_static/manage-bower-packages.png)

* Verificare che il "salvare le modifiche a *bower. JSON*" casella di controllo è selezionata. Selezionare una versione dall'elenco a discesa e fare clic su di **installare** pulsante. Il **Output** finestra Visualizza i dettagli di installazione.

### <a name="manual-installation-in-bowerjson"></a>Installazione manuale in bower. JSON

Aprire il *bower. JSON* "tipo di carattere straordinario" aggiungere le dipendenze e dei file. IntelliSense mostra i pacchetti disponibili. Quando si seleziona un pacchetto, vengono visualizzate le versioni disponibili. Le immagini seguenti sono precedenti e non corrisponderanno a quanto visualizzato.

![IntelliSense di Esplora pacchetti bower](bower/_static/add-package.png)

![versione bower IntelliSense](bower/_static/version-intelliSense.png)

Bower utilizza [controllo delle versioni semantico](http://semver.org/) per organizzare le dipendenze. Controllo delle versioni semantico, noto anche come SemVer, identifica i pacchetti con lo schema di numerazione \<principale >.\< secondaria >. \<patch >. IntelliSense semplifica il controllo delle versioni semantico mostrando solo alcune opzioni comuni. Il primo elemento nell'elenco di IntelliSense (4.6.3 nell'esempio precedente) viene considerato l'ultima versione stabile del pacchetto. Il simbolo di accento circonflesso (^) corrisponda alla versione principale più recente e la tilde (~) corrisponda alla versione secondaria più recente.

Salvare il *bower. JSON* file. Visual Studio controlla il *bower. JSON* file per le modifiche. Al momento del salvataggio, il *installazione bower* comando viene eseguito. Vedere la finestra di Output **Bower o npm** vista per eseguire il comando esatto.

Aprire il *. bowerrc* file *bower. JSON*. Il `directory` è impostata su *wwwroot/lib* che indica la posizione Bower installerà le risorse del pacchetto.

```json
{
 "directory": "wwwroot/lib"
}
```

È possibile utilizzare la casella di ricerca in Esplora soluzioni per trovare e visualizzare il pacchetto straordinario con tipo di carattere.

Aprire il *Views\Shared\_cshtml* file e aggiungere il file CSS straordinario con tipo di carattere ambiente [Helper di Tag](xref:mvc/views/tag-helpers/intro) per `Development`. Da Esplora soluzioni, trascinare e rilasciare *carattere awesome.css* all'interno di `<environment names="Development">` elemento.

[!code-html[Main](bower/sample/_Layout.cshtml?highlight=4&range=9-13)]

In un'app di produzione si aggiungerebbe *carattere awesome.min.css* per l'helper di tag di ambiente per `Staging,Production`.

Sostituire il contenuto del *Views\Home\About.cshtml* file Razor con il markup seguente:

[!code-html[Main](bower/sample/About.cshtml)]

Eseguire l'app e passare alla visualizzazione di informazioni per verificare il funzionamento del pacchetto straordinario con tipo di carattere.

## <a name="exploring-the-client-side-build-process"></a>Esplorare il processo di compilazione sul lato client

La maggior parte dei modelli di progetto ASP.NET Core sono già configurati per utilizzare Bower. In questa procedura dettagliata successiva inizia con un progetto vuoto di ASP.NET Core e aggiunge ogni elemento manualmente, è possibile ottenere un aspetto della modalità di utilizzo Bower in un progetto. È possibile vedere cosa accade alla struttura di progetto e il runtime di output come viene eseguita ogni modifica alla configurazione.

I passaggi generali per utilizzare il processo di compilazione sul lato client con Bower sono:

* Definire pacchetti utilizzati nel progetto. <!-- once defined, you don't need to download them, VS does -->
* Pacchetti di riferimento dalle pagine web.

### <a name="define-packages"></a>Definire pacchetti

Una volta elencare i pacchetti nel *bower. JSON* file, Visual Studio li scaricheranno. L'esempio seguente usa Bower caricare jQuery e Bootstrap per il *wwwroot* cartella.

* Creare una nuova app Web di ASP.NET Core con il **applicazione Web di ASP.NET Core (Core .NET)** modello. Selezionare il **vuoto** modello di progetto e fare clic su **OK**.

* In Esplora soluzioni, fare clic sul progetto > **Aggiungi nuovo elemento** e selezionare **File di configurazione Bower**. Nota: A *. bowerrc* verrà inoltre aggiunto file.

* Aprire *bower. JSON*e aggiungere jquery e bootstrap per il `dependencies` sezione. Il valore risultante *bower. JSON* file sarà simile al seguente. Le versioni cambiano nel tempo e potrebbero non corrispondere nell'immagine seguente.

[!code-json[Main](bower/sample/bower.json?highlight=5,6)]

* Salvare il *bower. JSON* file.

 Verificare che il progetto includa il *bootstrap* e *jQuery* directory *wwwroot/lib*. Bower utilizza il *. bowerrc* file per installare gli asset in *wwwroot/lib*.

 Nota: L'interfaccia utente di "Gestione dei pacchetti Bower" fornisce un'alternativa alla modifica dei file manuale.

### <a name="enable-static-files"></a>Abilitare i file statici

* Aggiungere il `Microsoft.AspNetCore.StaticFiles` pacchetto NuGet al progetto.
* Abilitare i file statici da gestire con il [middleware file statici](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions). Aggiungere una chiamata a [UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions) per il `Configure` metodo `Startup`.

[!code-csharp[Main](bower/sample/Startup.cs?highlight=9)]

### <a name="reference-packages"></a>Pacchetti di riferimento

In questa sezione si creerà una pagina HTML per verificare che i pacchetti distribuiti può accedervi.

* Aggiungere una nuova pagina HTML denominata *Index.html* per il *wwwroot* cartella. Nota: È necessario aggiungere il file HTML per il *wwwroot* cartella. Per impostazione predefinita, il contenuto statico non può essere visualizzato all'esterno di *wwwroot*. Vedere [utilizzo di file statici](xref:fundamentals/static-files) per ulteriori informazioni.

 Sostituire il contenuto di *Index.html* con il markup seguente:

[!code-html[Main](bower/sample/Index.html)]

* Eseguire l'app e passare a `http://localhost:<port>/Index.html`. In alternativa, con *Index.html* aperta, premere `Ctrl+Shift+W`. Verificare che venga applicato lo stile jumbotron, il codice jQuery risponde quando viene scelto il pulsante e che il Bootstrap cambia lo stato.

 ![stile Jumbotron applicato](bower/_static/jumbotron.png)
