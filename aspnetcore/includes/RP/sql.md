# <a name="work-with-sqlite-in-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="4015c-101">Usare SQLite in un'app ASP.NET Core Razor Pages</span><span class="sxs-lookup"><span data-stu-id="4015c-101">Work with SQLite in an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="4015c-102">Di [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4015c-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4015c-103">L'oggetto `MovieContext` gestisce l'attività di connessione al database e di mapping degli oggetti `Movie` ai record di database.</span><span class="sxs-lookup"><span data-stu-id="4015c-103">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="4015c-104">Il contesto del database viene registrato nel contenitore [Inserimento dipendenze](xref:fundamentals/dependency-injection) (DI) del metodo `ConfigureServices` nel file *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="4015c-104">The database context is registered with the [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](code/Startup.cs?name=snippet2&highlight=6-8)]

<span data-ttu-id="4015c-105">Per altre informazioni sull'uso di `DbContext` con Inserimento dipendenze, vedere [Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection) (Uso di DbContext con Inserimento dipendenze).</span><span class="sxs-lookup"><span data-stu-id="4015c-105">For more information on using `DbContext` with DI, see [Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection).</span></span>

## <a name="sqlite"></a><span data-ttu-id="4015c-106">SQLite</span><span class="sxs-lookup"><span data-stu-id="4015c-106">SQLite</span></span>

<span data-ttu-id="4015c-107">Nel sito Web di [SQLite](https://www.sqlite.org/) si dichiara:</span><span class="sxs-lookup"><span data-stu-id="4015c-107">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="4015c-108">SQLite è un motore di database SQL autonomo, a elevata affidabilità, incorporato, completo e di dominio pubblico.</span><span class="sxs-lookup"><span data-stu-id="4015c-108">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="4015c-109">SQLite è il motore di database più usato in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="4015c-109">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="4015c-110">Per gestire e visualizzare un database SQLite, sono disponibili numerosi strumenti di terze parti che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="4015c-110">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="4015c-111">L'immagine seguente è stata tratta da [DB Browser per SQLite](http://sqlitebrowser.org/).</span><span class="sxs-lookup"><span data-stu-id="4015c-111">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="4015c-112">Se si preferisce uno strumento SQLite in particolare, aggiungere un commento sui motivi della preferenza.</span><span class="sxs-lookup"><span data-stu-id="4015c-112">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![DB Browser for SQLite con il database dei film](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="4015c-114">Specificare il valore di inizializzazione del database</span><span class="sxs-lookup"><span data-stu-id="4015c-114">Seed the database</span></span>

<span data-ttu-id="4015c-115">Creare una nuova classe denominata `SeedData` nella cartella *Models*.</span><span class="sxs-lookup"><span data-stu-id="4015c-115">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="4015c-116">Sostituire il codice generato con il seguente:</span><span class="sxs-lookup"><span data-stu-id="4015c-116">Replace the generated code with the following:</span></span>

[!code-csharp[](code/Models/SeedData.cs)]

<span data-ttu-id="4015c-117">Se sono presenti film nel database, l'inizializzatore del valore di inizializzazione viene restituito.</span><span class="sxs-lookup"><span data-stu-id="4015c-117">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="4015c-118">Aggiungere l'inizializzatore del valore di inizializzazione</span><span class="sxs-lookup"><span data-stu-id="4015c-118">Add the seed initializer</span></span>

<span data-ttu-id="4015c-119">Aggiungere l'inizializzatore del valore di inizializzazione al metodo `Main` nel file *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="4015c-119">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Program.cs)]

### <a name="test-the-app"></a><span data-ttu-id="4015c-120">Eseguire il test dell'app</span><span class="sxs-lookup"><span data-stu-id="4015c-120">Test the app</span></span>

<span data-ttu-id="4015c-121">Eliminare tutti i record del database; verrà quindi eseguito il metodo di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="4015c-121">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="4015c-122">Arrestare e avviare l'app per inizializzare il database.</span><span class="sxs-lookup"><span data-stu-id="4015c-122">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="4015c-123">L'app mostra i dati inizializzati.</span><span class="sxs-lookup"><span data-stu-id="4015c-123">The app shows the seeded data.</span></span>
