---
title: ASP.NET Core MVC con EF Core - Argomenti avanzati - 10 di 10
author: rick-anderson
description: Questa esercitazione presenta argomenti utili dopo aver appreso le nozioni di base sullo sviluppo di applicazioni Web ASP.NET Core che usano Entity Framework Core.
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/24/2018
uid: data/ef-mvc/advanced
ms.openlocfilehash: ba3834b29e78972bf914a5cba1a2cae3cc19a315
ms.sourcegitcommit: 184ba5b44d1c393076015510ac842b77bc9d4d93
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "50090784"
---
# <a name="aspnet-core-mvc-with-ef-core---advanced---10-of-10"></a><span data-ttu-id="19a7c-103">ASP.NET Core MVC con EF Core - Argomenti avanzati - 10 di 10</span><span class="sxs-lookup"><span data-stu-id="19a7c-103">ASP.NET Core MVC with EF Core - Advanced - 10 of 10</span></span>

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc-21.md)]

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="19a7c-104">Di [Tom Dykstra](https://github.com/tdykstra) e [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="19a7c-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="19a7c-105">L'applicazione Web di esempio Contoso University illustra come creare applicazioni Web ASP.NET Core MVC con Entity Framework Core e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19a7c-105">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="19a7c-106">Per informazioni sulla serie di esercitazioni, vedere la [prima esercitazione della serie](intro.md).</span><span class="sxs-lookup"><span data-stu-id="19a7c-106">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="19a7c-107">Nell'esercitazione precedente è stata implementata l'ereditarietà tabella per gerarchia.</span><span class="sxs-lookup"><span data-stu-id="19a7c-107">In the previous tutorial, you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="19a7c-108">Questa esercitazione presenta diversi argomenti che è utile tenere presente dopo aver appreso le nozioni di base sullo sviluppo di applicazioni Web ASP.NET Core che usano Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="19a7c-108">This tutorial introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET Core web applications that use Entity Framework Core.</span></span>

## <a name="raw-sql-queries"></a><span data-ttu-id="19a7c-109">Query SQL non elaborate</span><span class="sxs-lookup"><span data-stu-id="19a7c-109">Raw SQL Queries</span></span>

<span data-ttu-id="19a7c-110">Uno dei vantaggi dell'utilizzo di Entity Framework è la mancanza di un collegamento troppo stretto del codice a un particolare metodo di archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="19a7c-110">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="19a7c-111">Le query e i comandi SQL vengono generati automaticamente e non è necessario scriverli.</span><span class="sxs-lookup"><span data-stu-id="19a7c-111">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="19a7c-112">Esistono tuttavia alcuni scenari particolari in cui è necessario eseguire query SQL specifiche create manualmente.</span><span class="sxs-lookup"><span data-stu-id="19a7c-112">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created.</span></span> <span data-ttu-id="19a7c-113">Per questi scenari, l'API Code First di Entity Framework include metodi che consentono di passare i comandi SQL direttamente al database.</span><span class="sxs-lookup"><span data-stu-id="19a7c-113">For these scenarios, the Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="19a7c-114">In EF Core 1.0 sono possibili le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="19a7c-114">You have the following options in EF Core 1.0:</span></span>

* <span data-ttu-id="19a7c-115">Usare il metodo `DbSet.FromSql` per le query che restituiscono tipi di entità.</span><span class="sxs-lookup"><span data-stu-id="19a7c-115">Use the `DbSet.FromSql` method for queries that return entity types.</span></span> <span data-ttu-id="19a7c-116">Gli oggetti restituiti devono essere del tipo previsto dall'oggetto `DbSet` e vengono registrati automaticamente dal contesto del database a meno che non [venga disattivata la registrazione](crud.md#no-tracking-queries).</span><span class="sxs-lookup"><span data-stu-id="19a7c-116">The returned objects must be of the type expected by the `DbSet` object, and they're automatically tracked by the database context unless you [turn tracking off](crud.md#no-tracking-queries).</span></span>

* <span data-ttu-id="19a7c-117">Usare `Database.ExecuteSqlCommand` per i comandi non query.</span><span class="sxs-lookup"><span data-stu-id="19a7c-117">Use the `Database.ExecuteSqlCommand` for non-query commands.</span></span>

<span data-ttu-id="19a7c-118">Se è necessario eseguire una query che restituisca i tipi che non sono entità, è possibile usare ADO.NET con la connessione di database fornita da EF.</span><span class="sxs-lookup"><span data-stu-id="19a7c-118">If you need to run a query that returns types that aren't entities, you can use ADO.NET with the database connection provided by EF.</span></span> <span data-ttu-id="19a7c-119">I dati restituiti non vengono registrati dal contesto di database, anche se il metodo viene usato per recuperare i tipi di entità.</span><span class="sxs-lookup"><span data-stu-id="19a7c-119">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>

<span data-ttu-id="19a7c-120">Come avviene quando si eseguono comandi SQL in un'applicazione Web, è necessario adottare delle precauzioni per proteggere il sito dagli attacchi SQL injection.</span><span class="sxs-lookup"><span data-stu-id="19a7c-120">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="19a7c-121">A questo scopo è possibile usare query parametrizzate per assicurarsi che le stringhe inviate da una pagina Web non possano essere interpretate come comandi SQL.</span><span class="sxs-lookup"><span data-stu-id="19a7c-121">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="19a7c-122">In questa esercitazione verranno usate query parametrizzate quando l'input dell'utente viene integrato in una query.</span><span class="sxs-lookup"><span data-stu-id="19a7c-122">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

## <a name="call-a-query-that-returns-entities"></a><span data-ttu-id="19a7c-123">Chiamare una query che restituisce le entità</span><span class="sxs-lookup"><span data-stu-id="19a7c-123">Call a query that returns entities</span></span>

<span data-ttu-id="19a7c-124">La classe `DbSet<TEntity>` offre un metodo che è possibile usare per eseguire una query che restituisce un'entità di tipo `TEntity`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-124">The `DbSet<TEntity>` class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="19a7c-125">Per osservare questo funzionamento viene modificato il codice nel metodo `Details` del controller Department.</span><span class="sxs-lookup"><span data-stu-id="19a7c-125">To see how this works you'll change the code in the `Details` method of the Department controller.</span></span>

<span data-ttu-id="19a7c-126">In *DepartmentsController.cs* nel metodo `Details` sostituire il codice che recupera un reparto con una chiamata al metodo `FromSql`, come illustrato nel codice evidenziato seguente:</span><span class="sxs-lookup"><span data-stu-id="19a7c-126">In *DepartmentsController.cs*, in the `Details` method, replace the code that retrieves a department with a `FromSql` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_RawSQL&highlight=8,9,10,13)]

