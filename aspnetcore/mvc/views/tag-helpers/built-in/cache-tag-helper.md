---
title: Helper tag di cache in ASP.NET Core MVC
author: pkellner
description: Informazioni su come usare l'helper tag di cache.
ms.author: riande
ms.date: 02/14/2017
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: 11754d2858d8f02c7eb9baac8feda9b50ddb3d79
ms.sourcegitcommit: 4d5f8680d68b39c411b46c73f7014f8aa0f12026
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47028155"
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="45270-103">Helper tag di cache in ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="45270-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="45270-104">Di [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="45270-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="45270-105">L'helper tag di cache consente di migliorare notevolmente le prestazioni dell'app ASP.NET Core memorizzandone il contenuto nel provider di cache ASP.NET Core interno.</span><span class="sxs-lookup"><span data-stu-id="45270-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="45270-106">Il motore di visualizzazione Razor imposta il valore predefinito di `expires-after` su venti minuti.</span><span class="sxs-lookup"><span data-stu-id="45270-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="45270-107">Il seguente codice Razor memorizza nella cache la data/ora:</span><span class="sxs-lookup"><span data-stu-id="45270-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="45270-108">La prima richiesta della pagina che contiene `CacheTagHelper` visualizza la data/ora corrente.</span><span class="sxs-lookup"><span data-stu-id="45270-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="45270-109">Le richieste successive visualizzano il valore memorizzato nella cache fino a quando la cache scade (impostazione predefinita: 20 minuti) o viene rimossa da richieste d'uso della memoria.</span><span class="sxs-lookup"><span data-stu-id="45270-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="45270-110">È possibile impostare la durata della cache con i seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="45270-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="45270-111">Attributi dell'helper tag di cache</span><span class="sxs-lookup"><span data-stu-id="45270-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="45270-112">enabled</span><span class="sxs-lookup"><span data-stu-id="45270-112">enabled</span></span>    


