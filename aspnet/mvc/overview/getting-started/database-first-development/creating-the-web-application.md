---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: "Database di Entity Framework prima di tutto con ASP.NET MVC: creazione dell'applicazione Web e i modelli di dati | Microsoft Docs"
author: Rick-Anderson
description: Usa MVC, Entity Framework e lo Scaffolding di ASP.NET, è possibile creare un'applicazione web che fornisce un'interfaccia a un database esistente. Questa esercitazione seri...
ms.author: riande
ms.date: 10/01/2014
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 6679b61326bd016481d96a4b5d58ec006f86b633
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020797"
---
<a name="ef-database-first-with-aspnet-mvc-creating-the-web-application-and-data-models"></a><span data-ttu-id="750d3-104">Database di Entity Framework prima di tutto con ASP.NET MVC: creazione dell'applicazione Web e i modelli di dati</span><span class="sxs-lookup"><span data-stu-id="750d3-104">EF Database First with ASP.NET MVC: Creating the Web Application and Data Models</span></span>
====================
<span data-ttu-id="750d3-105">da [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="750d3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="750d3-106">Usa MVC, Entity Framework e lo Scaffolding di ASP.NET, è possibile creare un'applicazione web che fornisce un'interfaccia a un database esistente.</span><span class="sxs-lookup"><span data-stu-id="750d3-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="750d3-107">Questa serie di esercitazioni illustra come generare il codice che consente agli utenti di visualizzare, modificare, creare automaticamente ed eliminare dati che si trovano in una tabella di database.</span><span class="sxs-lookup"><span data-stu-id="750d3-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="750d3-108">Il codice generato corrispondente alle colonne nella tabella di database.</span><span class="sxs-lookup"><span data-stu-id="750d3-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="750d3-109">Questa parte della serie è incentrato sulla creazione dell'applicazione web e la generazione di modelli di dati basati su tabelle di database.</span><span class="sxs-lookup"><span data-stu-id="750d3-109">This part of the series focuses on creating the web application, and generating the data models based on your database tables.</span></span>


## <a name="create-a-new-aspnet-web-application"></a><span data-ttu-id="750d3-110">Creare una nuova applicazione Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="750d3-110">Create a new ASP.NET Web Application</span></span>

<span data-ttu-id="750d3-111">In una nuova soluzione o la stessa soluzione come progetto di database, creare un nuovo progetto in Visual Studio e selezionare il **applicazione Web ASP.NET** modello.</span><span class="sxs-lookup"><span data-stu-id="750d3-111">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="750d3-112">Denominare il progetto **ContosoSite**.</span><span class="sxs-lookup"><span data-stu-id="750d3-112">Name the project **ContosoSite**.</span></span>

![Crea progetto](creating-the-web-application/_static/image1.png)

<span data-ttu-id="750d3-114">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="750d3-114">Click **OK**.</span></span>

<span data-ttu-id="750d3-115">Nella finestra Nuovo progetto ASP.NET, selezionare la **MVC** modello.</span><span class="sxs-lookup"><span data-stu-id="750d3-115">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="750d3-116">È possibile cancellare il **ospita nel cloud** opzione per il momento, perché si distribuirà l'applicazione nel cloud in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="750d3-116">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="750d3-117">Fare clic su **OK** per creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="750d3-117">Click **OK** to create the application.</span></span>

![Selezionare il modello mvc](creating-the-web-application/_static/image2.png)

<span data-ttu-id="750d3-119">Il progetto viene creato con i file predefiniti e le cartelle.</span><span class="sxs-lookup"><span data-stu-id="750d3-119">The project is created with the default files and folders.</span></span>

<span data-ttu-id="750d3-120">In questa esercitazione si userà Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="750d3-120">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="750d3-121">È possibile verificare la versione di Entity Framework nel progetto tramite la finestra Gestisci pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="750d3-121">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="750d3-122">Se necessario, aggiornare la versione di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="750d3-122">If necessary, update your version of Entity Framework.</span></span>

![Mostra versione](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="750d3-124">Genera i modelli</span><span class="sxs-lookup"><span data-stu-id="750d3-124">Generate the models</span></span>

<span data-ttu-id="750d3-125">Ora si creerà i modelli di Entity Framework dalle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="750d3-125">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="750d3-126">Questi modelli sono classi che si userà per lavorare con i dati.</span><span class="sxs-lookup"><span data-stu-id="750d3-126">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="750d3-127">Ogni modello riflette una tabella nel database e contiene proprietà che corrispondono alle colonne nella tabella.</span><span class="sxs-lookup"><span data-stu-id="750d3-127">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="750d3-128">Fare doppio clic il **modelli** cartella e selezionare **Add** e **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="750d3-128">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

![Aggiungi nuovo elemento](creating-the-web-application/_static/image4.png)

<span data-ttu-id="750d3-130">Nella finestra Aggiungi nuovo elemento, selezionare **Data** nel riquadro sinistro e **ADO.NET Entity Data Model** tra le opzioni nel riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="750d3-130">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="750d3-131">Denominare il nuovo file di modello **ContosoModel**.</span><span class="sxs-lookup"><span data-stu-id="750d3-131">Name the new model file **ContosoModel**.</span></span>

![Crea modello](creating-the-web-application/_static/image5.png)

<span data-ttu-id="750d3-133">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="750d3-133">Click **Add**.</span></span>

<span data-ttu-id="750d3-134">Nella procedura guidata Entity Data Model, selezionare **Entity Framework Designer da database**.</span><span class="sxs-lookup"><span data-stu-id="750d3-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

![Genera da database](creating-the-web-application/_static/image6.png)

<span data-ttu-id="750d3-136">Scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="750d3-136">Click **Next**.</span></span>

<span data-ttu-id="750d3-137">Se si dispone di connessioni di database definite all'interno dell'ambiente di sviluppo, si potrebbe vedere una di queste connessioni pre-selezionate.</span><span class="sxs-lookup"><span data-stu-id="750d3-137">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="750d3-138">Tuttavia, si desidera creare una nuova connessione al database creato nella prima parte di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="750d3-138">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="750d3-139">Scegliere il **nuova connessione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="750d3-139">Click the **New Connection** button.</span></span>

![connettersi al database](creating-the-web-application/_static/image7.png)

<span data-ttu-id="750d3-141">Nella finestra proprietà di connessione, specificare il nome del server locale in cui è stato creato il database (in questo caso **\ProjectsV12 (localdb)**).</span><span class="sxs-lookup"><span data-stu-id="750d3-141">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV12**).</span></span> <span data-ttu-id="750d3-142">Dopo aver specificato il nome del server, selezionare il ContosoUniversityData dai database di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="750d3-142">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![impostare le proprietà di connessione](creating-the-web-application/_static/image8.png)

<span data-ttu-id="750d3-144">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="750d3-144">Click **OK**.</span></span>

<span data-ttu-id="750d3-145">Sono ora visualizzate le proprietà di connessione corretta.</span><span class="sxs-lookup"><span data-stu-id="750d3-145">The correct connection properties are now displayed.</span></span> <span data-ttu-id="750d3-146">È possibile usare il nome predefinito per la connessione nel file Web. config</span><span class="sxs-lookup"><span data-stu-id="750d3-146">You can use the default name for connection in the Web.Config file</span></span>

![impostazioni di connessione](creating-the-web-application/_static/image9.png)

<span data-ttu-id="750d3-148">Scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="750d3-148">Click **Next**.</span></span>

<span data-ttu-id="750d3-149">Selezionare **tabelle** per generare modelli per tutte le tre tabelle.</span><span class="sxs-lookup"><span data-stu-id="750d3-149">Select **Tables** to generate models for all three tables.</span></span>

![Selezionare le tabelle](creating-the-web-application/_static/image10.png)

<span data-ttu-id="750d3-151">Scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="750d3-151">Click **Finish**.</span></span>

<span data-ttu-id="750d3-152">Se si riceve un avviso di sicurezza, selezionare **OK** per continuare l'esecuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="750d3-152">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="750d3-153">I modelli vengono generati dalle tabelle del database e viene visualizzato un diagramma che mostra le proprietà e relazioni tra le tabelle.</span><span class="sxs-lookup"><span data-stu-id="750d3-153">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![diagramma del modello](creating-the-web-application/_static/image11.png)

<span data-ttu-id="750d3-155">La cartella Models ora include molti nuovi file correlati ai modelli generati dal database.</span><span class="sxs-lookup"><span data-stu-id="750d3-155">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

![Mostra i nuovi file di modello](creating-the-web-application/_static/image12.png)

<span data-ttu-id="750d3-157">Il **ContosoModel.Context.cs** file contiene una classe che deriva dalle **DbContext** classe e fornisce una proprietà per ogni classe di modello che corrisponde a una tabella di database.</span><span class="sxs-lookup"><span data-stu-id="750d3-157">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="750d3-158">Il **Course.cs**, **Enrollment.cs**, e **Student.cs** file contengono le classi del modello che rappresentano le tabelle di database.</span><span class="sxs-lookup"><span data-stu-id="750d3-158">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="750d3-159">Si utilizzerà la classe del contesto sia le classi del modello quando si lavora con scaffolding.</span><span class="sxs-lookup"><span data-stu-id="750d3-159">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="750d3-160">Prima di procedere con questa esercitazione, compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="750d3-160">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="750d3-161">Nella sezione successiva, si genererà codice basato su modelli di data, ma tale sezione non funzionerà se non è stato compilato il progetto.</span><span class="sxs-lookup"><span data-stu-id="750d3-161">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="750d3-162">[Precedente](setting-up-database.md)
> [Successivo](generating-views.md)</span><span class="sxs-lookup"><span data-stu-id="750d3-162">[Previous](setting-up-database.md)
[Next](generating-views.md)</span></span>