<span data-ttu-id="19a7c-127">Per verificare il corretto funzionamento del nuovo codice, selezionare la scheda **Departments** e quindi **Dettagli** per uno dei reparti.</span><span class="sxs-lookup"><span data-stu-id="19a7c-127">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![Dettagli del reparto](advanced/_static/department-details.png)

## <a name="call-a-query-that-returns-other-types"></a><span data-ttu-id="19a7c-129">Chiamare una query che restituisce altri tipi</span><span class="sxs-lookup"><span data-stu-id="19a7c-129">Call a query that returns other types</span></span>

<span data-ttu-id="19a7c-130">In precedenza è stata creata una griglia delle statistiche degli studenti per la pagina About che visualizza il numero di studenti per ogni data di registrazione.</span><span class="sxs-lookup"><span data-stu-id="19a7c-130">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="19a7c-131">I dati sono stati ottenuti dal set di entità Students (`_context.Students`) ed è stato usato LINQ per proiettare i risultati in un elenco degli oggetti del modello di visualizzazione `EnrollmentDateGroup`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-131">You got the data from the Students entity set (`_context.Students`) and used LINQ to project the results into a list of `EnrollmentDateGroup` view model objects.</span></span> <span data-ttu-id="19a7c-132">Si supponga di voler scrivere un codice SQL anziché usare LINQ.</span><span class="sxs-lookup"><span data-stu-id="19a7c-132">Suppose you want to write the SQL itself rather than using LINQ.</span></span> <span data-ttu-id="19a7c-133">A tale scopo è necessario eseguire una query SQL che restituisca elementi diversi dagli oggetti entità.</span><span class="sxs-lookup"><span data-stu-id="19a7c-133">To do that you need to run a SQL query that returns something other than entity objects.</span></span> <span data-ttu-id="19a7c-134">In EF Core 1.0 è possibile scrivere codice ADO.NET e ottenere la connessione di database da EF.</span><span class="sxs-lookup"><span data-stu-id="19a7c-134">In EF Core 1.0, one way to do that is write ADO.NET code and get the database connection from EF.</span></span>

<span data-ttu-id="19a7c-135">In *HomeController.cs* sostituire il metodo `About` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="19a7c-135">In *HomeController.cs*, replace the `About` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseRawSQL&highlight=3-32)]

<span data-ttu-id="19a7c-136">Aggiungere un'istruzione using:</span><span class="sxs-lookup"><span data-stu-id="19a7c-136">Add a using statement:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings2)]

<span data-ttu-id="19a7c-137">Eseguire l'app e passare alla pagina About.</span><span class="sxs-lookup"><span data-stu-id="19a7c-137">Run the app and go to the About page.</span></span> <span data-ttu-id="19a7c-138">Vengono visualizzati gli stessi dati visualizzati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="19a7c-138">It displays the same data it did before.</span></span>

![Pagina About](advanced/_static/about.png)

## <a name="call-an-update-query"></a><span data-ttu-id="19a7c-140">Chiamare una query di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="19a7c-140">Call an update query</span></span>