| <span data-ttu-id="45270-113">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-113">Attribute Type</span></span>    | <span data-ttu-id="45270-114">Valori validi</span><span class="sxs-lookup"><span data-stu-id="45270-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="45270-115">boolean</span><span class="sxs-lookup"><span data-stu-id="45270-115">boolean</span></span>           | <span data-ttu-id="45270-116">"true" (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="45270-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="45270-117">"false"</span><span class="sxs-lookup"><span data-stu-id="45270-117">"false"</span></span>   |


<span data-ttu-id="45270-118">Determina se il contenuto incluso nell'helper tag di cache è memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="45270-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="45270-119">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="45270-119">The default is `true`.</span></span>  <span data-ttu-id="45270-120">Se impostato su `false` l'helper tag di cache non applica la memorizzazione nella cache all'output sottoposto a rendering.</span><span class="sxs-lookup"><span data-stu-id="45270-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="45270-121">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="45270-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="45270-122">expires-on</span></span> 

| <span data-ttu-id="45270-123">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-123">Attribute Type</span></span> |           <span data-ttu-id="45270-124">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-124">Example Value</span></span>            |
|----------------|------------------------------------|
| <span data-ttu-id="45270-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="45270-125">DateTimeOffset</span></span> | <span data-ttu-id="45270-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="45270-126">"@new DateTime(2025,1,29,17,02,0)"</span></span> |

<span data-ttu-id="45270-127">Imposta un'ora di scadenza assoluta.</span><span class="sxs-lookup"><span data-stu-id="45270-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="45270-128">Il codice di esempio seguente memorizza nella cache il contenuto dell'helper tag di cache fino alle 17:02 del 29 gennaio 2025.</span><span class="sxs-lookup"><span data-stu-id="45270-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="45270-129">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="45270-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="45270-130">expires-after</span></span>

| <span data-ttu-id="45270-131">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-131">Attribute Type</span></span> |        <span data-ttu-id="45270-132">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-132">Example Value</span></span>         |
|----------------|------------------------------|
|    <span data-ttu-id="45270-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45270-133">TimeSpan</span></span>    | <span data-ttu-id="45270-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="45270-134">"@TimeSpan.FromSeconds(120)"</span></span> |

<span data-ttu-id="45270-135">Imposta il tempo di memorizzazione del contenuto nella cache a partire dalla prima richiesta.</span><span class="sxs-lookup"><span data-stu-id="45270-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="45270-136">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="45270-137">expires-sliding</span><span class="sxs-lookup"><span data-stu-id="45270-137">expires-sliding</span></span>

| <span data-ttu-id="45270-138">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-138">Attribute Type</span></span> |        <span data-ttu-id="45270-139">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-139">Example Value</span></span>        |
|----------------|-----------------------------|
|    <span data-ttu-id="45270-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="45270-140">TimeSpan</span></span>    | <span data-ttu-id="45270-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="45270-141">"@TimeSpan.FromSeconds(60)"</span></span> |

<span data-ttu-id="45270-142">Imposta il tempo trascorso il quale un elemento memorizzato nella cache viene rimosso se non è stato usato.</span><span class="sxs-lookup"><span data-stu-id="45270-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="45270-143">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="45270-144">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="45270-144">vary-by-header</span></span>

| <span data-ttu-id="45270-145">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-145">Attribute Type</span></span>    | <span data-ttu-id="45270-146">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-147">Stringa</span><span class="sxs-lookup"><span data-stu-id="45270-147">String</span></span>            | <span data-ttu-id="45270-148">"User-Agent"</span><span class="sxs-lookup"><span data-stu-id="45270-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="45270-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="45270-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="45270-150">Accetta un valore di intestazione singolo o un elenco delimitato da virgole di valori di intestazione che attivano un aggiornamento della cache quando vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="45270-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="45270-151">L'esempio seguente esegue il monitoraggio del valore dell'intestazione `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="45270-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="45270-152">Il codice dell'esempio memorizza nella cache il contenuto di ogni singolo elemento `User-Agent` presentato al server Web.</span><span class="sxs-lookup"><span data-stu-id="45270-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="45270-153">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="45270-154">vary-by-query</span><span class="sxs-lookup"><span data-stu-id="45270-154">vary-by-query</span></span>

| <span data-ttu-id="45270-155">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-155">Attribute Type</span></span>    | <span data-ttu-id="45270-156">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-157">Stringa</span><span class="sxs-lookup"><span data-stu-id="45270-157">String</span></span>            | <span data-ttu-id="45270-158">"Make"</span><span class="sxs-lookup"><span data-stu-id="45270-158">"Make"</span></span>                |
|                   | <span data-ttu-id="45270-159">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="45270-159">"Make,Model"</span></span> |

<span data-ttu-id="45270-160">Accetta un valore di intestazione singolo o un elenco delimitato da virgole di valori di intestazione che attivano un aggiornamento della cache quando il valore dell'intestazione cambia.</span><span class="sxs-lookup"><span data-stu-id="45270-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="45270-161">Il codice dell'esempio seguente esamina i valori di `Make` e `Model`.</span><span class="sxs-lookup"><span data-stu-id="45270-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="45270-162">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="45270-163">vary-by-route</span><span class="sxs-lookup"><span data-stu-id="45270-163">vary-by-route</span></span>

| <span data-ttu-id="45270-164">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-164">Attribute Type</span></span>    | <span data-ttu-id="45270-165">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-166">Stringa</span><span class="sxs-lookup"><span data-stu-id="45270-166">String</span></span>            | <span data-ttu-id="45270-167">"Make"</span><span class="sxs-lookup"><span data-stu-id="45270-167">"Make"</span></span>                |
|                   | <span data-ttu-id="45270-168">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="45270-168">"Make,Model"</span></span> |

<span data-ttu-id="45270-169">Accetta un valore di intestazione singolo o un elenco delimitato da virgole di valori di intestazione che attivano un aggiornamento della cache quando il o i valori del parametro dati della route cambiano.</span><span class="sxs-lookup"><span data-stu-id="45270-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="45270-170">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-170">Example:</span></span>

<span data-ttu-id="45270-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="45270-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```

<span data-ttu-id="45270-172">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="45270-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="45270-173">vary-by-cookie</span><span class="sxs-lookup"><span data-stu-id="45270-173">vary-by-cookie</span></span>

| <span data-ttu-id="45270-174">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-174">Attribute Type</span></span>    | <span data-ttu-id="45270-175">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-176">Stringa</span><span class="sxs-lookup"><span data-stu-id="45270-176">String</span></span>            | <span data-ttu-id="45270-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="45270-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="45270-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="45270-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="45270-179">Accetta un valore di intestazione singolo o un elenco delimitato da virgole di valori di intestazione che attivano un aggiornamento della cache quando il o i valore dell'intestazione cambiano.</span><span class="sxs-lookup"><span data-stu-id="45270-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="45270-180">Il codice dell'esempio seguente esamina il cookie associato ad ASP.NET Core Identity.</span><span class="sxs-lookup"><span data-stu-id="45270-180">The following example looks at the cookie associated with ASP.NET Core Identity.</span></span> <span data-ttu-id="45270-181">Quando un utente è autenticato, questo è il cookie di richiesta da impostare per attivare un aggiornamento della cache.</span><span class="sxs-lookup"><span data-stu-id="45270-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="45270-182">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="45270-183">vary-by-user</span><span class="sxs-lookup"><span data-stu-id="45270-183">vary-by-user</span></span>

| <span data-ttu-id="45270-184">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-184">Attribute Type</span></span>    | <span data-ttu-id="45270-185">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-186">Booleano</span><span class="sxs-lookup"><span data-stu-id="45270-186">Boolean</span></span>             | <span data-ttu-id="45270-187">"true"</span><span class="sxs-lookup"><span data-stu-id="45270-187">"true"</span></span>                  |
|                     | <span data-ttu-id="45270-188">"false" (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="45270-188">"false" (default)</span></span> |

<span data-ttu-id="45270-189">Specifica se è necessario reimpostare la cache quando l'utente registrato (o l'entità di contesto registrata) cambia.</span><span class="sxs-lookup"><span data-stu-id="45270-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="45270-190">L'utente corrente è detto anche entità di sicurezza del contesto della richiesta e può essere visualizzato in una visualizzazione Razor mediante riferimento a `@User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="45270-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="45270-191">Il codice dell'esempio seguente esamina l'utente corrente registrato.</span><span class="sxs-lookup"><span data-stu-id="45270-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="45270-192">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="45270-193">Questo attributo consente di mantenere il contenuto nella cache durante un ciclo di accesso e chiusura sessione.</span><span class="sxs-lookup"><span data-stu-id="45270-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="45270-194">Quando si usa `vary-by-user="true"` un'azione di accesso e chiusura sessione invalida la cache per l'utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="45270-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="45270-195">La cache viene invalidata perché al momento dell'accesso viene generato un nuovo valore di cookie univoco.</span><span class="sxs-lookup"><span data-stu-id="45270-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="45270-196">La cache viene mantenuta per lo stato anonimo se non è presente nessun cookie o il cookie è scaduto.</span><span class="sxs-lookup"><span data-stu-id="45270-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="45270-197">Ciò significa che se nessun utente ha eseguito l'accesso la cache viene mantenuta.</span><span class="sxs-lookup"><span data-stu-id="45270-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="45270-198">vary-by</span><span class="sxs-lookup"><span data-stu-id="45270-198">vary-by</span></span>

| <span data-ttu-id="45270-199">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-199">Attribute Type</span></span> | <span data-ttu-id="45270-200">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-200">Example Values</span></span> |
|----------------|----------------|
|     <span data-ttu-id="45270-201">Stringa</span><span class="sxs-lookup"><span data-stu-id="45270-201">String</span></span>     |    <span data-ttu-id="45270-202">"@Model"</span><span class="sxs-lookup"><span data-stu-id="45270-202">"@Model"</span></span>    |

<span data-ttu-id="45270-203">Consente di personalizzare quali dati vengono memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="45270-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="45270-204">Quando l'oggetto al quale fa riferimento il valore stringa dell'attributo cambia, il contenuto dell'helper tag di cache viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="45270-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="45270-205">Spesso a questo attributo viene assegnata una concatenazione stringa di valori del modello.</span><span class="sxs-lookup"><span data-stu-id="45270-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="45270-206">Di fatto ciò significa che l'aggiornamento di uno qualsiasi dei valori concatenati invalida la cache.</span><span class="sxs-lookup"><span data-stu-id="45270-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="45270-207">L'esempio seguente presuppone che il metodo del controller che esegue il rendering della vista effettui la somma dei valori interi dei due parametri di route `myParam1` e `myParam2` e restituisca la somma come proprietà singola del modello.</span><span class="sxs-lookup"><span data-stu-id="45270-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="45270-208">Quando questa somma cambia, il contenuto dell'helper tag di cache viene sottoposto a rendering e memorizzato di nuovo nella cache.</span><span class="sxs-lookup"><span data-stu-id="45270-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="45270-209">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-209">Example:</span></span>

<span data-ttu-id="45270-210">Azione:</span><span class="sxs-lookup"><span data-stu-id="45270-210">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="45270-211">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="45270-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="45270-212">priority</span><span class="sxs-lookup"><span data-stu-id="45270-212">priority</span></span>

| <span data-ttu-id="45270-213">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="45270-213">Attribute Type</span></span>    | <span data-ttu-id="45270-214">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="45270-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="45270-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="45270-215">CacheItemPriority</span></span>  | <span data-ttu-id="45270-216">"High"</span><span class="sxs-lookup"><span data-stu-id="45270-216">"High"</span></span>                   |
|                    | <span data-ttu-id="45270-217">"Low"</span><span class="sxs-lookup"><span data-stu-id="45270-217">"Low"</span></span> |
|                    | <span data-ttu-id="45270-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="45270-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="45270-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="45270-219">"Normal"</span></span> |

<span data-ttu-id="45270-220">Offre indicazioni per la rimozione dalla cache al provider di cache incorporato.</span><span class="sxs-lookup"><span data-stu-id="45270-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="45270-221">Se sottoposto a richieste di memoria intensive, il server Web rimuove inizialmente `Low` voci della cache.</span><span class="sxs-lookup"><span data-stu-id="45270-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="45270-222">Esempio:</span><span class="sxs-lookup"><span data-stu-id="45270-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="45270-223">L'attributo `priority` non garantisce un livello specifico di mantenimento nella cache.</span><span class="sxs-lookup"><span data-stu-id="45270-223">The `priority` attribute doesn't guarantee a specific level of cache retention.</span></span> <span data-ttu-id="45270-224">`CacheItemPriority` è un semplice suggerimento.</span><span class="sxs-lookup"><span data-stu-id="45270-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="45270-225">L'impostazione dell'attributo su `NeverRemove` non garantisce che la cache verrà sempre mantenuta.</span><span class="sxs-lookup"><span data-stu-id="45270-225">Setting this attribute to `NeverRemove` doesn't guarantee that the cache will always be retained.</span></span> <span data-ttu-id="45270-226">Per altre informazioni, vedere [Risorse aggiuntive](#additional-resources).</span><span class="sxs-lookup"><span data-stu-id="45270-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="45270-227">L'helper tag di cache dipende dal [servizio cache in memoria](xref:performance/caching/memory).</span><span class="sxs-lookup"><span data-stu-id="45270-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="45270-228">L'helper tag di cache aggiunge il servizio se non è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="45270-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45270-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="45270-229">Additional resources</span></span>

* [<span data-ttu-id="45270-230">Cache in memoria</span><span class="sxs-lookup"><span data-stu-id="45270-230">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="45270-231">Introduzione a Identity</span><span class="sxs-lookup"><span data-stu-id="45270-231">Introduction to Identity</span></span>](xref:security/authentication/identity)
