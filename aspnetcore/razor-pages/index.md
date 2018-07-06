---
title: Introduzione a Razor Pages in ASP.NET Core
author: Rick-Anderson
description: Informazioni su come Razor Pages in ASP.NET Core semplifica e rende più produttiva la scrittura di codice incentrata sulle pagine rispetto a MVC.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/12/2018
uid: razor-pages/index
ms.openlocfilehash: 9d7d4d49dbb55e327a208df99a0e3ca744de8609
ms.sourcegitcommit: 931b6a2d7eb28a0f1295e8a95690b8c4c5f58477
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37077748"
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="8a72e-103">Introduzione a Razor Pages in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8a72e-103">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="8a72e-104">Di [Rick Anderson](https://twitter.com/RickAndMSFT) e [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="8a72e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="8a72e-105">Razor Pages è una nuova funzionalità di ASP.NET Core MVC che semplifica e rende più produttiva la scrittura di codice incentrata sulle pagine.</span><span class="sxs-lookup"><span data-stu-id="8a72e-105">Razor Pages is a new aspect of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="8a72e-106">Se si sta cercando un'esercitazione in cui si usa l'approccio Model-View-Controller, vedere [Introduzione ad ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="8a72e-106">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Get started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="8a72e-107">Questo documento offre un'introduzione a Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="8a72e-107">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="8a72e-108">Non è un'esercitazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="8a72e-108">It's not a step by step tutorial.</span></span> <span data-ttu-id="8a72e-109">Se alcune sezioni risultano troppo avanzate, vedere [Introduzione a Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span><span class="sxs-lookup"><span data-stu-id="8a72e-109">If you find some of the sections too advanced, see [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="8a72e-110">Per una panoramica di ASP.NET Core, vedere [Introduzione a ASP.NET Core](xref:index).</span><span class="sxs-lookup"><span data-stu-id="8a72e-110">For an overview of ASP.NET Core, see the [Introduction to ASP.NET Core](xref:index).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a72e-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8a72e-111">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a><span data-ttu-id="8a72e-112">Creazione di un progetto Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-112">Creating a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="8a72e-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a72e-113">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="8a72e-114">Per istruzioni dettagliate su come creare un progetto Razor Pages con Visual Studio, vedere [Introduzione a Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span><span class="sxs-lookup"><span data-stu-id="8a72e-114">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project using Visual Studio.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="8a72e-115">Visual Studio per Mac</span><span class="sxs-lookup"><span data-stu-id="8a72e-115">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a72e-116">Eseguire `dotnet new webapp` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-116">Run `dotnet new webapp` from the command line.</span></span>

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="8a72e-117">Eseguire `dotnet new razor` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-117">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

<span data-ttu-id="8a72e-118">Aprire il file *CSPROJ* generato da Visual Studio per Mac.</span><span class="sxs-lookup"><span data-stu-id="8a72e-118">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="8a72e-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8a72e-119">Visual Studio Code</span></span>](#tab/visual-studio-code)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a72e-120">Eseguire `dotnet new webapp` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-120">Run `dotnet new webapp` from the command line.</span></span>

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="8a72e-121">Eseguire `dotnet new razor` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-121">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="8a72e-122">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="8a72e-122">.NET Core CLI</span></span>](#tab/netcore-cli)

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a72e-123">Eseguire `dotnet new webapp` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-123">Run `dotnet new webapp` from the command line.</span></span>

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="8a72e-124">Eseguire `dotnet new razor` dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8a72e-124">Run `dotnet new razor` from the command line.</span></span>

::: moniker-end

---

## <a name="razor-pages"></a><span data-ttu-id="8a72e-125">Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-125">Razor Pages</span></span>

<span data-ttu-id="8a72e-126">La funzionalità Razor Pages è abilitata in *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-126">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="8a72e-127">Si consideri una pagina di base: <a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="8a72e-127">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="8a72e-128">Il codice precedente è molto simile a un file di visualizzazione Razor.</span><span class="sxs-lookup"><span data-stu-id="8a72e-128">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="8a72e-129">Ciò che lo differenzia è la direttiva `@page`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-129">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="8a72e-130">`@page` trasforma il file in un'azione MVC, ovvero gestisce le richieste direttamente, senza passare attraverso un controller.</span><span class="sxs-lookup"><span data-stu-id="8a72e-130">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="8a72e-131">`@page` deve essere la prima direttiva Razor in una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-131">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="8a72e-132">`@page` influisce sul comportamento di altri costrutti Razor.</span><span class="sxs-lookup"><span data-stu-id="8a72e-132">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="8a72e-133">Nei due file seguenti viene visualizzata una pagina simile che usa una classe `PageModel`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-133">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="8a72e-134">Il file *Pages/Index2.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-134">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="8a72e-135">Il modello di pagina *Pages/Index2.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-135">The *Pages/Index2.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="8a72e-136">Per convenzione, il file di classe `PageModel` ha lo stesso nome del file della pagina Razor con l'aggiunta di *.cs*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-136">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="8a72e-137">Ad esempio, la pagina Razor precedente è *Pages/Index2.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-137">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="8a72e-138">Il file che contiene la classe `PageModel` è denominato *Pages/Index2.cshtml.cs*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-138">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="8a72e-139">Le associazioni dei percorsi URL alle pagine sono determinate dalla posizione della pagina nel file system.</span><span class="sxs-lookup"><span data-stu-id="8a72e-139">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="8a72e-140">Nella tabella seguente sono riportati alcuni percorsi di pagina Razor con gli URL corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="8a72e-140">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="8a72e-141">Percorso e nome file</span><span class="sxs-lookup"><span data-stu-id="8a72e-141">File name and path</span></span>               | <span data-ttu-id="8a72e-142">URL corrispondente</span><span class="sxs-lookup"><span data-stu-id="8a72e-142">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="8a72e-143">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-143">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="8a72e-144">`/` o `/Index`</span><span class="sxs-lookup"><span data-stu-id="8a72e-144">`/` or `/Index`</span></span> |
| <span data-ttu-id="8a72e-145">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-145">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="8a72e-146">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-146">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="8a72e-147">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-147">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="8a72e-148">`/Store` o `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="8a72e-148">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="8a72e-149">Note:</span><span class="sxs-lookup"><span data-stu-id="8a72e-149">Notes:</span></span>

* <span data-ttu-id="8a72e-150">Il runtime cerca i file delle pagine Razor nella cartella *Pages* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8a72e-150">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="8a72e-151">`Index` è la pagina predefinita quando un URL non include una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-151">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="writing-a-basic-form"></a><span data-ttu-id="8a72e-152">Scrittura di un form di base</span><span class="sxs-lookup"><span data-stu-id="8a72e-152">Writing a basic form</span></span>

<span data-ttu-id="8a72e-153">Razor Pages semplifica l'implementazione dei modelli normalmente usati con i Web browser durante la creazione di un'app.</span><span class="sxs-lookup"><span data-stu-id="8a72e-153">Razor Pages is designed to make common patterns used with web browsers easy to implement when building an app.</span></span> <span data-ttu-id="8a72e-154">L'[associazione di modelli](xref:mvc/models/model-binding), gli [helper tag](xref:mvc/views/tag-helpers/intro) e gli helper HTML *funzionano* tutti con le proprietà definite in una classe di pagina Razor.</span><span class="sxs-lookup"><span data-stu-id="8a72e-154">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="8a72e-155">Si consideri una pagina che implementa un form "contact us" di base per il modello `Contact`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-155">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="8a72e-156">Per gli esempi riportati in questo documento, `DbContext` viene inizializzato nel file [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16).</span><span class="sxs-lookup"><span data-stu-id="8a72e-156">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="8a72e-157">Il modello di dati:</span><span class="sxs-lookup"><span data-stu-id="8a72e-157">The data model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="8a72e-158">Il contesto del database:</span><span class="sxs-lookup"><span data-stu-id="8a72e-158">The db context:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="8a72e-159">Il file di visualizzazione *Pages/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-159">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="8a72e-160">Il modello di pagina *Pages/Create.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-160">The *Pages/Create.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="8a72e-161">Per convenzione, la classe `PageModel` è denominata `<PageName>Model` e si trova nello stesso spazio dei nomi della pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-161">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="8a72e-162">La classe `PageModel` consente la separazione della logica di una pagina dalla relativa presentazione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-162">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="8a72e-163">Definisce i gestori di pagina per le richieste inviate alla pagina e i dati usati per il rendering della pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-163">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="8a72e-164">Questa separazione consente di gestire le dipendenze della pagina tramite [inserimento delle dipendenze](xref:fundamentals/dependency-injection) e di eseguire [unit test](xref:test/razor-pages-tests) delle pagine.</span><span class="sxs-lookup"><span data-stu-id="8a72e-164">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:test/razor-pages-tests) the pages.</span></span>

<span data-ttu-id="8a72e-165">La pagina contiene un oggetto `OnPostAsync`, ovvero un *metodo gestore* che viene eseguito per le richieste `POST`, quando un utente invia il form.</span><span class="sxs-lookup"><span data-stu-id="8a72e-165">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="8a72e-166">È possibile aggiungere metodi gestore per qualsiasi verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="8a72e-166">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="8a72e-167">I gestori più comuni sono:</span><span class="sxs-lookup"><span data-stu-id="8a72e-167">The most common handlers are:</span></span>

* <span data-ttu-id="8a72e-168">`OnGet` per inizializzare lo stato necessario per la pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-168">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="8a72e-169">Esempio di [OnGet](#OnGet).</span><span class="sxs-lookup"><span data-stu-id="8a72e-169">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="8a72e-170">`OnPost` per gestire gli invii di form.</span><span class="sxs-lookup"><span data-stu-id="8a72e-170">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="8a72e-171">Il suffisso `Async` nel nome è facoltativo, ma viene spesso usato per convenzione per le funzioni asincrone.</span><span class="sxs-lookup"><span data-stu-id="8a72e-171">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="8a72e-172">Il codice `OnPostAsync` nell'esempio precedente è simile a ciò che in genere si scrive in un controller.</span><span class="sxs-lookup"><span data-stu-id="8a72e-172">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="8a72e-173">Il codice precedente è tipico di Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="8a72e-173">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="8a72e-174">La maggior parte delle primitive di MVC, ad esempio l'[associazione di modelli](xref:mvc/models/model-binding), la [convalida](xref:mvc/models/validation) e i risultati dell'azione vengono condivise.</span><span class="sxs-lookup"><span data-stu-id="8a72e-174">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="8a72e-175">Il metodo `OnPostAsync` precedente:</span><span class="sxs-lookup"><span data-stu-id="8a72e-175">The previous `OnPostAsync` method:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="8a72e-176">Il flusso di base di `OnPostAsync`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-176">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="8a72e-177">Verificare se sono presenti errori di convalida.</span><span class="sxs-lookup"><span data-stu-id="8a72e-177">Check for validation errors.</span></span>

*  <span data-ttu-id="8a72e-178">Se non sono presenti errori, salvare i dati e reindirizzare.</span><span class="sxs-lookup"><span data-stu-id="8a72e-178">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="8a72e-179">Se sono presenti errori, visualizzare di nuovo la pagina con i messaggi di convalida.</span><span class="sxs-lookup"><span data-stu-id="8a72e-179">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="8a72e-180">La convalida lato client è identica alle applicazioni ASP.NET Core MVC tradizionali.</span><span class="sxs-lookup"><span data-stu-id="8a72e-180">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="8a72e-181">In molti casi gli errori di convalida vengono rilevati nel client e mai inviati al server.</span><span class="sxs-lookup"><span data-stu-id="8a72e-181">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="8a72e-182">Quando i dati vengono immessi correttamente, il metodo gestore `OnPostAsync` chiama il metodo helper `RedirectToPage` per restituire un'istanza di `RedirectToPageResult`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-182">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="8a72e-183">`RedirectToPage` è un nuovo risultato dell'azione, simile a `RedirectToAction` o `RedirectToRoute`, ma personalizzato per le pagine.</span><span class="sxs-lookup"><span data-stu-id="8a72e-183">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="8a72e-184">Nell'esempio precedente viene reindirizzato alla pagina di indice radice (`/Index`).</span><span class="sxs-lookup"><span data-stu-id="8a72e-184">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="8a72e-185">Il metodo `RedirectToPage` è descritto in dettaglio nella sezione [Generazione di URL per le pagine](#url_gen).</span><span class="sxs-lookup"><span data-stu-id="8a72e-185">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="8a72e-186">Quando il form inviato contiene errori di convalida (che vengono passati al server), il metodo gestore `OnPostAsync` chiama il metodo helper `Page`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-186">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="8a72e-187">`Page` restituisce un'istanza di `PageResult`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-187">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="8a72e-188">La restituzione di `Page` è simile al modo in cui le azioni nel controller restituiscono `View`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-188">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="8a72e-189">`PageResult` è il tipo restituito <!-- Review  --> predefinito per un metodo gestore.</span><span class="sxs-lookup"><span data-stu-id="8a72e-189">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="8a72e-190">Un metodo gestore che restituisce `void` esegue il rendering della pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-190">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="8a72e-191">La proprietà `Customer` usa l'attributo `[BindProperty]` optare per consentire l'associazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="8a72e-191">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="8a72e-192">Per impostazione predefinita Razor Pages associa le proprietà solo ai verbi non GET.</span><span class="sxs-lookup"><span data-stu-id="8a72e-192">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="8a72e-193">Il binding alle proprietà può ridurre la quantità di codice da scrivere.</span><span class="sxs-lookup"><span data-stu-id="8a72e-193">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="8a72e-194">Riduce il codice usando la stessa proprietà per il eseguire il rendering dei campi del form (`<input asp-for="Customer.Name" />`) e accettare l'input.</span><span class="sxs-lookup"><span data-stu-id="8a72e-194">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

> [!NOTE]
> <span data-ttu-id="8a72e-195">Per motivi di sicurezza, è necessario acconsentire esplicitamente all'associazione dei dati della richiesta GET alle proprietà del modello di pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-195">For security reasons, you must opt in to binding GET request data to page model properties.</span></span> <span data-ttu-id="8a72e-196">Verificare l'input dell'utente prima di eseguirne il mapping alle proprietà.</span><span class="sxs-lookup"><span data-stu-id="8a72e-196">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="8a72e-197">Acconsentire esplicitamente a questo comportamento è utile quando si lavora in scenari basati su valori route o stringa di query.</span><span class="sxs-lookup"><span data-stu-id="8a72e-197">Opting in to this behavior is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="8a72e-198">Per associare una proprietà nelle richieste GET, impostare la proprietà `SupportsGet` dell'attributo `[BindProperty]` su `true`: `[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="8a72e-198">To bind a property on GET requests, set the `[BindProperty]` attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>

<span data-ttu-id="8a72e-199">La home page (*Index.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="8a72e-199">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="8a72e-200">La classe `PageModel` associata (*Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a72e-200">The associated `PageModel` class (*Index.cshtml.cs*):</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="8a72e-201">Il file *Index.cshtml* contiene il markup seguente per creare un collegamento di modifica per ogni contatto:</span><span class="sxs-lookup"><span data-stu-id="8a72e-201">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="8a72e-202">[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) ha usato l'attributo `asp-route-{value}` per generare un collegamento alla pagina di modifica.</span><span class="sxs-lookup"><span data-stu-id="8a72e-202">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="8a72e-203">Il collegamento contiene i dati della route con l'ID contatto.</span><span class="sxs-lookup"><span data-stu-id="8a72e-203">The link contains route data with the contact ID.</span></span> <span data-ttu-id="8a72e-204">Ad esempio `http://localhost:5000/Edit/1`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-204">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="8a72e-205">Il file *Pages/Edit.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-205">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="8a72e-206">La prima riga contiene la direttiva `@page "{id:int}"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-206">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="8a72e-207">Il vincolo di routing `"{id:int}"` indica alla pagina di accettare le richieste inviate alla pagina che contengono i dati della route `int`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-207">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="8a72e-208">Se una richiesta inviata alla pagina non contiene dati della route che possono essere convertiti in un oggetto `int`, il runtime restituisce un errore HTTP 404 (non trovato).</span><span class="sxs-lookup"><span data-stu-id="8a72e-208">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span> <span data-ttu-id="8a72e-209">Per rendere l'ID facoltativo, aggiungere `?` al vincolo di route:</span><span class="sxs-lookup"><span data-stu-id="8a72e-209">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

<span data-ttu-id="8a72e-210">Il file *Pages/Edit.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-210">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="8a72e-211">Il file *Index.cshtml* contiene anche il markup per creare un pulsante di eliminazione per ogni contatto cliente:</span><span class="sxs-lookup"><span data-stu-id="8a72e-211">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="8a72e-212">Quando viene eseguito il rendering del pulsante di eliminazione in HTML, il relativo `formaction` include i parametri per:</span><span class="sxs-lookup"><span data-stu-id="8a72e-212">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="8a72e-213">L'ID di contatto cliente dall'attributo `asp-route-id`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-213">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="8a72e-214">L'`handler` specificato dall'attributo `asp-page-handler`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-214">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="8a72e-215">Di seguito è riportato un esempio di pulsante di eliminazione di cui è stato eseguito il rendering con un ID di contatto cliente `1`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-215">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="8a72e-216">Quando il pulsante è selezionato, viene inviata una richiesta `POST` di modulo al server.</span><span class="sxs-lookup"><span data-stu-id="8a72e-216">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="8a72e-217">Per convenzione, il nome del metodo del gestore viene selezionato in base al valore del parametro `handler` in base allo schema `OnPost[handler]Async`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-217">By convention, the name of the handler method is selected based the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="8a72e-218">Poiché in questo esempio l'`handler` è `delete`, il metodo `OnPostDeleteAsync` viene usato per elaborare la richiesta `POST`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-218">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="8a72e-219">Se `asp-page-handler` viene impostato su un valore diverso, come `remove`, viene selezionato un metodo gestore della pagina con il nome `OnPostRemoveAsync`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-219">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="8a72e-220">Il metodo `OnPostDeleteAsync`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-220">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="8a72e-221">Accetta l'`id` dalla stringa di query.</span><span class="sxs-lookup"><span data-stu-id="8a72e-221">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="8a72e-222">Interroga il database in merito al contatto del cliente con `FindAsync`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-222">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="8a72e-223">Se viene trovato il contatto cliente, viene rimosso dall'elenco dei contatti del cliente.</span><span class="sxs-lookup"><span data-stu-id="8a72e-223">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="8a72e-224">Il database viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="8a72e-224">The database is updated.</span></span>
* <span data-ttu-id="8a72e-225">Chiama `RedirectToPage` per reindirizzare alla pagina di indice radice (`/Index`).</span><span class="sxs-lookup"><span data-stu-id="8a72e-225">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-required"></a><span data-ttu-id="8a72e-226">Contrassegnare le proprietà della pagina con Required</span><span class="sxs-lookup"><span data-stu-id="8a72e-226">Mark page properties required</span></span>

<span data-ttu-id="8a72e-227">Le proprietà di `PageModel` possono essere decorate con l'attributo con [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute):</span><span class="sxs-lookup"><span data-stu-id="8a72e-227">Properties on a `PageModel` can be decorated with the [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) attribute:</span></span>

[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]

<span data-ttu-id="8a72e-228">Per altre informazioni, vedere [Convalida del modello](xref:mvc/models/validation).</span><span class="sxs-lookup"><span data-stu-id="8a72e-228">See [Model validation](xref:mvc/models/validation) for more information.</span></span>

## <a name="manage-head-requests-with-the-onget-handler"></a><span data-ttu-id="8a72e-229">Gestire le richieste HEAD con il gestore OnGet</span><span class="sxs-lookup"><span data-stu-id="8a72e-229">Manage HEAD requests with the OnGet handler</span></span>

<span data-ttu-id="8a72e-230">In genere, per le richieste HEAD viene creato e chiamato un gestore HEAD:</span><span class="sxs-lookup"><span data-stu-id="8a72e-230">Ordinarily, a HEAD handler is created and called for HEAD requests:</span></span>

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

<span data-ttu-id="8a72e-231">In assenza di un gestore HEAD (`OnHead`) definito, Razor Pages ricorre alla chiamata del gestore di pagine GET (`OnGet`) come fallback in ASP.NET Core 2.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8a72e-231">If no HEAD handler (`OnHead`) is defined, Razor Pages falls back to calling the GET page handler (`OnGet`) in ASP.NET Core 2.1 or later.</span></span> <span data-ttu-id="8a72e-232">È possibile acconsentire esplicitamente a questo comportamento con il [metodo SetCompatibilityVersion](xref:fundamentals/startup#setcompatibilityversion-for-aspnet-core-mvc) in `Startup.Configure` per ASP.NET Core 2.1-2.x:</span><span class="sxs-lookup"><span data-stu-id="8a72e-232">Opt in to this behavior with the [SetCompatibilityVersion method](xref:fundamentals/startup#setcompatibilityversion-for-aspnet-core-mvc) in `Startup.Configure` for ASP.NET Core 2.1 to 2.x:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

<span data-ttu-id="8a72e-233">`SetCompatibilityVersion` imposta effettivamente l'opzione di Razor Pages `AllowMappingHeadRequestsToGetHandler` su `true`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-233">`SetCompatibilityVersion` effectively sets the Razor Pages option `AllowMappingHeadRequestsToGetHandler` to `true`.</span></span>

<span data-ttu-id="8a72e-234">Anziché acconsentire esplicitamente a tutti i comportamenti 2.1 con `SetCompatibilityVersion`, è possibile accettare comportamenti specifici.</span><span class="sxs-lookup"><span data-stu-id="8a72e-234">Rather than opting into all 2.1 behaviors with `SetCompatibilityVersion`, you can explicitly opt-in to specific behaviors.</span></span> <span data-ttu-id="8a72e-235">Il codice seguente consente di accettare le richieste HEAD di mapping nel gestore GET.</span><span class="sxs-lookup"><span data-stu-id="8a72e-235">The following code opts into the mapping HEAD requests to the GET handler.</span></span>


```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```
::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="8a72e-236">XSRF/CSRF e Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-236">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="8a72e-237">Non è necessario scrivere codice per la [convalida antifalsificazione](xref:security/anti-request-forgery).</span><span class="sxs-lookup"><span data-stu-id="8a72e-237">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="8a72e-238">La generazione e la convalida del token antifalsificazione sono automaticamente incluse in Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="8a72e-238">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="8a72e-239">Uso di layout, righe parzialmente eseguite, modelli e helper tag con Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-239">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="8a72e-240">Le pagine funzionano con tutte le funzionalità del motore di visualizzazione Razor.</span><span class="sxs-lookup"><span data-stu-id="8a72e-240">Pages work with all the capabilities of the Razor view engine.</span></span> <span data-ttu-id="8a72e-241">I layout, le righe parzialmente eseguite, i modelli, gli helper tag, *_ViewStart.cshtml* e *_ViewImports.cshtml* funzionano esattamente come nelle normali visualizzazioni Razor.</span><span class="sxs-lookup"><span data-stu-id="8a72e-241">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="8a72e-242">La pagina verrà ora riorganizzata in modo da usufruire di alcune di queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8a72e-242">Let's declutter this page by taking advantage of some of those capabilities.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a72e-243">Aggiungere una [pagina di layout](xref:mvc/views/layout) a *Pages/Shared/_Layout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-243">Add a [layout page](xref:mvc/views/layout) to *Pages/Shared/_Layout.cshtml*:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="8a72e-244">Aggiungere una [pagina di layout](xref:mvc/views/layout) a *Pages/_Layout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-244">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

::: moniker-end

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="8a72e-245">Il [Layout](xref:mvc/views/layout):</span><span class="sxs-lookup"><span data-stu-id="8a72e-245">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="8a72e-246">Controlla il layout di ogni pagina, a meno che la pagina non accetti il layout.</span><span class="sxs-lookup"><span data-stu-id="8a72e-246">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="8a72e-247">Importa le strutture HTML, ad esempio JavaScript e i fogli di stile.</span><span class="sxs-lookup"><span data-stu-id="8a72e-247">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="8a72e-248">Vedere l'articolo sulla [pagina Layout](xref:mvc/views/layout) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="8a72e-248">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="8a72e-249">La proprietà [Layout](xref:mvc/views/layout#specifying-a-layout) proprietà viene impostata in *Pages/_ViewStart.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-249">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a72e-250">Il layout è nella cartella *Shared/Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-250">The layout is in the *Shared/Pages* folder.</span></span> <span data-ttu-id="8a72e-251">Le pagine cercano altre visualizzazioni (layout, modelli, righe parzialmente eseguite) in modo gerarchico, partendo dalla stessa cartella della pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="8a72e-251">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="8a72e-252">Un layout nella cartella *Shared/Pages* può essere usato da qualsiasi pagina Razor della cartella *Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-252">A layout in the *Shared/Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="8a72e-253">Il file di layout dovrebbe andare nella cartella *Pages/Shared*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-253">The layout file should go in the *Pages/Shared* folder.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="8a72e-254">Il layout è nella cartella *Pages* (Pagine).</span><span class="sxs-lookup"><span data-stu-id="8a72e-254">The layout is in the *Pages* folder.</span></span> <span data-ttu-id="8a72e-255">Le pagine cercano altre visualizzazioni (layout, modelli, righe parzialmente eseguite) in modo gerarchico, partendo dalla stessa cartella della pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="8a72e-255">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="8a72e-256">Un layout nella cartella *Pages* può essere usato da qualsiasi pagina Razor della cartella *Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-256">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

::: moniker-end

<span data-ttu-id="8a72e-257">Si consiglia di **non** inserire il file di layout nella cartella *Views/Shared*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-257">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="8a72e-258">*Views/Shared* è un modello destinato alle visualizzazioni MVC.</span><span class="sxs-lookup"><span data-stu-id="8a72e-258">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="8a72e-259">Le pagine Razor devono basarsi sulla gerarchia di cartelle, non su convenzioni di percorso.</span><span class="sxs-lookup"><span data-stu-id="8a72e-259">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="8a72e-260">La ricerca delle visualizzazioni da una pagina Razor include la cartella *Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-260">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="8a72e-261">Il layout, i modelli e le righe parzialmente eseguite in uso con i controller MVC e le visualizzazioni Razor standard *funzionano solo*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-261">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="8a72e-262">Aggiungere un file *Pages/_ViewImports.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-262">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="8a72e-263">`@namespace` viene spiegato in seguito nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-263">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="8a72e-264">La direttiva `@addTagHelper` inserisce gli [helper tag predefiniti](xref:mvc/views/tag-helpers/builtin-th/Index) in tutte le pagine presenti nella cartella *Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-264">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="8a72e-265">Quando la direttiva `@namespace` viene usata in modo esplicito in una pagina:</span><span class="sxs-lookup"><span data-stu-id="8a72e-265">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="8a72e-266">La direttiva imposta lo spazio dei nomi per la pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-266">The directive sets the namespace for the page.</span></span> <span data-ttu-id="8a72e-267">La direttiva `@model` non deve necessariamente includere lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8a72e-267">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="8a72e-268">Se la direttiva `@namespace` è contenuta in *_ViewImports.cshtml*, lo spazio dei nomi specificato indica il prefisso per lo spazio dei nomi generato nella pagina che importa la direttiva `@namespace`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-268">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="8a72e-269">Il resto dello spazio dei nomi generato (la parte del suffisso) è il percorso relativo separato dal punto tra la cartella contenente *_Viewimports.cshtml* e la cartella contenente la pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-269">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="8a72e-270">Ad esempio, la classe `PageModel` *Pages/Customers/Edit.cshtml.cs* imposta in modo esplicito lo spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="8a72e-270">For example, the `PageModel` class *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="8a72e-271">Il file *Pages/_ViewImports.cshtml* file imposta il seguente spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="8a72e-271">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="8a72e-272">Lo spazio dei nomi generato per la pagina Razor *Pages/Customers/Edit.cshtml* corrisponde alla classe `PageModel`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-272">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the `PageModel` class.</span></span>

<span data-ttu-id="8a72e-273">`@namespace` *Funziona anche con le normali visualizzazioni Razor.*</span><span class="sxs-lookup"><span data-stu-id="8a72e-273">`@namespace` *also works with conventional Razor views.*</span></span>

<span data-ttu-id="8a72e-274">Il file di visualizzazione *Pages/Create.cshtml* originale:</span><span class="sxs-lookup"><span data-stu-id="8a72e-274">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="8a72e-275">Il file di visualizzazione *Pages/Create.cshtml* aggiornato:</span><span class="sxs-lookup"><span data-stu-id="8a72e-275">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="8a72e-276">Il [progetto iniziale per Razor Pages](#rpvs17) contiene il file *Pages/_ValidationScriptsPartial.cshtml*, che esegue la convalida sul lato client.</span><span class="sxs-lookup"><span data-stu-id="8a72e-276">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="8a72e-277">Generazione di URL per le pagine</span><span class="sxs-lookup"><span data-stu-id="8a72e-277">URL generation for Pages</span></span>

<span data-ttu-id="8a72e-278">La pagina `Create`, riportata in precedenza, usa `RedirectToPage`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-278">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="8a72e-279">L'applicazione ha la struttura di file o cartella seguente:</span><span class="sxs-lookup"><span data-stu-id="8a72e-279">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="8a72e-280">*/Pages*</span><span class="sxs-lookup"><span data-stu-id="8a72e-280">*/Pages*</span></span>

  * <span data-ttu-id="8a72e-281">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-281">*Index.cshtml*</span></span>
  * <span data-ttu-id="8a72e-282">*/Customers*</span><span class="sxs-lookup"><span data-stu-id="8a72e-282">*/Customers*</span></span>

    * <span data-ttu-id="8a72e-283">*Create.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-283">*Create.cshtml*</span></span>
    * <span data-ttu-id="8a72e-284">*Edit.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-284">*Edit.cshtml*</span></span>
    * <span data-ttu-id="8a72e-285">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="8a72e-285">*Index.cshtml*</span></span>

<span data-ttu-id="8a72e-286">Le pagine *Pages/Customers/Create.cshtml* e *Pages/Customers/Edit.cshtml* reindirizzano a *Pages/Index.cshtml* dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-286">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="8a72e-287">La stringa `/Index` fa parte dell'URI di accesso alla pagina precedente.</span><span class="sxs-lookup"><span data-stu-id="8a72e-287">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="8a72e-288">La stringa `/Index` può essere usata per generare gli URI alla pagina *Pages/Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-288">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="8a72e-289">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8a72e-289">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="8a72e-290">Il nome della pagina è il percorso alla pagina dalla cartella radice */Pages*, inclusa una barra iniziale `/`, ad esempio `/Index`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-290">The page name is the path to the page from the root */Pages* folder including a leading `/` (for example, `/Index`).</span></span> <span data-ttu-id="8a72e-291">Gli esempi di generazione di URL precedenti offrono opzioni e caratteristiche funzionali avanzate rispetto agli URL hardcoded.</span><span class="sxs-lookup"><span data-stu-id="8a72e-291">The preceding URL generation samples offer enhanced options and functional capabilities over hardcoding a URL.</span></span> <span data-ttu-id="8a72e-292">La generazione di URL usa il [routing](xref:mvc/controllers/routing) ed è in grado di generare e codificare i parametri in base al modo in cui la route è definita nel percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-292">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="8a72e-293">La generazione di URL per le pagine supporta i nomi relativi.</span><span class="sxs-lookup"><span data-stu-id="8a72e-293">URL generation for pages supports relative names.</span></span> <span data-ttu-id="8a72e-294">La tabella seguente indica quale pagina di indice viene selezionata con diversi parametri `RedirectToPage` da *Pages/Customers/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8a72e-294">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="8a72e-295">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="8a72e-295">RedirectToPage(x)</span></span>| <span data-ttu-id="8a72e-296">Pagina</span><span class="sxs-lookup"><span data-stu-id="8a72e-296">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="8a72e-297">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="8a72e-297">RedirectToPage("/Index")</span></span> | <span data-ttu-id="8a72e-298">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="8a72e-298">*Pages/Index*</span></span> |
| <span data-ttu-id="8a72e-299">RedirectToPage("./Index");</span><span class="sxs-lookup"><span data-stu-id="8a72e-299">RedirectToPage("./Index");</span></span> | <span data-ttu-id="8a72e-300">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="8a72e-300">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="8a72e-301">RedirectToPage("../Index")</span><span class="sxs-lookup"><span data-stu-id="8a72e-301">RedirectToPage("../Index")</span></span> | <span data-ttu-id="8a72e-302">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="8a72e-302">*Pages/Index*</span></span> |
| <span data-ttu-id="8a72e-303">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="8a72e-303">RedirectToPage("Index")</span></span>  | <span data-ttu-id="8a72e-304">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="8a72e-304">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="8a72e-305">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, e `RedirectToPage("../Index")` sono <em>nomi relativi</em>.</span><span class="sxs-lookup"><span data-stu-id="8a72e-305">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are <em>relative names</em>.</span></span> <span data-ttu-id="8a72e-306">Il parametro `RedirectToPage` è <em>combinato</em> con il percorso della pagina corrente per calcolare il nome della pagina di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-306">The `RedirectToPage` parameter is <em>combined</em> with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

<span data-ttu-id="8a72e-307">Il collegamento dei nomi relativi è utile quando si compilano siti con una struttura complessa.</span><span class="sxs-lookup"><span data-stu-id="8a72e-307">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="8a72e-308">Se si usano i nomi relativi per il collegamento tra le pagine in una cartella, è possibile rinominare tale cartella.</span><span class="sxs-lookup"><span data-stu-id="8a72e-308">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="8a72e-309">Tutti i collegamenti continuano a funzionare perché non includono il nome della cartella.</span><span class="sxs-lookup"><span data-stu-id="8a72e-309">All the links still work (because they didn't include the folder name).</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="viewdata-attribute"></a><span data-ttu-id="8a72e-310">Attributo viewData</span><span class="sxs-lookup"><span data-stu-id="8a72e-310">ViewData attribute</span></span>

<span data-ttu-id="8a72e-311">È possibile passare i dati a una pagina tramite [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span><span class="sxs-lookup"><span data-stu-id="8a72e-311">Data can be passed to a page with [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="8a72e-312">I valori delle proprietà nei controller o nei modelli Razor Page decorate con `[ViewData]` vengono archiviati e caricati da [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span><span class="sxs-lookup"><span data-stu-id="8a72e-312">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span></span>

<span data-ttu-id="8a72e-313">Nell'esempio seguente `AboutModel` contiene una proprietà `Title` decorata con `[ViewData]`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-313">In the following example, the `AboutModel` contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="8a72e-314">La proprietà `Title` è impostata sul titolo della pagina About (Informazioni):</span><span class="sxs-lookup"><span data-stu-id="8a72e-314">The `Title` property is set to the title of the About page:</span></span>

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

<span data-ttu-id="8a72e-315">Nella pagina About (Informazioni) accedere alla proprietà `Title` come proprietà del modello:</span><span class="sxs-lookup"><span data-stu-id="8a72e-315">In the About page, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="8a72e-316">Nel layout il titolo viene letto dal dizionario ViewData:</span><span class="sxs-lookup"><span data-stu-id="8a72e-316">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```
::: moniker-end

## <a name="tempdata"></a><span data-ttu-id="8a72e-317">TempData</span><span class="sxs-lookup"><span data-stu-id="8a72e-317">TempData</span></span>

<span data-ttu-id="8a72e-318">ASP.NET Core espone la proprietà [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) per un [controller](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span><span class="sxs-lookup"><span data-stu-id="8a72e-318">ASP.NET Core exposes the [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="8a72e-319">Questa proprietà archivia i dati finché non viene letta.</span><span class="sxs-lookup"><span data-stu-id="8a72e-319">This property stores data until it's read.</span></span> <span data-ttu-id="8a72e-320">I metodi `Keep` e `Peek` possono essere usati per esaminare i dati senza eliminazione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-320">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="8a72e-321">`TempData` è utile per il reindirizzamento quando i dati sono necessari per più di una singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="8a72e-321">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="8a72e-322">L'attributo `[TempData]` è nuovo in ASP.NET Core 2.0 ed è supportato per controller e pagine.</span><span class="sxs-lookup"><span data-stu-id="8a72e-322">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="8a72e-323">Il codice seguente imposta il valore di `Message` usando `TempData`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-323">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="8a72e-324">Il markup seguente nel file *Pages/Customers/Index.cshtml* visualizza il valore di `Message` usando `TempData`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-324">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="8a72e-325">Il modello di pagina *Pages/Customers/Index.cshtml.cs* applica l'attributo `[TempData]` alla proprietà `Message`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-325">The *Pages/Customers/Index.cshtml.cs* page model applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="8a72e-326">Per altre informazioni, vedere [TempData](xref:fundamentals/app-state#tempdata).</span><span class="sxs-lookup"><span data-stu-id="8a72e-326">See [TempData](xref:fundamentals/app-state#tempdata) for more information.</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="8a72e-327">Più gestori per pagina</span><span class="sxs-lookup"><span data-stu-id="8a72e-327">Multiple handlers per page</span></span>

<span data-ttu-id="8a72e-328">La pagina seguente genera markup per due gestori di pagina usando l'helper tag `asp-page-handler`:</span><span class="sxs-lookup"><span data-stu-id="8a72e-328">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

<span data-ttu-id="8a72e-329">Il form nell'esempio precedente contiene due pulsanti di invio, ognuno dei quali usa `FormActionTagHelper` per l'invio a un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="8a72e-329">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="8a72e-330">L'attributo `asp-page-handler` è correlato a `asp-page`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-330">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="8a72e-331">`asp-page-handler` genera gli URL che indirizzano a ognuno dei metodi gestore definiti da una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-331">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="8a72e-332">`asp-page` non è specificato poiché l'esempio è collegato alla pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="8a72e-332">`asp-page` isn't specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="8a72e-333">Il modello di pagina:</span><span class="sxs-lookup"><span data-stu-id="8a72e-333">The page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="8a72e-334">Il codice precedente usa *metodi gestore denominati*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-334">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="8a72e-335">I metodi gestore denominati vengono creati usando il testo che nel nome segue `On<HTTP Verb>` e precede `Async` (se presente).</span><span class="sxs-lookup"><span data-stu-id="8a72e-335">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="8a72e-336">Nell'esempio precedente i metodi della pagina sono OnPost**JoinList**Async e OnPost**JoinListUC**Async.</span><span class="sxs-lookup"><span data-stu-id="8a72e-336">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="8a72e-337">Rimuovendo *OnPost* e *Async*, i nomi dei gestori sono `JoinList` e `JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-337">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="8a72e-338">Usando il codice precedente, il percorso URL che indirizza a `OnPostJoinListAsync` è `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-338">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="8a72e-339">Il percorso URL che indirizza a `OnPostJoinListUCAsync` è `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-339">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>

## <a name="custom-routes"></a><span data-ttu-id="8a72e-340">Route personalizzate</span><span class="sxs-lookup"><span data-stu-id="8a72e-340">Custom routes</span></span>

<span data-ttu-id="8a72e-341">Usare la direttiva `@page` per:</span><span class="sxs-lookup"><span data-stu-id="8a72e-341">Use the `@page` directive to:</span></span>

* <span data-ttu-id="8a72e-342">Specificare una route personalizzata a una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-342">Specify a custom route to a page.</span></span> <span data-ttu-id="8a72e-343">Ad esempio, è possibile impostare la route alla pagina About (Informazioni) su `/Some/Other/Path` con `@page "/Some/Other/Path"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-343">For example, the route to the About page can be set to `/Some/Other/Path` with `@page "/Some/Other/Path"`.</span></span>
* <span data-ttu-id="8a72e-344">Aggiungere segmenti alla route predefinita di una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-344">Append segments to a page's default route.</span></span> <span data-ttu-id="8a72e-345">Ad esempio, è possibile aggiungere un segmento "item" alla route predefinita di una pagina con `@page "item"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-345">For example, an "item" segment can be added to a page's default route with `@page "item"`.</span></span>
* <span data-ttu-id="8a72e-346">Aggiungere parametri alla route predefinita di una pagina.</span><span class="sxs-lookup"><span data-stu-id="8a72e-346">Append parameters to a page's default route.</span></span> <span data-ttu-id="8a72e-347">Ad esempio, un parametro ID, `id`, può essere necessario per una pagina con `@page "{id}"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-347">For example, an ID parameter, `id`, can be required for a page with `@page "{id}"`.</span></span>

<span data-ttu-id="8a72e-348">Un percorso relativo alla directory radice designato da una tilde (`~`) all'inizio del percorso è supportato.</span><span class="sxs-lookup"><span data-stu-id="8a72e-348">A root-relative path designated by a tilde (`~`) at the beginning of the path is supported.</span></span> <span data-ttu-id="8a72e-349">Ad esempio, `@page "~/Some/Other/Path"` equivale a `@page "/Some/Other/Path"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-349">For example, `@page "~/Some/Other/Path"` is the same as `@page "/Some/Other/Path"`.</span></span>

<span data-ttu-id="8a72e-350">È possibile modificare la stringa di query `?handler=JoinList` nell'URL in un segmento di route `/JoinList` specificando il modello di route `@page "{handler?}"`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-350">You can change the query string `?handler=JoinList` in the URL to a route segment `/JoinList` by specifying the route template `@page "{handler?}"`.</span></span>

<span data-ttu-id="8a72e-351">Se si vuole omettere la stringa di query `?handler=JoinList` dall'URL, è possibile modificare la route in modo da inserire il nome del gestore nella parte di percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="8a72e-351">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="8a72e-352">È possibile personalizzare la route aggiungendo un modello di route racchiuso tra virgolette doppie dopo la direttiva `@page`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-352">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="8a72e-353">Usando il codice precedente, il percorso URL che indirizza a `OnPostJoinListAsync` è `http://localhost:5000/Customers/CreateFATH/JoinList`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-353">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH/JoinList`.</span></span> <span data-ttu-id="8a72e-354">Il percorso URL che indirizza a `OnPostJoinListUCAsync` è `http://localhost:5000/Customers/CreateFATH/JoinListUC`.</span><span class="sxs-lookup"><span data-stu-id="8a72e-354">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH/JoinListUC`.</span></span>

<span data-ttu-id="8a72e-355">`?` che segue `handler` indica che il parametro di route è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="8a72e-355">The `?` following `handler` means the route parameter is optional.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="8a72e-356">Configurazione e impostazioni</span><span class="sxs-lookup"><span data-stu-id="8a72e-356">Configuration and settings</span></span>

<span data-ttu-id="8a72e-357">Per configurare le opzioni avanzate, usare il metodo di estensione `AddRazorPagesOptions` nel generatore MVC:</span><span class="sxs-lookup"><span data-stu-id="8a72e-357">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="8a72e-358">Attualmente è possibile usare `RazorPagesOptions` per impostare la directory radice per le pagine o aggiungere convenzioni di modello applicativo per le pagine.</span><span class="sxs-lookup"><span data-stu-id="8a72e-358">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="8a72e-359">In questo modo si potrà garantire una maggiore estendibilità in futuro.</span><span class="sxs-lookup"><span data-stu-id="8a72e-359">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="8a72e-360">Per la precompilazione delle visualizzazioni, vedere l'articolo sulla [compilazione delle visualizzazioni Razor](xref:mvc/views/view-compilation).</span><span class="sxs-lookup"><span data-stu-id="8a72e-360">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="8a72e-361">[Scaricare o visualizzare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="8a72e-361">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).</span></span>

<span data-ttu-id="8a72e-362">Vedere [Introduzione a Razor Pages](xref:tutorials/razor-pages/razor-pages-start), che si basa su questa introduzione.</span><span class="sxs-lookup"><span data-stu-id="8a72e-362">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="8a72e-363">Specificare che Razor Pages si trova nella radice del contenuto</span><span class="sxs-lookup"><span data-stu-id="8a72e-363">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="8a72e-364">Per impostazione predefinita, la directory radice di Razor Pages è */Pages*.</span><span class="sxs-lookup"><span data-stu-id="8a72e-364">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="8a72e-365">Aggiungere [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) a [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) per specificare che Razor Pages è nella radice del contenuto ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) dell'app:</span><span class="sxs-lookup"><span data-stu-id="8a72e-365">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="8a72e-366">Specificare che Razor Pages è in una directory radice personalizzata</span><span class="sxs-lookup"><span data-stu-id="8a72e-366">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="8a72e-367">Aggiungere [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) a [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) per specificare che Razor Pages si trova in una directory radice personalizzata nell'app (fornire un percorso relativo):</span><span class="sxs-lookup"><span data-stu-id="8a72e-367">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="see-also"></a><span data-ttu-id="8a72e-368">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8a72e-368">See also</span></span>

* [<span data-ttu-id="8a72e-369">Introduzione a ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8a72e-369">Introduction to ASP.NET Core</span></span>](xref:index)
* [<span data-ttu-id="8a72e-370">Sintassi Razor</span><span class="sxs-lookup"><span data-stu-id="8a72e-370">Razor syntax</span></span>](xref:mvc/views/razor)
* [<span data-ttu-id="8a72e-371">Introduzione a Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-371">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="8a72e-372">Convenzioni di autorizzazione di Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-372">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
* [<span data-ttu-id="8a72e-373">Route personalizzata di Razor Pages e provider di modelli di pagina</span><span class="sxs-lookup"><span data-stu-id="8a72e-373">Razor Pages custom route and page model providers</span></span>](xref:razor-pages/razor-pages-conventions)
* [<span data-ttu-id="8a72e-374">Unit test per Razor Pages</span><span class="sxs-lookup"><span data-stu-id="8a72e-374">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)