<span data-ttu-id="19a7c-141">Si supponga che gli amministratori di Contoso University vogliano eseguire modifiche globali nel database, ad esempio modificare il numero di crediti di ogni corso.</span><span class="sxs-lookup"><span data-stu-id="19a7c-141">Suppose Contoso University administrators want to perform global changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="19a7c-142">Se il numero di corsi dell'università è elevato, potrebbe non essere utile recuperarli tutti come entità e modificarli singolarmente.</span><span class="sxs-lookup"><span data-stu-id="19a7c-142">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="19a7c-143">In questa sezione viene implementata una pagina Web che consente all'utente di specificare un fattore in base al quale modificare il numero di crediti di tutti i corsi e viene apportata la modifica eseguendo un'istruzione SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="19a7c-143">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL UPDATE statement.</span></span> <span data-ttu-id="19a7c-144">La pagina Web apparirà come segue:</span><span class="sxs-lookup"><span data-stu-id="19a7c-144">The web page will look like the following illustration:</span></span>

![Pagina di aggiornamento dei crediti dei corsi](advanced/_static/update-credits.png)

<span data-ttu-id="19a7c-146">In *CoursesContoller.cs* aggiungere i metodi UpdateCourseCredits per HttpGet e HttpPost:</span><span class="sxs-lookup"><span data-stu-id="19a7c-146">In *CoursesContoller.cs*, add UpdateCourseCredits methods for HttpGet and HttpPost:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdateGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdatePost)]

<span data-ttu-id="19a7c-147">Quando il controller elabora una richiesta HttpGet, non viene restituito alcun elemento in `ViewData["RowsAffected"]` e la visualizzazione mostra una casella di testo vuota e un pulsante di invio, come illustrato nella figura precedente.</span><span class="sxs-lookup"><span data-stu-id="19a7c-147">When the controller processes an HttpGet request, nothing is returned in `ViewData["RowsAffected"]`, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="19a7c-148">Quando viene fatto clic sul pulsante **Aggiorna**, viene chiamato il metodo HttpPost e il moltiplicatore ha il valore immesso nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="19a7c-148">When the **Update** button is clicked, the HttpPost method is called, and multiplier has the value entered in the text box.</span></span> <span data-ttu-id="19a7c-149">Il codice esegue quindi l'SQL che aggiorna i corsi e restituisce il numero di righe interessate nella visualizzazione in `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-149">The code then executes the SQL that updates courses and returns the number of affected rows to the view in `ViewData`.</span></span> <span data-ttu-id="19a7c-150">Quando riceve un valore `RowsAffected`, la visualizzazione mostra il numero di righe aggiornate.</span><span class="sxs-lookup"><span data-stu-id="19a7c-150">When the view gets a `RowsAffected` value, it displays the number of rows updated.</span></span>

<span data-ttu-id="19a7c-151">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella *Views/Courses* e quindi fare clic su **Aggiungi > Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="19a7c-151">In **Solution Explorer**, right-click the *Views/Courses* folder, and then click **Add > New Item**.</span></span>

<span data-ttu-id="19a7c-152">Nella finestra di dialogo **Aggiungi nuovo elemento** fare clic su **ASP.NET** in **Installati** nel riquadro sinistro, fare clic su **Pagina visualizzazione MVC** e assegnare alla nuova visualizzazione il nome *UpdateCourseCredits.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="19a7c-152">In the **Add New Item** dialog, click **ASP.NET** under **Installed** in the left pane, click **MVC View Page**, and name the new view *UpdateCourseCredits.cshtml*.</span></span>

<span data-ttu-id="19a7c-153">In *Views/Courses/UpdateCourseCredits.cshtml* sostituire il codice del modello con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="19a7c-153">In *Views/Courses/UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-html[](intro/samples/cu/Views/Courses/UpdateCourseCredits.cshtml)]

<span data-ttu-id="19a7c-154">Eseguire il metodo `UpdateCourseCredits` selezionando la scheda **Courses**, quindi aggiungendo "/UpdateCourseCredits" alla fine dell'URL nella barra degli indirizzi del browser (ad esempio: `http://localhost:5813/Courses/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="19a7c-154">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:5813/Courses/UpdateCourseCredits`).</span></span> <span data-ttu-id="19a7c-155">Immettere un numero nella casella di testo:</span><span class="sxs-lookup"><span data-stu-id="19a7c-155">Enter a number in the text box:</span></span>

![Pagina di aggiornamento dei crediti dei corsi](advanced/_static/update-credits.png)

<span data-ttu-id="19a7c-157">Fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="19a7c-157">Click **Update**.</span></span> <span data-ttu-id="19a7c-158">Viene visualizzato il numero di righe interessate:</span><span class="sxs-lookup"><span data-stu-id="19a7c-158">You see the number of rows affected:</span></span>

![Righe interessate della pagina Update Course Credits](advanced/_static/update-credits-rows-affected.png)

