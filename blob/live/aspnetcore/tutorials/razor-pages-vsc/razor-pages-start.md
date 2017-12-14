---
title: Introduzione all'uso di pagine Razor in ASP.NET Core con Visual Studio Code
author: rick-anderson
description: Introduzione all'uso di pagine Razor in ASP.NET Core con Visual Studio Code
keywords: ASP.NET Core, pagine Razor, scaffolding, Entity Framework Core, EF, EF Core, database, mac, macOS, Visual Studio Code, Code
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: 1b9dff14fa98314601fa44aa229aef6b73bb79d0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="getting-started-with-razor-pages-in-aspnet-core-with-visual-studio-code"></a><span data-ttu-id="8b13d-104">Introduzione all'uso di pagine Razor in ASP.NET Core con Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8b13d-104">Getting started with Razor Pages in ASP.NET Core with Visual Studio Code</span></span>

<span data-ttu-id="8b13d-105">Di [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8b13d-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8b13d-106">Questa esercitazione illustra le nozioni di base della creazione di un'app Web pagine Razor di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8b13d-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="8b13d-107">Si consiglia di leggere [Introduzione all'uso di pagine Razor](xref:mvc/razor-pages/index) prima di iniziare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8b13d-107">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="8b13d-108">Pagine Razor è il modo consigliato per creare l'interfaccia utente per applicazioni Web in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8b13d-108">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b13d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b13d-109">Prerequisites</span></span>

<span data-ttu-id="8b13d-110">Installare gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b13d-110">Install the following:</span></span>

* <span data-ttu-id="8b13d-111">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) o versione successiva</span><span class="sxs-lookup"><span data-stu-id="8b13d-111">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* [<span data-ttu-id="8b13d-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8b13d-112">Visual Studio Code</span></span>](https://code.visualstudio.com)
* <span data-ttu-id="8b13d-113">VS Code [estensione C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="8b13d-113">VS Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span> 

## <a name="create-a-razor-web-app"></a><span data-ttu-id="8b13d-114">Creare un'app Web Razor</span><span class="sxs-lookup"><span data-stu-id="8b13d-114">Create a Razor web app</span></span>

<span data-ttu-id="8b13d-115">Da un terminale eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b13d-115">From a terminal, run the following commands:</span></span>

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="8b13d-116">I comandi precedenti usano [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) per creare ed eseguire un progetto di pagine Razor.</span><span class="sxs-lookup"><span data-stu-id="8b13d-116">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="8b13d-117">Aprire un browser all'indirizzo http://localhost:5000/ per visualizzare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b13d-117">Open a browser to http://localhost:5000 to view the application.</span></span>

![Pagina Home o di indice](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="8b13d-119">Aprire il progetto</span><span class="sxs-lookup"><span data-stu-id="8b13d-119">Open the project</span></span>

<span data-ttu-id="8b13d-120">Premere Ctrl + C per arrestare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b13d-120">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="8b13d-121">Da Visual Studio Code (VS Code), selezionare **File > Apri cartella**, quindi selezionare la cartella *RazorPagesMovie*.</span><span class="sxs-lookup"><span data-stu-id="8b13d-121">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="8b13d-122">Selezionare **Yes** (Sì) nel messaggio di **avviso** indicante che le risorse necessarie per la compilazione e il debug mancano in "RazorPagesMovie"</span><span class="sxs-lookup"><span data-stu-id="8b13d-122">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="8b13d-123">e se si vuole aggiungerle.</span><span class="sxs-lookup"><span data-stu-id="8b13d-123">Add them?"</span></span>
- <span data-ttu-id="8b13d-124">Selezionare **Ripristina** per il messaggio di **informazione** "Dipendenze non risolte".</span><span class="sxs-lookup"><span data-stu-id="8b13d-124">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="8b13d-125">Avviare l'app</span><span class="sxs-lookup"><span data-stu-id="8b13d-125">Launch the app</span></span>

<span data-ttu-id="8b13d-126">Premere CTRL+F5 per avviare l'app senza debug.</span><span class="sxs-lookup"><span data-stu-id="8b13d-126">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="8b13d-127">In alternativa, scegliere **Avvia senza eseguire debug** dal menu **Debug**.</span><span class="sxs-lookup"><span data-stu-id="8b13d-127">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="8b13d-128">Nella prossima esercitazione viene aggiunto un modello al progetto.</span><span class="sxs-lookup"><span data-stu-id="8b13d-128">In the next tutorial, we add a model to the project.</span></span> 

>[!div class="step-by-step"]
[<span data-ttu-id="8b13d-129">Avanti: Aggiunta di un modello</span><span class="sxs-lookup"><span data-stu-id="8b13d-129">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  