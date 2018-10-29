---
title: Eseguire la migrazione da API Web ASP.NET ad ASP.NET Core
author: ardalis
description: Informazioni su come eseguire la migrazione di un'implementazione di API web dall'API Web ASP.NET 4.x ad ASP.NET Core MVC.
ms.author: scaddie
ms.custom: mvc
ms.date: 10/01/2018
uid: migration/webapi
ms.openlocfilehash: f5d886a7c3182b5cd372762ade67c2e748051049
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207277"
---
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a>Eseguire la migrazione da API Web ASP.NET ad ASP.NET Core

Dal [Scott Addie](https://twitter.com/scott_addie) e [Steve Smith](https://ardalis.com/)

Un'API Web ASP.NET 4.x è un servizio HTTP che raggiunge un'ampia gamma di client, inclusi browser e dispositivi mobili. Unifica di ASP.NET Core MVC di ASP.NET del 4.x e i modelli di app per le API Web in un modello di programmazione più semplice, noto come ASP.NET Core MVC. Questo articolo illustra i passaggi necessari per eseguire la migrazione dall'API Web ASP.NET 4.x ad ASP.NET Core MVC.

[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample) ([procedura per il download](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>Prerequisiti

* [.NET Core 2.1 SDK o versione successiva](https://www.microsoft.com/net/download/all)
* [Visual Studio 2017](https://www.visualstudio.com/downloads/) versione 15.7.3 o successive con il carico di lavoro **Sviluppo ASP.NET e Web**

## <a name="review-aspnet-4x-web-api-project"></a>Esaminare progetto API Web ASP.NET 4.x

Come punto di partenza, questo articolo usa il *ProductsApp* al progetto creato in [Introduzione a ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api). Nel progetto, un semplice progetto di API Web ASP.NET 4.x è configurato come indicato di seguito.

Nelle *Global.asax.cs*, viene effettuata una chiamata a `WebApiConfig.Register`:

[!code-csharp[](webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

`WebApiConfig` è definito nel *App_Start* cartella. Ha solo una riga statica `Register` metodo:

[!code-csharp[](webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15-20)]

Questa classe consente di configurare [routing con attributi](/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2), anche se non è effettivamente utilizzato nel progetto. Configura inoltre la tabella di routing, che viene usata da ASP.NET Web API. In questo caso, API Web ASP.NET 4.x prevede che gli URL in base al formato `/api/{controller}/{id}`, con `{id}` sia facoltativo.

Il *ProductsApp* progetto include un controller. Il controller eredita da `ApiController` ed espone due metodi:

[!code-csharp[](webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

Il `Product` modello utilizzato da `ProductsController` è una semplice classe:

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

Le sezioni seguenti illustrano la migrazione del progetto API Web ad ASP.NET Core MVC.

## <a name="create-destination-project"></a>Creare il progetto di destinazione

Completare i passaggi seguenti in Visual Studio:

* Passare a **File** > **nuova** > **progetto** > **altri tipi di progetto**  >  **Soluzioni di visual Studio**. Selezionare **soluzione vuota**e denominare la soluzione *WebAPIMigration*. Scegliere il **OK** pulsante.
* Aggiungi esistenti *ProductsApp* progetto alla soluzione.
* Aggiungere un nuovo **applicazione Web ASP.NET Core** progetto alla soluzione. Selezionare il **.NET Core** destinati a framework dall'elenco a discesa e selezionare il **API** modello di progetto. Denominare il progetto *ProductsCore*, fare clic sui **OK** pulsante.

A questo punto, la soluzione contiene due progetti. Le sezioni seguenti illustrano la migrazione di *ProductsApp* contenuto del progetto per il *ProductsCore* progetto.

## <a name="migrate-configuration"></a>La migrazione della configurazione

ASP.NET Core non usa la *App_Start* cartella o il *Global. asax* file e il *Web. config* file viene aggiunto al momento della pubblicazione. *Startup.cs* sostituisce la *Global. asax* e si trova nella radice del progetto. Il `Startup` classe gestisce tutte le attività di avvio di app. Per altre informazioni, vedere <xref:fundamentals/startup>.

In ASP.NET Core MVC, il routing con attributi è incluso per impostazione predefinita quando <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> viene chiamato `Startup.Configure`. Quanto segue `UseMvc` chiamare sostituisce il *ProductsApp* del progetto *App_Start/WebApiConfig.cs* file:

[!code-csharp[](webapi/sample/ProductsCore/Startup.cs?name=snippet_Configure&highlight=13])]

## <a name="migrate-models-and-controllers"></a>Eseguire la migrazione di modelli e controller

Copiare il *ProductApp* controller del progetto e il modello utilizzato. Attenersi ai passaggi riportati di seguito.

1. Copia *Controllers/ProductsController.cs* dal progetto originale a quello nuovo.
1. Copiare l'intera *modelli* cartella dal progetto originale a quello nuovo.
1. Modificare gli spazi dei nomi i file copiati in modo che corrisponda il nuovo nome del progetto (*ProductsCore*). Modificare il `using ProductsApp.Models;` istruzione nel *ProductsController.cs* troppo.

Compilazione a questo punto, i risultati per le app in un numero di errori di compilazione. Gli errori si verificano perché i componenti seguenti non esistono in ASP.NET Core:

* Classe `ApiController`
* Spazio dei nomi `System.Web.Http`
* `IHttpActionResult` Interfaccia

Correggere gli errori come indicato di seguito:

1. Change `ApiController` a <xref:Microsoft.AspNetCore.Mvc.ControllerBase>. Aggiungere `using Microsoft.AspNetCore.Mvc;` per risolvere il `ControllerBase` riferimento.
1. Eliminare `using System.Web.Http;`.
1. Modifica il `GetProduct` tipo restituito dell'azione dal `IHttpActionResult` a `ActionResult<Product>`.

## <a name="configure-routing"></a>Configurare il routing

Configurare il routing come indicato di seguito:

1. Decorare il `ProductsController` classe con gli attributi seguenti:

    ```csharp
    [Route("api/[controller]")]
    [ApiController]
    ```

    Precedente [[Route]](xref:Microsoft.AspNetCore.Mvc.RouteAttribute) attributo Configura modello di routing di attributi del controller. Il [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attributo rende il routing di un requisito per tutte le azioni in questo controller di attributo.

    Routing con attributi supporta i token, ad esempio `[controller]` e `[action]`. In fase di esecuzione, ogni token viene sostituito con il nome del controller o azione, rispettivamente, a cui è stato applicato l'attributo. I token di riducono il numero di "stringhe magiche" nel progetto. I token assicurarsi anche le route rimangano sincronizzate con i corrispondenti controller e azioni quando refactoring di ridenominazione automatica da applicare.
1. Abilitare le richieste HTTP Get per il `ProductController` azioni:
    * Si applicano i [[HttpGet]](xref:Microsoft.AspNetCore.Mvc.HttpGetAttribute) dell'attributo di `GetAllProducts` azione.
    * Si applicano i `[HttpGet("{id}")]` dell'attributo di `GetProduct` azione.

Dopo queste modifiche e la rimozione di inutilizzati `using` istruzioni *ProductsController.cs* file avrà un aspetto simile al seguente:

[!code-csharp[](webapi/sample/ProductsCore/Controllers/ProductsController.cs)]

Eseguire il progetto migrato e passare a `/api/products`. Viene visualizzato un elenco completo delle tre prodotti. Passare a `/api/products/1`. Viene visualizzato il primo prodotto.

## <a name="compatibility-shim"></a>Shim di compatibilità

Il [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) libreria fornisce uno shim di compatibilità per spostare i progetti API Web ASP.NET 4.x ad ASP.NET Core. Lo shim di compatibilità si estende a ASP.NET Core per supportare un numero di convenzioni da ASP.NET 4.x Web API 2. L'esempio trasferita in precedenza in questo documento è abbastanza semplice che non lo shim di compatibilità era necessario. Per progetti di grandi dimensioni usano lo shim di compatibilità può essere utile per temporaneamente colmare la lacuna API tra ASP.NET Core e ASP.NET 4.x Web API 2.

Lo shim di compatibilità delle API Web deve essere utilizzata come misura temporanea per supportare la migrazione grandi progetti ASP.NET 4.x API Web ad ASP.NET Core. Nel corso del tempo, i progetti devono essere aggiornati per usare i modelli ASP.NET Core anziché basarsi sullo shim di compatibilità.

Le funzionalità di compatibilità inclusi in `Microsoft.AspNetCore.Mvc.WebApiCompatShim` includono:

* Aggiunge un `ApiController` tipo in modo che i tipi di base di controller non devono essere aggiornati.
* Consente l'associazione del modello basato su Web API. ASP.NET Core MVC modellare le funzioni di associazione in modo analogo a quello di ASP.NET 4.x MVC 5, per impostazione predefinita. Le modifiche di shim di compatibilità del modello dell'associazione per essere più simile alle convenzioni dell'associazione del modello ASP.NET 4.x Web API 2. Ad esempio, i tipi complessi vengono associati automaticamente dal corpo della richiesta.
* Estende l'associazione di modelli in modo che le azioni del controller possono accettare parametri di tipo `HttpRequestMessage`.
* Aggiunge i formattatori dei messaggi che consente le azioni per restituire i risultati di tipo `HttpResponseMessage`.
* Aggiunge i metodi di risposta aggiuntivi che le azioni di API Web 2 potrebbero essere utilizzati per gestire le risposte:
  * `HttpResponseMessage` generatori di:
    * `CreateResponse<T>`
    * `CreateErrorResponse`
  * Metodi di azione risultati:
    * `BadRequestErrorMessageResult`
    * `ExceptionResult`
    * `InternalServerErrorResult`
    * `InvalidModelStateResult`
    * `NegotiatedContentResult`
    * `ResponseMessageResult`
* Aggiunge un'istanza di `IContentNegotiator` all'app del contenitore di inserimento delle dipendenze e rende disponibili i tipi correlati alla negoziazione del contenuto da [ASPNET](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/). Esempi di tali tipi `DefaultContentNegotiator` e `MediaTypeFormatter`.

Per usare lo shim di compatibilità:

1. Installare il [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) pacchetto NuGet.
1. Registrazione servizi dello shim di compatibilità con contenitore di inserimento delle dipendenze dell'app tramite la chiamata `services.AddMvc().AddWebApiConventions()` in `Startup.ConfigureServices`.
1. Definire web specifici dell'API instrada usando `MapWebApiRoute` nella `IRouteBuilder` dell'app `IApplicationBuilder.UseMvc` chiamare.

## <a name="additional-resources"></a>Risorse aggiuntive

* <xref:web-api/index>
* <xref:web-api/action-return-types>
