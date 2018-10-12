---
title: Introduzione all'uso di pagine Razor in ASP.NET Core
author: rick-anderson
description: Questa serie di esercitazioni illustra come usare Razor Pages in ASP.NET Core. Offre informazioni su come creare un modello, generare codice per Razor Pages, usare Entity Framework Core e SQL Server per l'accesso ai dati, aggiungere funzionalità di ricerca, aggiungere la convalida dell'input e usare le migrazioni per aggiornare il modello.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 2e1c84a704856a22e1e105f56612194d4bb9c234
ms.sourcegitcommit: 599ebae5c2d6fcb22dfa6ae7d1f4bdfcacb79af4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47211000"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="5b6b3-104">Esercitazione: Introduzione all'uso di Razor Pages in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5b6b3-104">Tutorial: Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="5b6b3-105">Di [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5b6b3-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="5b6b3-106">È consigliabile usare la versione ASP.NET Core 2.1 di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-106">We recommend you follow the ASP.NET Core 2.1 version of this tutorial.</span></span> <span data-ttu-id="5b6b3-107">È **molto** più semplice da seguire e vengono illustrate più funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-107">It's **much** easier to follow and covers more features.</span></span> <span data-ttu-id="5b6b3-108">Selezionare **ASP.NET Core 2.1** nel selettore di versione.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-108">Select **ASP.NET Core 2.1** in the version selector.</span></span>

![Selettore di versione nel sommario](razor-pages-start/_static/v21.png)

::: moniker-end

<span data-ttu-id="5b6b3-110">Questa esercitazione illustra le nozioni di base della creazione di un'app Web pagine Razor di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-110">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="5b6b3-111">Le pagine Razor sono il modo consigliato per creare l'interfaccia utente per app Web in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-111">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="5b6b3-112">Sono disponibili tre versioni di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="5b6b3-112">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="5b6b3-113">Windows: questa esercitazione</span><span class="sxs-lookup"><span data-stu-id="5b6b3-113">Windows: This tutorial</span></span>
* <span data-ttu-id="5b6b3-114">MacOS: [Introduzione a pagine Razor con Visual Studio per Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="5b6b3-114">MacOS: [Get started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="5b6b3-115">macOS, Linux e Windows: [Introduzione a pagine Razor ASP.NET Core in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="5b6b3-115">macOS, Linux, and Windows: [Get started with ASP.NET Core Razor Pages in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="5b6b3-116">[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([procedura per il download](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5b6b3-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="prerequisites"></a><span data-ttu-id="5b6b3-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5b6b3-117">Prerequisites</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="5b6b3-118">Creare un'app Web Razor</span><span class="sxs-lookup"><span data-stu-id="5b6b3-118">Create a Razor web app</span></span>

* <span data-ttu-id="5b6b3-119">Dal menu **File** di Visual Studio selezionare **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-119">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="5b6b3-120">Creare una nuova applicazione Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-120">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="5b6b3-121">Denominare il progetto **RazorPagesMovie**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-121">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="5b6b3-122">È importante denominare il progetto *RazorPagesMovie* in modo che gli spazi dei nomi corrispondano nell'operazione di copia/incolla del codice.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-122">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="5b6b3-123">![nuova applicazione Web ASP.NET Core](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="5b6b3-123">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>
* <span data-ttu-id="5b6b3-124">Selezionare **ASP.NET Core 2.1** nell'elenco a discesa, quindi selezionare **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-124">Select **ASP.NET Core 2.1** in the dropdown, and then select **Web Application**.</span></span>

 ![nuova applicazione Web ASP.NET Core](razor-pages-start/_static/np_2_2.1.png)

<span data-ttu-id="5b6b3-126">Il modello di Visual Studio crea un progetto di avvio:</span><span class="sxs-lookup"><span data-stu-id="5b6b3-126">The Visual Studio template creates a starter project:</span></span>

![Esplora soluzioni](razor-pages-start/_static/se2.1.png)

<span data-ttu-id="5b6b3-128">Premere **F5** per eseguire l'app in modalità debug o **CTRL+F5** per eseguirla senza collegarsi al debugger.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-128">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span> <span data-ttu-id="5b6b3-129">Selezionare **Accept** (Accetto) per autorizzare il rilevamento.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-129">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="5b6b3-130">Questa app non rileva informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-130">This app doesn't track personal information.</span></span> <span data-ttu-id="5b6b3-131">Il codice generato del modello include asset che consentono di soddisfare il [Regolamento generale sulla protezione dei dati (GDPR)](xref:security/gdpr).</span><span class="sxs-lookup"><span data-stu-id="5b6b3-131">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

![Pagina Home o di indice](razor-pages-start/_static/homeGDPR.png)

<span data-ttu-id="5b6b3-133">La figura seguente illustra l'app dopo aver accettato il rilevamento:</span><span class="sxs-lookup"><span data-stu-id="5b6b3-133">The following image shows the app after accepting tracking:</span></span>

![Pagina Home o di indice](razor-pages-start/_static/home2.1.png)

* <span data-ttu-id="5b6b3-135">Visual Studio avvia [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) ed esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-135">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="5b6b3-136">La barra degli indirizzi visualizza `localhost:port#` e non `example.com` o simili.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-136">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="5b6b3-137">Ciò accade perché `localhost` è il nome host standard per il computer locale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-137">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="5b6b3-138">Localhost viene usato solo per le richieste web del computer locale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-138">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="5b6b3-139">Quando Visual Studio crea un progetto Web, per il server Web viene usata una porta casuale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-139">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="5b6b3-140">Nell'immagine precedente, il numero di porta è 5001.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-140">In the preceding image, the port number is 5001.</span></span> <span data-ttu-id="5b6b3-141">Quando si esegue l'app verrà visualizzato un numero di porta diverso.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-141">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="5b6b3-142">Se si avvia l'app con **CTRL+F5** (modalità non di debug) sarà possibile apportare modifiche al codice, salvare il file, aggiornare il browser e visualizzare le modifiche del codice.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-142">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="5b6b3-143">Molti sviluppatori preferiscono usare la modalità non di debug per avviare l'app rapidamente e visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-143">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

[!INCLUDE [F7](~/includes/RP/F7.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="prerequisites"></a><span data-ttu-id="5b6b3-144">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5b6b3-144">Prerequisites</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="5b6b3-145">Creare un'app Web Razor</span><span class="sxs-lookup"><span data-stu-id="5b6b3-145">Create a Razor web app</span></span>

* <span data-ttu-id="5b6b3-146">Dal menu **File** di Visual Studio selezionare **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-146">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="5b6b3-147">Creare una nuova applicazione Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-147">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="5b6b3-148">Denominare il progetto **RazorPagesMovie**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-148">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="5b6b3-149">È importante denominare il progetto *RazorPagesMovie* in modo che gli spazi dei nomi corrispondano nell'operazione di copia/incolla del codice.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-149">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="5b6b3-150">![nuova applicazione Web ASP.NET Core](../../razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="5b6b3-150">![new ASP.NET Core Web Application](../../razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="5b6b3-151">Selezionare **ASP.NET Core 2.0** nell'elenco a discesa, quindi selezionare **applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-151">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE [install 2.0](~/includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="5b6b3-152">Il modello di Visual Studio crea un progetto di avvio:</span><span class="sxs-lookup"><span data-stu-id="5b6b3-152">The Visual Studio template creates a starter project:</span></span>

![Esplora soluzioni](razor-pages-start/_static/se.png)

<span data-ttu-id="5b6b3-154">Premere **F5** per eseguire l'app in modalità di debug o **Ctrl-F5** per l'esecuzione senza collegamento del debugger</span><span class="sxs-lookup"><span data-stu-id="5b6b3-154">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![Pagina Home o di indice](razor-pages-start/_static/home.png)

* <span data-ttu-id="5b6b3-156">Visual Studio avvia [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) ed esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-156">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="5b6b3-157">La barra degli indirizzi visualizza `localhost:port#` e non `example.com` o simili.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-157">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="5b6b3-158">Ciò accade perché `localhost` è il nome host standard per il computer locale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-158">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="5b6b3-159">Localhost viene usato solo per le richieste web del computer locale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-159">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="5b6b3-160">Quando Visual Studio crea un progetto Web, per il server Web viene usata una porta casuale.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-160">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="5b6b3-161">Nell'immagine precedente, il numero di porta è 5000.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-161">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="5b6b3-162">Quando si esegue l'app verrà visualizzato un numero di porta diverso.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-162">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="5b6b3-163">Se si avvia l'app con **CTRL+F5** (modalità non di debug) sarà possibile apportare modifiche al codice, salvare il file, aggiornare il browser e visualizzare le modifiche del codice.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-163">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="5b6b3-164">Molti sviluppatori preferiscono usare la modalità non di debug per avviare l'app rapidamente e visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5b6b3-164">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/razor-pages-start.md)]

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="5b6b3-165">Avanti: Aggiunta di un modello</span><span class="sxs-lookup"><span data-stu-id="5b6b3-165">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
