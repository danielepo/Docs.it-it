---
title: "Aggiunta della funzionalità di ricerca alle pagine Razor di ASP.NET Core MVC"
author: rick-anderson
description: "Illustra come aggiungere la funzionalità di ricerca alle pagine Razor di ASP.NET Core"
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/razor-pages/search
ms.openlocfilehash: 2859d52e42d4430808e01739474df0598c07c805
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="adding-search-to-a-razor-pages-app"></a>Aggiunta della funzionalità di ricerca a un'app di pagine Razor

Di [Rick Anderson](https://twitter.com/RickAndMSFT)

In questo documento viene aggiunta una funzionalità di ricerca alla pagina di indice che consente di ricercare i film in base al *genere* o al *nome*.

Aggiornare il metodo `OnGetAsync` della pagina di indice con il codice seguente:

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

La prima riga del metodo `OnGetAsync` crea una query [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) per selezionare i film:

```csharp
var movies = from m in _context.Movie
             select m;
```

La query viene *solo* definita in questo punto, ma **non** viene eseguita nel database.

Se il parametro `searchString` contiene una stringa, la query dei film viene modificata per filtrare gli elementi in base alla stringa di ricerca:

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

Il codice `s => s.Title.Contains()` è un'[espressione lambda](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions). Le espressioni lambda vengono usate nelle query [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/) basate sul metodo come argomenti dei metodi di operatore query standard, ad esempio il metodo [Where](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) o `Contains` (usato nel codice precedente). Le query LINQ non vengono eseguite al momento della definizione o della modifica chiamando un metodo, ad esempio `Where`, `Contains` o `OrderBy`. L'esecuzione della query viene invece posticipata. Per esecuzione posticipata si intende che la valutazione di un'espressione viene ritardata finché non viene eseguita l'iterazione del valore ottenuto o non viene chiamato il metodo `ToListAsync`. Per altre informazioni, vedere [Esecuzione di query](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/query-execution).

**Nota:** il metodo [Contains](https://docs.microsoft.com//dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) viene eseguito sul database, non nel codice C#. La distinzione tra maiuscole/minuscole nella query dipende dal database e dalle regole di confronto. In SQL Server `Contains` esegue il mapping a [SQL LIKE](https://docs.microsoft.com/sql/t-sql/language-elements/like-transact-sql) che fa distinzione tra maiuscole e minuscole. In SQLite, con le regole di confronto predefinite si fa distinzione tra maiuscole e minuscole.

Passare alla pagina Movies e aggiungere una stringa di query, ad esempio `?searchString=Ghost` all'URL, ad esempio `http://localhost:5000/Movies?searchString=Ghost`. Vengono visualizzati i film filtrati.

![Vista Index](search/_static/ghost.png)

Se il modello di route seguente viene aggiunto alla pagina di indice, la stringa di ricerca può essere passata come segmento di URL, ad esempio `http://localhost:5000/Movies/ghost`.

```cshtml
@page "{searchString?}"
```

Il vincolo di route precedente consente la ricerca del titolo come dati della route (un segmento URL), anziché come valore della stringa di query.  Il carattere `?` in `"{searchString?}"` indica che questo parametro di route è facoltativo.

![Vista Index con la parola ghost aggiunta all'URL e un elenco restituito di due film: Ghostbusters e Ghostbusters 2](search/_static/g2.png)

Non è tuttavia possibile supporre che gli utenti modifichino l'URL per cercare un film. In questo passaggio viene aggiunta l'interfaccia utente per filtrare i film. Rimuovere il vincolo di route `"{searchString?}"`, se è stato aggiunto.

Aprire il file *Pages/Movies/Index.cshtml* e aggiungere il markup `<form>` evidenziato nel codice seguente:

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

Il tag HTML `<form>` usa l'[helper tag del modulo](xref:mvc/views/working-with-forms#the-form-tag-helper). Quando il modulo viene inviato, la stringa di filtro verrà inviata alla pagina *Pages/Movies/Index*. Salvare le modifiche e testare il filtro.

![Vista Index con la parola ghost digitata nella casella di testo del filtro del titolo](search/_static/filter.png)

## <a name="search-by-genre"></a>Ricerca in base al genere

Aggiungere le proprietà evidenziate seguenti in *Pages/Movies/Index.cshtml.cs*:

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-)]

`SelectList Genres` contiene l'elenco dei generi. Consente all'utente di selezionare un genere dall'elenco.

La proprietà `MovieGenre` contiene il genere specificato selezionate dall'utente, ad esempio, "Western".

Aggiornare il metodo `OnGetAsync` con il codice seguente:

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

Il codice seguente è una query LINQ che recupera tutti i generi dal database.

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

L'elenco `SelectList` di generi viene creato presentando generi distinti.

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There is no start line.

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a>Aggiunta della funzionalità di ricerca in base al genere

Aggiornare *Index.cshtml* come indicato di seguito:

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

Eseguire il test dell'app effettuando una ricerca per genere, titolo del film e usando entrambi i filtri.

>[!div class="step-by-step"]
[Precedente: Aggiornamento delle pagine](xref:tutorials/razor-pages/da1)
[Successivo: Aggiunta di un nuovo campo](xref:tutorials/razor-pages/new-field)