<span data-ttu-id="19a7c-160">Fare clic su **Torna all'elenco** per visualizzare l'elenco dei corsi con il numero di crediti modificato.</span><span class="sxs-lookup"><span data-stu-id="19a7c-160">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="19a7c-161">Tenere presente che il codice di produzione assicurerà che gli aggiornamenti restituiscano sempre dati validi.</span><span class="sxs-lookup"><span data-stu-id="19a7c-161">Note that production code would ensure that updates always result in valid data.</span></span> <span data-ttu-id="19a7c-162">Il codice semplificato illustrato potrebbe moltiplicare il numero di crediti e restituire numeri maggiori di 5.</span><span class="sxs-lookup"><span data-stu-id="19a7c-162">The simplified code shown here could multiply the number of credits enough to result in numbers greater than 5.</span></span> <span data-ttu-id="19a7c-163">(La proprietà `Credits` ha un attributo `[Range(0, 5)]`). La query di aggiornamento funzionerebbe ma i dati non validi potrebbero causare risultati non previsti in altre parti del sistema che presuppongono che il numero di crediti sia 5 o un numero minore.</span><span class="sxs-lookup"><span data-stu-id="19a7c-163">(The `Credits` property has a `[Range(0, 5)]` attribute.) The update query would work but the invalid data could cause unexpected results in other parts of the system that assume the number of credits is 5 or less.</span></span>

<span data-ttu-id="19a7c-164">Per altre informazioni sulle query SQL non elaborate, vedere [Query SQL non elaborate](/ef/core/querying/raw-sql).</span><span class="sxs-lookup"><span data-stu-id="19a7c-164">For more information about raw SQL queries, see [Raw SQL Queries](/ef/core/querying/raw-sql).</span></span>

## <a name="examine-sql-sent-to-the-database"></a><span data-ttu-id="19a7c-165">Esaminare il codice SQL inviato al database</span><span class="sxs-lookup"><span data-stu-id="19a7c-165">Examine SQL sent to the database</span></span>

<span data-ttu-id="19a7c-166">A volte può essere utile visualizzare le query SQL inviate al database.</span><span class="sxs-lookup"><span data-stu-id="19a7c-166">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="19a7c-167">La funzionalità di registrazione incorporata di ASP.NET Core viene usata automaticamente da EF Core per creare i log contenenti il codice SQL di query e aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="19a7c-167">Built-in logging functionality for ASP.NET Core is automatically used by EF Core to write logs that contain the SQL for queries and updates.</span></span> <span data-ttu-id="19a7c-168">In questa sezione vengono presentati alcuni esempi di registrazione SQL.</span><span class="sxs-lookup"><span data-stu-id="19a7c-168">In this section you'll see some examples of SQL logging.</span></span>

<span data-ttu-id="19a7c-169">Aprire *StudentsController.cs* e nel metodo `Details` impostare un punto di interruzione nell'istruzione `if (student == null)`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-169">Open *StudentsController.cs* and in the `Details` method set a breakpoint on the `if (student == null)` statement.</span></span>

<span data-ttu-id="19a7c-170">Eseguire l'app in modalità di debug e passare alla pagina Details di uno studente.</span><span class="sxs-lookup"><span data-stu-id="19a7c-170">Run the app in debug mode, and go to the Details page for a student.</span></span>

<span data-ttu-id="19a7c-171">Passare alla finestra **Output** con l'output del debug per visualizzare la query:</span><span class="sxs-lookup"><span data-stu-id="19a7c-171">Go to the **Output** window showing debug output, and you see the query:</span></span>

```
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (56ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT TOP(2) [s].[ID], [s].[Discriminator], [s].[FirstName], [s].[LastName], [s].[EnrollmentDate]
FROM [Person] AS [s]
WHERE ([s].[Discriminator] = N'Student') AND ([s].[ID] = @__id_0)
ORDER BY [s].[ID]
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (122ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT [s.Enrollments].[EnrollmentID], [s.Enrollments].[CourseID], [s.Enrollments].[Grade], [s.Enrollments].[StudentID], [e.Course].[CourseID], [e.Course].[Credits], [e.Course].[DepartmentID], [e.Course].[Title]
FROM [Enrollment] AS [s.Enrollments]
INNER JOIN [Course] AS [e.Course] ON [s.Enrollments].[CourseID] = [e.Course].[CourseID]
INNER JOIN (
    SELECT TOP(1) [s0].[ID]
    FROM [Person] AS [s0]
    WHERE ([s0].[Discriminator] = N'Student') AND ([s0].[ID] = @__id_0)
    ORDER BY [s0].[ID]
) AS [t] ON [s.Enrollments].[StudentID] = [t].[ID]
ORDER BY [t].[ID]
```

<span data-ttu-id="19a7c-172">Si noti che il codice SQL seleziona un massimo di 2 righe (`TOP(2)`) dalla tabella Person.</span><span class="sxs-lookup"><span data-stu-id="19a7c-172">You'll notice something here that might surprise you: the SQL selects up to 2 rows (`TOP(2)`) from the Person table.</span></span> <span data-ttu-id="19a7c-173">Il metodo `SingleOrDefaultAsync` non viene risolto in 1 riga nel server.</span><span class="sxs-lookup"><span data-stu-id="19a7c-173">The `SingleOrDefaultAsync` method doesn't resolve to 1 row on the server.</span></span> <span data-ttu-id="19a7c-174">La ragione di questo comportamento è la seguente:</span><span class="sxs-lookup"><span data-stu-id="19a7c-174">Here's why:</span></span>

