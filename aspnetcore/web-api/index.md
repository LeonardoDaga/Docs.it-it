---
title: Creare API Web con ASP.NET Core
author: scottaddie
description: Informazioni sulle funzionalità disponibili per la creazione di un'API Web in ASP.NET Core e su quando è appropriato usare ciascuna funzionalità.
ms.author: scaddie
ms.custom: mvc
ms.date: 08/15/2018
uid: web-api/index
ms.openlocfilehash: 763b95fb8ed3806bc67b7ad199153ea1027efa57
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090420"
---
# <a name="build-web-apis-with-aspnet-core"></a>Creare API Web con ASP.NET Core

Di [Scott Addie](https://github.com/scottaddie)

[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([procedura per il download](xref:tutorials/index#how-to-download-a-sample))

Questo documento illustra come creare un'API Web in ASP.NET Core e indica quando è più appropriato usare ciascuna funzionalità.

## <a name="derive-class-from-controllerbase"></a>Derivare una classe da ControllerBase

Ereditare dalla classe <xref:Microsoft.AspNetCore.Mvc.ControllerBase> in un controller progettato per svolgere la funzione di API Web. Ad esempio:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

La classe `ControllerBase` consente l'accesso a diverse proprietà e a svariati metodi. Nel codice precedente, <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> e <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)> sono due esempi. Questi metodi vengono chiamati all'interno di metodi di azioni per restituire rispettivamente i codici di stato HTTP 400 e HTTP 201. Alla proprietà <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState>, fornita anche questa da `ControllerBase`, si accede per gestire la convalida del modello di richiesta.

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a>Annotare una classe con l'attributo ApiController

ASP.NET Core 2.1 introduce l'attributo [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) per indicare una classe controller API Web. Ad esempio:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

Per usare questo attributo, è necessaria una versione di compatibilità di 2.1 o versioni successive impostata tramite <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>. Ad esempio, il codice evidenziato in *Startup.ConfigureServices* imposta il flag di compatibilità 2.2:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

Per ulteriori informazioni, vedere <xref:mvc/compatibility-version>.

L'attributo `[ApiController]` è in genere associato a `ControllerBase` per abilitare il comportamento specifico di REST per i controller. `ControllerBase` consente l'accesso a metodi quali <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> e <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*>.

Un altro approccio consiste nel creare una classe controller di base personalizzata annotata con l'attributo `[ApiController]`:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

Le sezioni seguenti descrivono le funzionalità aggiunte dall'attributo che favoriscono una maggiore praticità.

### <a name="problem-details-responses-for-error-status-codes"></a>Risposte con i dettagli del problema per i codici di stato di errore

ASP.NET Core 2.1 e versioni successive include [ProblemDetails](xref:Microsoft.AspNetCore.Mvc.ProblemDetails), un tipo basato sulla [specifica RFC 7807](https://tools.ietf.org/html/rfc7807). Il tipo `ProblemDetails` fornisce un formato standardizzato per trasmettere i dettagli leggibili dal computer degli errori in una risposta HTTP.

In ASP.NET Core 2.2 e versioni successive, MVC trasforma i risultati del codice di stato di errore (codice di stato 400 e versioni successive) in un risultato con `ProblemDetails`. Esaminare il codice seguente:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_ProblemDetails_StatusCode&highlight=4)]

La risposta HTTP per il risultato `NotFound` ha il codice di stato 404 con un corpo `ProblemDetails` analogo al seguente:

```js
{
    type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    title: "Not Found",
    status: 404,
    traceId: "0HLHLV31KRN83:00000001"
}
```

La funzionalità dei dettagli del problema richiede un flag di compatibilità pari a 2.2 o versione successiva. Il comportamento predefinito viene disabilitato quando la proprietà [SuppressMapClientErrors](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressMapClientErrors> --> è impostata su `true`. Il codice seguente evidenziato da `Startup.ConfigureServices` disabilita i dettagli del problema:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=8)]

Usare la proprietà [ClientErrorMapping](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.ClientErrorMapping> --> per configurare il contenuto della risposta `ProblemDetails`. Ad esempio, il codice seguente aggiorna la proprietà `type` per le risposte 404:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=10)]

### <a name="automatic-http-400-responses"></a>Risposte HTTP 400 automatiche

Gli errori di convalida attivano automaticamente una risposta HTTP 400. Il codice seguente non è più necessario nelle azioni:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

Usare <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> per personalizzare l'output della risposta prodotta.

Il comportamento predefinito viene disabilitato quando la proprietà <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> è impostata su `true`. Aggiungere il codice seguente in *Startup.ConfigureServices* dopo `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

Con un flag di compatibilità pari a 2.2 o versioni successive, il tipo di risposta predefinito restituito per le risposte 400 è un <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>. Usare la proprietà [SuppressUseValidationProblemDetailsForInvalidModelStateResponses](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressUseValidationProblemDetailsForInvalidModelStateResponses> --> per usare il formato di errore ASP.NET Core 2.1.

### <a name="binding-source-parameter-inference"></a>Inferenza del parametro di origine di associazione

Un attributo di origine di associazione definisce la posizione in cui viene trovato il valore del parametro di un'azione. Esistono gli attributi di origine di associazione seguente:

|Attributo|Origine di associazione |
|---------|---------|
|**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**     | Corpo della richiesta |
|**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**     | Dati di modulo nel corpo della richiesta |
|**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)** | Intestazione della richiesta |
|**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**   | Parametri della stringa di query della richiesta |
|**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**   | Dati della route della richiesta corrente |
|**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)** | Il servizio richiesta inserito come parametro di azione |

> [!WARNING]
> Non usare `[FromRoute]` quando i valori potrebbero contenere `%2f` (vale a dire `/`). `%2f` non sarà convertito in `/` rimuovendo i caratteri di escape. Usare `[FromQuery]` se il valore potrebbe contenere `%2f`.

Senza l'attributo `[ApiController]`, gli attributi di origine di associazione vengono definiti in modo esplicito. Nell'esempio seguente, l'attributo `[FromQuery]` indica che il valore del parametro `discontinuedOnly` è specificato nella stringa di query dell'URL della richiesta:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

Le regole di inferenza vengono applicate per le origini dati predefinite dei parametri di azione. Queste regole configurano le origini di associazione altrimenti applicate manualmente con ogni probabilità ai parametri di azione. Gli attributi di origine di associazione si comportano nel modo seguente:

* **[FromBody]**  viene dedotto per i parametri di tipo complesso. Un'eccezione a questa regola è costituita dai tipi predefiniti complessi con un significato speciale, ad esempio <xref:Microsoft.AspNetCore.Http.IFormCollection> e <xref:System.Threading.CancellationToken>. Il codice di inferenza di origine di associazione ignora tali tipi speciali. `[FromBody]` non viene dedotto per i tipi semplici, ad esempio `string` o `int`. Pertanto, l'attributo `[FromBody]` deve essere usato per i tipi semplici se si desidera tale funzionalità. Quando per un'azione esistono più parametri, specificati in modo esplicito (tramite `[FromBody]`) o dedotti in quanto associati dal corpo della richiesta, viene generata un'eccezione. Le firme di azione seguenti, ad esempio, causano un'eccezione:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* **[FromForm]** viene dedotto per i parametri di azione di tipo <xref:Microsoft.AspNetCore.Http.IFormFile> e <xref:Microsoft.AspNetCore.Http.IFormFileCollection>. Non viene dedotto per i tipi semplici o definiti dall'utente.
* **[FromRoute]**  viene dedotto per i nomi di parametro di azione corrispondenti a un parametro nel modello di route. Quando più di una route corrisponde a un parametro di azione, tutti i valori di route vengono considerati `[FromRoute]`.
* **[FromQuery]**  viene dedotto per tutti gli altri parametri di azione.

Le regole di inferenza predefinite vengono disabilitate quando la proprietà <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> è impostata su `true`. Aggiungere il codice seguente in *Startup.ConfigureServices* dopo `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a>Inferenza di richieste multipart/form-data

Quando un parametro di azione è annotato con l'attributo [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute), viene dedotto il tipo di contenuto `multipart/form-data` per la richiesta.

Il comportamento predefinito viene disabilitato quando la proprietà <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> è impostata su `true`. Aggiungere il codice seguente in *Startup.ConfigureServices* dopo `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a>Requisiti del routing degli attributi

Il routing degli attributi diventa un requisito. Ad esempio:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

Le azioni non sono accessibili tramite le [route convenzionali](xref:mvc/controllers/routing#conventional-routing) definite in <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> o da <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> in *Startup.Configure*.

::: moniker-end

## <a name="additional-resources"></a>Risorse aggiuntive

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>