* <span data-ttu-id="19a7c-175">Se la query restituisse più righe, il metodo restituirebbe un valore Null.</span><span class="sxs-lookup"><span data-stu-id="19a7c-175">If the query would return multiple rows, the method returns null.</span></span>
* <span data-ttu-id="19a7c-176">Per determinare se la query restituirà più righe, EF deve controllare se restituisce almeno 2 righe.</span><span class="sxs-lookup"><span data-stu-id="19a7c-176">To determine whether the query would return multiple rows, EF has to check if it returns at least 2.</span></span>

<span data-ttu-id="19a7c-177">Si noti che non è necessario usare la modalità di debug e arrestarsi in un punto di interruzione per visualizzare l'output di registrazione nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="19a7c-177">Note that you don't have to use debug mode and stop at a breakpoint to get logging output in the **Output** window.</span></span> <span data-ttu-id="19a7c-178">Si tratta soltanto di un metodo pratico per arrestare la registrazione nel punto in cui si desidera visualizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="19a7c-178">It's just a convenient way to stop the logging at the point you want to look at the output.</span></span> <span data-ttu-id="19a7c-179">Se non si esegue questa operazione, la registrazione continua ed è necessario scorrere indietro per individuare le parti desiderate.</span><span class="sxs-lookup"><span data-stu-id="19a7c-179">If you don't do that, logging continues and you have to scroll back to find the parts you're interested in.</span></span>

## <a name="repository-and-unit-of-work-patterns"></a><span data-ttu-id="19a7c-180">Modelli di repository e unità di lavoro</span><span class="sxs-lookup"><span data-stu-id="19a7c-180">Repository and unit of work patterns</span></span>

<span data-ttu-id="19a7c-181">Molti sviluppatori scrivono codice per implementare i modelli di repository e unità di lavoro come wrapper per il codice usato con Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="19a7c-181">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="19a7c-182">Questi modelli sono progettati per la creazione di un livello di astrazione tra il livello di accesso ai dati e il livello della logica di business di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="19a7c-182">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="19a7c-183">L'implementazione di questi modelli può essere utile per isolare l'applicazione dalle modifiche nell'archivio dati e può semplificare il testing unità automatizzato o lo sviluppo basato su test (TDD).</span><span class="sxs-lookup"><span data-stu-id="19a7c-183">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="19a7c-184">Tuttavia, la scrittura di codice aggiuntivo per l'implementazione di questi modelli non è sempre la scelta migliore per le applicazioni che usano EF, per diverse ragioni:</span><span class="sxs-lookup"><span data-stu-id="19a7c-184">However, writing additional code to implement these patterns isn't always the best choice for applications that use EF, for several reasons:</span></span>

* <span data-ttu-id="19a7c-185">La classe del contesto EF isola il codice dal codice specifico dell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="19a7c-185">The EF context class itself insulates your code from data-store-specific code.</span></span>

* <span data-ttu-id="19a7c-186">La classe del contesto di EF può svolgere la funzione di classe di unità di lavoro per gli aggiornamenti di database eseguiti usando EF.</span><span class="sxs-lookup"><span data-stu-id="19a7c-186">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>

* <span data-ttu-id="19a7c-187">EF include funzionalità che consentono di implementare lo sviluppo basato su test senza scrivere codice di repository.</span><span class="sxs-lookup"><span data-stu-id="19a7c-187">EF includes features for implementing TDD without writing repository code.</span></span>

<span data-ttu-id="19a7c-188">Per informazioni su come implementare i modelli di repository e unità di lavoro, vedere [la versione Entity Framework 5 di questa serie di esercitazioni](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="19a7c-188">For information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span></span>

<span data-ttu-id="19a7c-189">Entity Framework Core implementa un provider di database in memoria che è possibile usare per il test.</span><span class="sxs-lookup"><span data-stu-id="19a7c-189">Entity Framework Core implements an in-memory database provider that can be used for testing.</span></span> <span data-ttu-id="19a7c-190">Per altre informazioni, vedere [Test con InMemory](/ef/core/miscellaneous/testing/in-memory).</span><span class="sxs-lookup"><span data-stu-id="19a7c-190">For more information, see [Test with InMemory](/ef/core/miscellaneous/testing/in-memory).</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="19a7c-191">Rilevamento automatico delle modifiche</span><span class="sxs-lookup"><span data-stu-id="19a7c-191">Automatic change detection</span></span>

<span data-ttu-id="19a7c-192">Entity Framework determina come è stata modificata un'entità (e di conseguenza gli aggiornamenti da inviare al database) confrontando i valori correnti di un'entità con i valori originali.</span><span class="sxs-lookup"><span data-stu-id="19a7c-192">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="19a7c-193">I valori originali vengono memorizzati quando viene eseguita una query sull'entità o quando viene collegata.</span><span class="sxs-lookup"><span data-stu-id="19a7c-193">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="19a7c-194">I metodi che causano il rilevamento automatico delle modifiche includono:</span><span class="sxs-lookup"><span data-stu-id="19a7c-194">Some of the methods that cause automatic change detection are the following:</span></span>

* <span data-ttu-id="19a7c-195">DbContext.SaveChanges</span><span class="sxs-lookup"><span data-stu-id="19a7c-195">DbContext.SaveChanges</span></span>

* <span data-ttu-id="19a7c-196">DbContext.Entry</span><span class="sxs-lookup"><span data-stu-id="19a7c-196">DbContext.Entry</span></span>

* <span data-ttu-id="19a7c-197">ChangeTracker.Entries</span><span class="sxs-lookup"><span data-stu-id="19a7c-197">ChangeTracker.Entries</span></span>

<span data-ttu-id="19a7c-198">Se viene registrato un numero elevato di entità e uno solo di questi metodi viene chiamato più volte in un ciclo, è possibile ottenere miglioramenti significativi delle prestazioni disattivando temporaneamente il rilevamento automatico delle modifiche usando la proprietà `ChangeTracker.AutoDetectChangesEnabled`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-198">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the `ChangeTracker.AutoDetectChangesEnabled` property.</span></span> <span data-ttu-id="19a7c-199">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="19a7c-199">For example:</span></span>

```csharp
_context.ChangeTracker.AutoDetectChangesEnabled = false;
```

## <a name="entity-framework-core-source-code-and-development-plans"></a><span data-ttu-id="19a7c-200">Codice sorgente e piani di sviluppo di Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="19a7c-200">Entity Framework Core source code and development plans</span></span>

<span data-ttu-id="19a7c-201">Il codice sorgente di Entity Framework Core è disponibile in [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span><span class="sxs-lookup"><span data-stu-id="19a7c-201">The Entity Framework Core source is at [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span></span> <span data-ttu-id="19a7c-202">Il repository di EF Core contiene le compilazioni notturne, la gestione dei problemi, le specifiche delle funzionalità, le note delle riunioni di progettazione e [la roadmap per lo sviluppo futuro](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap).</span><span class="sxs-lookup"><span data-stu-id="19a7c-202">The EF Core repository contains nightly builds, issue tracking, feature specs, design meeting notes, and [the roadmap for future development](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap).</span></span> <span data-ttu-id="19a7c-203">È possibile archiviare o individuare i bug e contribuire.</span><span class="sxs-lookup"><span data-stu-id="19a7c-203">You can file or find bugs, and contribute.</span></span>

<span data-ttu-id="19a7c-204">Sebbene il codice sorgente sia disponibile, Entity Framework Core è completamente supportato come prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19a7c-204">Although the source code is open, Entity Framework Core is fully supported as a Microsoft product.</span></span> <span data-ttu-id="19a7c-205">Il team di Microsoft Entity Framework controlla i contributi accettati ed esegue il test di tutte le modifiche al codice per garantire la qualità di ogni rilascio.</span><span class="sxs-lookup"><span data-stu-id="19a7c-205">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="reverse-engineer-from-existing-database"></a><span data-ttu-id="19a7c-206">Eseguire il reverse engineering dal database esistente</span><span class="sxs-lookup"><span data-stu-id="19a7c-206">Reverse engineer from existing database</span></span>

<span data-ttu-id="19a7c-207">Per eseguire il reverse engineering di un modello di dati contenente classi di entità da un database esistente, usare il comando [scaffold-dbcontext](/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="19a7c-207">To reverse engineer a data model including entity classes from an existing database, use the [scaffold-dbcontext](/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) command.</span></span> <span data-ttu-id="19a7c-208">Vedere l'[esercitazione introduttiva](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="19a7c-208">See the [getting-started tutorial](/ef/core/get-started/aspnetcore/existing-db).</span></span>

<a id="dynamic-linq"></a>
## <a name="use-dynamic-linq-to-simplify-sort-selection-code"></a><span data-ttu-id="19a7c-209">Usare LINQ dinamico per semplificare il codice di selezione dell'ordinamento</span><span class="sxs-lookup"><span data-stu-id="19a7c-209">Use dynamic LINQ to simplify sort selection code</span></span>

<span data-ttu-id="19a7c-210">La [terza esercitazione di questa serie](sort-filter-page.md) descrive come scrivere codice LINQ impostando come hardcoded i nomi di colonna in un'istruzione `switch`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-210">The [third tutorial in this series](sort-filter-page.md) shows how to write LINQ code by hard-coding column names in a `switch` statement.</span></span> <span data-ttu-id="19a7c-211">Se la selezione viene effettuata tra due colonne, il funzionamento è corretto, ma in presenza di numerose colonne il codice potrebbe diventare troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="19a7c-211">With two columns to choose from, this works fine, but if you have many columns the code could get verbose.</span></span> <span data-ttu-id="19a7c-212">Per risolvere il problema, è possibile usare il metodo `EF.Property` per specificare il nome della proprietà come stringa.</span><span class="sxs-lookup"><span data-stu-id="19a7c-212">To solve that problem, you can use the `EF.Property` method to specify the name of the property as a string.</span></span> <span data-ttu-id="19a7c-213">Per provare questo approccio, sostituire il metodo `Index` in `StudentsController` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="19a7c-213">To try out this approach, replace the `Index` method in the `StudentsController` with the following code.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DynamicLinq)]

## <a name="next-steps"></a><span data-ttu-id="19a7c-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19a7c-214">Next steps</span></span>

<span data-ttu-id="19a7c-215">Questa esercitazione completa la serie di esercitazioni sull'uso di Entity Framework Core in un'applicazione ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="19a7c-215">This completes this series of tutorials on using the Entity Framework Core in an ASP.NET Core MVC application.</span></span>

<span data-ttu-id="19a7c-216">Per altre informazioni su EF Core, vedere la [documentazione di Entity Framework Core](/ef/core).</span><span class="sxs-lookup"><span data-stu-id="19a7c-216">For more information about EF Core, see the [Entity Framework Core documentation](/ef/core).</span></span> <span data-ttu-id="19a7c-217">È disponibile anche un libro: [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span><span class="sxs-lookup"><span data-stu-id="19a7c-217">A book is also available: [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span></span>

<span data-ttu-id="19a7c-218">Per informazioni su come distribuire un'app Web, vedere <xref:host-and-deploy/index>.</span><span class="sxs-lookup"><span data-stu-id="19a7c-218">For information on how to deploy a web app, see <xref:host-and-deploy/index>.</span></span>

<span data-ttu-id="19a7c-219">Per informazioni su altri argomenti correlati ad ASP.NET Core MVC, ad esempio sull'autenticazione e l'autorizzazione, vedere <xref:index>.</span><span class="sxs-lookup"><span data-stu-id="19a7c-219">For information about other topics related to ASP.NET Core MVC, such as authentication and authorization, see <xref:index>.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="19a7c-220">Ringraziamenti</span><span class="sxs-lookup"><span data-stu-id="19a7c-220">Acknowledgments</span></span>

<span data-ttu-id="19a7c-221">Tom Dykstra e Rick Anderson (twitter @RickAndMSFT) hanno scritto questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="19a7c-221">Tom Dykstra and Rick Anderson (twitter @RickAndMSFT) wrote this tutorial.</span></span> <span data-ttu-id="19a7c-222">Rowan Miller, Diego Vega e altri membri del team Entity Framework hanno offerto supporto per le revisioni del codice e per il debug dei problemi sorti durante la scrittura del codice per le esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="19a7c-222">Rowan Miller, Diego Vega, and other members of the Entity Framework team assisted with code reviews and helped debug issues that arose while we were writing code for the tutorials.</span></span>

## <a name="common-errors"></a><span data-ttu-id="19a7c-223">Errori comuni</span><span class="sxs-lookup"><span data-stu-id="19a7c-223">Common errors</span></span>

### <a name="contosouniversitydll-used-by-another-process"></a><span data-ttu-id="19a7c-224">ContosoUniversity.dll usata da un altro processo</span><span class="sxs-lookup"><span data-stu-id="19a7c-224">ContosoUniversity.dll used by another process</span></span>

<span data-ttu-id="19a7c-225">Messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="19a7c-225">Error message:</span></span>

> <span data-ttu-id="19a7c-226">Impossibile aprire '...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' per la scrittura -- 'Il processo non può accedere al file '...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll' perché è in uso da un altro processo.</span><span class="sxs-lookup"><span data-stu-id="19a7c-226">Cannot open '...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' for writing -- 'The process cannot access the file '...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll' because it is being used by another process.</span></span>

<span data-ttu-id="19a7c-227">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="19a7c-227">Solution:</span></span>

<span data-ttu-id="19a7c-228">Arrestare il sito in IIS Express.</span><span class="sxs-lookup"><span data-stu-id="19a7c-228">Stop the site in IIS Express.</span></span> <span data-ttu-id="19a7c-229">Passare alla barra delle applicazioni di Windows, trovare IIS Express e fare clic con il pulsante destro del mouse sull'icona, selezionare il sito Contoso University e quindi fare clic su **Arresta sito**.</span><span class="sxs-lookup"><span data-stu-id="19a7c-229">Go to the Windows System Tray, find IIS Express and right-click its icon, select the Contoso University site, and then click **Stop Site**.</span></span>

### <a name="migration-scaffolded-with-no-code-in-up-and-down-methods"></a><span data-ttu-id="19a7c-230">Migrazione con scaffolding senza codice nei metodi Up e Down</span><span class="sxs-lookup"><span data-stu-id="19a7c-230">Migration scaffolded with no code in Up and Down methods</span></span>

<span data-ttu-id="19a7c-231">Possibile causa:</span><span class="sxs-lookup"><span data-stu-id="19a7c-231">Possible cause:</span></span>

<span data-ttu-id="19a7c-232">I comandi CLI di EF non chiudono e salvano automaticamente i file di codice.</span><span class="sxs-lookup"><span data-stu-id="19a7c-232">The EF CLI commands don't automatically close and save code files.</span></span> <span data-ttu-id="19a7c-233">Se sono presenti modifiche non salvate quando si esegue il comando `migrations add`, EF non trova le modifiche.</span><span class="sxs-lookup"><span data-stu-id="19a7c-233">If you have unsaved changes when you run the `migrations add` command, EF won't find your changes.</span></span>

<span data-ttu-id="19a7c-234">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="19a7c-234">Solution:</span></span>

<span data-ttu-id="19a7c-235">Eseguire il comando `migrations remove`, salvare le modifiche al codice e rieseguire il comando `migrations add`.</span><span class="sxs-lookup"><span data-stu-id="19a7c-235">Run the `migrations remove` command, save your code changes and rerun the `migrations add` command.</span></span>

### <a name="errors-while-running-database-update"></a><span data-ttu-id="19a7c-236">Errori durante l'esecuzione dell'aggiornamento del database</span><span class="sxs-lookup"><span data-stu-id="19a7c-236">Errors while running database update</span></span>

<span data-ttu-id="19a7c-237">Quando si apportano modifiche allo schema in un database con dati esistenti è possibile che si verifichino altri errori.</span><span class="sxs-lookup"><span data-stu-id="19a7c-237">It's possible to get other errors when making schema changes in a database that has existing data.</span></span> <span data-ttu-id="19a7c-238">Se si verificano errori di migrazione che non si riesce a risolvere, è possibile modificare il nome del database nella stringa di connessione o eliminare il database.</span><span class="sxs-lookup"><span data-stu-id="19a7c-238">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="19a7c-239">Un nuovo database non contiene dati di cui eseguire la migrazione e ci sono maggiori probabilità che il comando update-database venga completato senza errori.</span><span class="sxs-lookup"><span data-stu-id="19a7c-239">With a new database, there's no data to migrate, and the update-database command is much more likely to complete without errors.</span></span>

<span data-ttu-id="19a7c-240">L'approccio più semplice consiste nel rinominare il database in *appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="19a7c-240">The simplest approach is to rename the database in *appsettings.json*.</span></span> <span data-ttu-id="19a7c-241">Alla successiva esecuzione di `database update`, verrà creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="19a7c-241">The next time you run `database update`, a new database will be created.</span></span>

<span data-ttu-id="19a7c-242">Per eliminare un database in SSOX, fare clic con il pulsante destro del mouse sul database, fare clic su **Elimina** e quindi nella finestra di dialogo **Elimina database** selezionare **Chiudi connessioni esistenti** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="19a7c-242">To delete a database in SSOX, right-click the database, click **Delete**, and then in the **Delete Database** dialog box select **Close existing connections** and click **OK**.</span></span>

<span data-ttu-id="19a7c-243">Per eliminare un database tramite l'interfaccia CLI, eseguire il comando CLI `database drop`:</span><span class="sxs-lookup"><span data-stu-id="19a7c-243">To delete a database by using the CLI, run the `database drop` CLI command:</span></span>

```console
dotnet ef database drop
```

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="19a7c-244">Errore di individuazione dell'istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="19a7c-244">Error locating SQL Server instance</span></span>

<span data-ttu-id="19a7c-245">Messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="19a7c-245">Error Message:</span></span>

> <span data-ttu-id="19a7c-246">Si è verificato un errore di rete o specifico dell'istanza mentre si cercava di stabilire una connessione con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19a7c-246">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="19a7c-247">Il server non è stato trovato o non è accessibile.</span><span class="sxs-lookup"><span data-stu-id="19a7c-247">The server was not found or was not accessible.</span></span> <span data-ttu-id="19a7c-248">Verificare che il nome dell'istanza sia corretto e che SQL Server sia configurato in modo da consentire connessioni remote.</span><span class="sxs-lookup"><span data-stu-id="19a7c-248">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="19a7c-249">(provider: Interfacce di rete SQL, errore: 26 - Errore nell'individuazione del server/dell'istanza specificati)</span><span class="sxs-lookup"><span data-stu-id="19a7c-249">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="19a7c-250">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="19a7c-250">Solution:</span></span>

<span data-ttu-id="19a7c-251">Controllare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="19a7c-251">Check the connection string.</span></span> <span data-ttu-id="19a7c-252">Se il file di database è stato eliminato manualmente, modificare il nome del database nella stringa di costruzione per riniziare con un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="19a7c-252">If you have manually deleted the database file, change the name of the database in the construction string to start over with a new database.</span></span>

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="19a7c-253">Precedente</span><span class="sxs-lookup"><span data-stu-id="19a7c-253">Previous</span></span>](inheritance.md)
