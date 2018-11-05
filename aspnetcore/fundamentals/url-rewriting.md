---
title: Middleware Riscrittura URL in ASP.NET Core
author: guardrex
description: Informazioni sulla riscrittura e il reindirizzamento di URL con il middleware Riscrittura URL nelle applicazioni ASP.NET Core.
ms.author: riande
ms.date: 08/17/2017
uid: fundamentals/url-rewriting
ms.openlocfilehash: 5a1891c838436467fb49ff6288587fab08201179
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207186"
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a><span data-ttu-id="33d9a-103">Middleware Riscrittura URL in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="33d9a-103">URL Rewriting Middleware in ASP.NET Core</span></span>

<span data-ttu-id="33d9a-104">Di [Luke Latham](https://github.com/guardrex) e [Mikael Mengistu](https://github.com/mikaelm12)</span><span class="sxs-lookup"><span data-stu-id="33d9a-104">By [Luke Latham](https://github.com/guardrex) and [Mikael Mengistu](https://github.com/mikaelm12)</span></span>

<span data-ttu-id="33d9a-105">[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/) ([procedura per il download](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="33d9a-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="33d9a-106">La riscrittura URL è l'azione di modificare gli URL di richiesta in base a una o più regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="33d9a-106">URL rewriting is the act of modifying request URLs based on one or more predefined rules.</span></span> <span data-ttu-id="33d9a-107">Il processo di riscrittura URL crea un'astrazione tra i percorsi delle risorse e i relativi indirizzi, in modo che i percorsi e gli indirizzi non risultino strettamente collegati.</span><span class="sxs-lookup"><span data-stu-id="33d9a-107">URL rewriting creates an abstraction between resource locations and their addresses so that the locations and addresses are not tightly linked.</span></span> <span data-ttu-id="33d9a-108">La riscrittura URL risulta utile in diversi scenari:</span><span class="sxs-lookup"><span data-stu-id="33d9a-108">There are several scenarios where URL rewriting is valuable:</span></span>

* <span data-ttu-id="33d9a-109">Spostamento o sostituzione temporanea o permanente di risorse server pur mantenendo localizzatori stabili di queste risorse.</span><span class="sxs-lookup"><span data-stu-id="33d9a-109">Moving or replacing server resources temporarily or permanently while maintaining stable locators for those resources.</span></span>
* <span data-ttu-id="33d9a-110">Suddivisione dell'elaborazione delle richieste tra diverse app o tra diverse aree di un'unica app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-110">Splitting request processing across different apps or across areas of one app.</span></span>
* <span data-ttu-id="33d9a-111">Rimozione, aggiunta o riorganizzazione di segmenti URL nelle richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="33d9a-111">Removing, adding, or reorganizing URL segments on incoming requests.</span></span>
* <span data-ttu-id="33d9a-112">Ottimizzazione degli URL pubblici per l'ottimizzazione motore di ricerca (SEO, Search Engine Optimization).</span><span class="sxs-lookup"><span data-stu-id="33d9a-112">Optimizing public URLs for Search Engine Optimization (SEO).</span></span>
* <span data-ttu-id="33d9a-113">Autorizzazione dell'uso di URL pubblici brevi per consentire agli utenti di prevedere il contenuto trovato seguendo un collegamento.</span><span class="sxs-lookup"><span data-stu-id="33d9a-113">Permitting the use of friendly public URLs to help people predict the content they will find by following a link.</span></span>
* <span data-ttu-id="33d9a-114">Reindirizzamento delle richieste non protette a endpoint protetti.</span><span class="sxs-lookup"><span data-stu-id="33d9a-114">Redirecting insecure requests to secure endpoints.</span></span>
* <span data-ttu-id="33d9a-115">Blocco dell'hotlinking di immagini.</span><span class="sxs-lookup"><span data-stu-id="33d9a-115">Preventing image hotlinking.</span></span>

<span data-ttu-id="33d9a-116">È possibile definire regole per la modifica dell'URL con diverse modalità, tra cui Regex, le regole di modulo Apache mod_rewrite, le regole di modulo IIS Rewrite e l'uso di logica delle regole personalizzata.</span><span class="sxs-lookup"><span data-stu-id="33d9a-116">You can define rules for changing the URL in several ways, including Regex, Apache mod_rewrite module rules, IIS Rewrite Module rules, and using custom rule logic.</span></span> <span data-ttu-id="33d9a-117">Questo documento presenta la riscrittura URL con istruzioni per l'uso del middleware Riscrittura URL nelle applicazioni ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="33d9a-117">This document introduces URL rewriting with instructions on how to use URL Rewriting Middleware in ASP.NET Core apps.</span></span>

> [!NOTE]
> <span data-ttu-id="33d9a-118">La riscrittura URL può ridurre le prestazioni di un'app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-118">URL rewriting can reduce the performance of an app.</span></span> <span data-ttu-id="33d9a-119">Ove possibile, limitare il numero e la complessità delle regole.</span><span class="sxs-lookup"><span data-stu-id="33d9a-119">Where feasible, you should limit the number and complexity of rules.</span></span>

## <a name="url-redirect-and-url-rewrite"></a><span data-ttu-id="33d9a-120">Reindirizzamento URL e riscrittura URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-120">URL redirect and URL rewrite</span></span>

<span data-ttu-id="33d9a-121">La differenza tra i termini *reindirizzamento URL* e *riscrittura URL* può apparire minima, ma ha implicazioni importanti nell'offerta di risorse ai clienti.</span><span class="sxs-lookup"><span data-stu-id="33d9a-121">The difference in wording between *URL redirect* and *URL rewrite* may seem subtle at first but has important implications for providing resources to clients.</span></span> <span data-ttu-id="33d9a-122">Il middleware Riscrittura URL di ASP.NET Core è in grado di svolgere entrambe le funzioni.</span><span class="sxs-lookup"><span data-stu-id="33d9a-122">ASP.NET Core's URL Rewriting Middleware is capable of meeting the need for both.</span></span>

<span data-ttu-id="33d9a-123">Un *reindirizzamento URL* è un'operazione lato client, in cui viene richiesto al client di accedere a una risorsa a un altro indirizzo.</span><span class="sxs-lookup"><span data-stu-id="33d9a-123">A *URL redirect* is a client-side operation, where the client is instructed to access a resource at another address.</span></span> <span data-ttu-id="33d9a-124">Questa operazione richiede una sequenza di andata e ritorno al server.</span><span class="sxs-lookup"><span data-stu-id="33d9a-124">This requires a round-trip to the server.</span></span> <span data-ttu-id="33d9a-125">L'URL di reindirizzamento restituito al client viene visualizzato nella barra degli indirizzi del browser quando il client effettua una nuova richiesta per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="33d9a-125">The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</span></span> 

<span data-ttu-id="33d9a-126">Se `/resource` viene *reindirizzato* a `/different-resource` il client richiede `/resource`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-126">If `/resource` is *redirected* to `/different-resource`, the client requests `/resource`.</span></span> <span data-ttu-id="33d9a-127">Il server risponde che il client deve ottenere la risorsa in `/different-resource` con un codice di stato che indica se il reindirizzamento è temporaneo o permanente.</span><span class="sxs-lookup"><span data-stu-id="33d9a-127">The server responds that the client should obtain the resource at `/different-resource` with a status code indicating that the redirect is either temporary or permanent.</span></span> <span data-ttu-id="33d9a-128">Il client esegue una nuova richiesta per la risorsa all'URL di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="33d9a-128">The client executes a new request for the resource at the redirect URL.</span></span>

![Un endpoint di servizio WebAPI è stato modificato temporaneamente dalla versione 1 (v1) alla versione 2 (v2) nel server.](url-rewriting/_static/url_redirect.png)

<span data-ttu-id="33d9a-134">Quando si reindirizzano le richieste a un URL diverso, indicare se il reindirizzamento è temporaneo o permanente.</span><span class="sxs-lookup"><span data-stu-id="33d9a-134">When redirecting requests to a different URL, you indicate whether the redirect is permanent or temporary.</span></span> <span data-ttu-id="33d9a-135">Il codice di stato 301 (Spostato permanentemente) viene usato se la risorsa ha un nuovo URL definitivo e si vuole indicare al client che tale URL dovrà essere usato per tutte le richieste future della risorsa.</span><span class="sxs-lookup"><span data-stu-id="33d9a-135">The 301 (Moved Permanently) status code is used where the resource has a new, permanent URL and you wish to instruct the client that all future requests for the resource should use the new URL.</span></span> <span data-ttu-id="33d9a-136">*Quando riceve un codice di stato 301 il client può memorizzare la risposta nella cache.*</span><span class="sxs-lookup"><span data-stu-id="33d9a-136">*The client may cache the response when a 301 status code is received.*</span></span> <span data-ttu-id="33d9a-137">Il codice di stato 302 (Trovato) viene usato quando il reindirizzamento è temporaneo o comunque soggetto a modifiche, in modo che il client non dovrà archiviare e riusare l'URL di reindirizzamento in futuro.</span><span class="sxs-lookup"><span data-stu-id="33d9a-137">The 302 (Found) status code is used where the redirection is temporary or generally subject to change, such that the client shouldn't store and reuse the redirect URL in the future.</span></span> <span data-ttu-id="33d9a-138">Per altre informazioni, vedere [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) (RFC 2616: Definizioni dei codici di stato).</span><span class="sxs-lookup"><span data-stu-id="33d9a-138">For more information, see [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

<span data-ttu-id="33d9a-139">Una *riscrittura URL* è un'operazione lato server che rende disponibile una risorsa da un indirizzo risorsa alternativo.</span><span class="sxs-lookup"><span data-stu-id="33d9a-139">A *URL rewrite* is a server-side operation to provide a resource from a different resource address.</span></span> <span data-ttu-id="33d9a-140">La riscrittura URL non richiede una sequenza di andata e ritorno al server.</span><span class="sxs-lookup"><span data-stu-id="33d9a-140">Rewriting a URL doesn't require a round-trip to the server.</span></span> <span data-ttu-id="33d9a-141">L'URL riscritto non viene restituito al client e non viene visualizzato nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="33d9a-141">The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</span></span> <span data-ttu-id="33d9a-142">Quando `/resource` viene *riscritto* in `/different-resource`, il client richiede `/resource` e il server recupera *internamente* la risorsa in `/different-resource`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-142">When `/resource` is *rewritten* to `/different-resource`, the client requests `/resource`, and the server *internally* fetches the resource at `/different-resource`.</span></span> <span data-ttu-id="33d9a-143">Anche se il client fosse in grado di recuperare la risorsa nell'URL riscritto, non verrà informato dell'esistenza della risorsa nell'URL riscritto quando effettua la richiesta e riceve la risposta.</span><span class="sxs-lookup"><span data-stu-id="33d9a-143">Although the client might be able to retrieve the resource at the rewritten URL, the client won't be informed that the resource exists at the rewritten URL when it makes its request and receives the response.</span></span>

![Un endpoint servizio WebAPI è stato modificato dalla versione 1 (v1) alla versione 2 (v2) sul server.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a><span data-ttu-id="33d9a-148">App di esempio per la riscrittura URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-148">URL rewriting sample app</span></span>

<span data-ttu-id="33d9a-149">È possibile esplorare le funzionalità del middleware Riscrittura URL con l'[app di esempio di riscrittura URL](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/).</span><span class="sxs-lookup"><span data-stu-id="33d9a-149">You can explore the features of the URL Rewriting Middleware with the [URL rewriting sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/).</span></span> <span data-ttu-id="33d9a-150">L'app esegue le regole di riscrittura e reindirizzamento e visualizza l'URL riscritto o reindirizzato.</span><span class="sxs-lookup"><span data-stu-id="33d9a-150">The app applies rewrite and redirect rules and shows the rewritten or redirected URL.</span></span>

## <a name="when-to-use-url-rewriting-middleware"></a><span data-ttu-id="33d9a-151">Quando usare il middleware Riscrittura URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-151">When to use URL Rewriting Middleware</span></span>

<span data-ttu-id="33d9a-152">Usare il middleware Riscrittura URL quando non è possibile usare il modulo [URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) con IIS in Windows Server, il modulo [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/) in Apache Server, la [riscrittura URL in Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/) o quando l'app è ospitata nel [server HTTP.sys](xref:fundamentals/servers/httpsys) (chiamato in precedenza [WebListener](xref:fundamentals/servers/weblistener)).</span><span class="sxs-lookup"><span data-stu-id="33d9a-152">Use URL Rewriting Middleware when you are unable to use the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) with IIS on Windows Server, the [Apache mod_rewrite module](https://httpd.apache.org/docs/2.4/rewrite/) on Apache Server, [URL rewriting on Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), or your app is hosted on [HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="33d9a-153">I motivi principali per l'uso delle tecnologie di riscrittura URL basate su server in IIS, Apache o Nginx sono il fatto che il middleware non supporta tutte le funzionalità di questi moduli e il fatto che le prestazioni del middleware possono risultare inferiori a quelle dei moduli.</span><span class="sxs-lookup"><span data-stu-id="33d9a-153">The main reasons to use the server-based URL rewriting technologies in IIS, Apache, or Nginx are that the middleware doesn't support the full features of these modules and the performance of the middleware probably won't match that of the modules.</span></span> <span data-ttu-id="33d9a-154">Tuttavia alcune funzionalità dei moduli server non funzionano con i progetti ASP.NET Core, ad esempio i vincoli `IsFile` e `IsDirectory` del modulo IIS Rewrite.</span><span class="sxs-lookup"><span data-stu-id="33d9a-154">However, there are some features of the server modules that don't work with ASP.NET Core projects, such as the `IsFile` and `IsDirectory` constraints of the IIS Rewrite module.</span></span> <span data-ttu-id="33d9a-155">In questi scenari è necessario usare il middleware.</span><span class="sxs-lookup"><span data-stu-id="33d9a-155">In these scenarios, use the middleware instead.</span></span>

## <a name="package"></a><span data-ttu-id="33d9a-156">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="33d9a-156">Package</span></span>

<span data-ttu-id="33d9a-157">Per includere il middleware nel progetto, aggiungere un riferimento al pacchetto [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/).</span><span class="sxs-lookup"><span data-stu-id="33d9a-157">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) package.</span></span> <span data-ttu-id="33d9a-158">Questa funzionalità è disponibile per le app destinate ad ASP.NET Core 1.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="33d9a-158">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="extension-and-options"></a><span data-ttu-id="33d9a-159">Estensioni e opzioni</span><span class="sxs-lookup"><span data-stu-id="33d9a-159">Extension and options</span></span>

<span data-ttu-id="33d9a-160">È possibile definire regole di riscrittura e reindirizzamento URL personalizzate creando un'istanza della classe [RewriteOptions](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptions) con metodi di estensione per le singole regole.</span><span class="sxs-lookup"><span data-stu-id="33d9a-160">Establish your URL rewrite and redirect rules by creating an instance of the [RewriteOptions](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptions) class with extension methods for each of your rules.</span></span> <span data-ttu-id="33d9a-161">Concatenare più regole nell'ordine in cui si vuole che vengano elaborate.</span><span class="sxs-lookup"><span data-stu-id="33d9a-161">Chain multiple rules in the order that you would like them processed.</span></span> <span data-ttu-id="33d9a-162">Le opzioni `RewriteOptions` vengono passare al middleware Riscrittura URL quando questo viene aggiunto alla pipeline della richiesta con `app.UseRewriter(options);`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-162">The `RewriteOptions` are passed into the URL Rewriting Middleware as it's added to the request pipeline with `app.UseRewriter(options);`.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1")
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true)
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")
        .Add(RedirectXMLRequests)
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="redirect-non-www-to-www"></a><span data-ttu-id="33d9a-163">Reindirizzare non-www su www</span><span class="sxs-lookup"><span data-stu-id="33d9a-163">Redirect non-www to www</span></span>

<span data-ttu-id="33d9a-164">Sono disponibili tre opzioni che consentono all'app di reindirizzare richieste non-`www` su `www`:</span><span class="sxs-lookup"><span data-stu-id="33d9a-164">Three options permit the app to redirect non-`www` requests to `www`:</span></span>

* <span data-ttu-id="33d9a-165">[AddRedirectToWwwPermanent(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowwwpermanent) &ndash; Reindirizza in modo permanente la richiesta al sottodominio `www` se la richiesta è non-`www`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-165">[AddRedirectToWwwPermanent(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowwwpermanent) &ndash; Permanently redirect the request to the `www` subdomain if the request is non-`www`.</span></span> <span data-ttu-id="33d9a-166">Reindirizza con un codice di stato [Status308PermanentRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status308permanentredirect).</span><span class="sxs-lookup"><span data-stu-id="33d9a-166">Redirects with a [Status308PermanentRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status308permanentredirect) status code.</span></span>
* <span data-ttu-id="33d9a-167">[AddRedirectToWww(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Reindirizza la richiesta al sottodominio `www` se la richiesta in ingresso è non-`www`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-167">[AddRedirectToWww(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Redirect the request to the `www` subdomain if the incoming request is non-`www`.</span></span> <span data-ttu-id="33d9a-168">Reindirizza con un codice di stato [Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect).</span><span class="sxs-lookup"><span data-stu-id="33d9a-168">Redirects with a [Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect) status code.</span></span>
* <span data-ttu-id="33d9a-169">[AddRedirectToWww(RewriteOptions, Int32)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Reindirizza la richiesta al sottodominio `www` se la richiesta in ingresso è non-`www`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-169">[AddRedirectToWww(RewriteOptions, Int32)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Redirect the request to the `www` subdomain if the incoming request is non-`www`.</span></span> <span data-ttu-id="33d9a-170">Consente di specificare il codice di stato per la risposta.</span><span class="sxs-lookup"><span data-stu-id="33d9a-170">Allows you to provide the status code for the response.</span></span> <span data-ttu-id="33d9a-171">Usare i campi della classe [StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes) per le assegnazioni ad `AddRedirectToWww`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-171">Use the fields of the [StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes) class for assignments to `AddRedirectToWww`.</span></span>

::: moniker-end

### <a name="url-redirect"></a><span data-ttu-id="33d9a-172">Renidirizzamento URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-172">URL redirect</span></span>

<span data-ttu-id="33d9a-173">Per reindirizzare le richieste, usare `AddRedirect`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-173">Use `AddRedirect` to redirect requests.</span></span> <span data-ttu-id="33d9a-174">Il primo parametro contiene l'espressione regolare per la corrispondenza in base al percorso dell'URL in ingresso.</span><span class="sxs-lookup"><span data-stu-id="33d9a-174">The first parameter contains your regex for matching on the path of the incoming URL.</span></span> <span data-ttu-id="33d9a-175">Il secondo parametro è la stringa di sostituzione.</span><span class="sxs-lookup"><span data-stu-id="33d9a-175">The second parameter is the replacement string.</span></span> <span data-ttu-id="33d9a-176">Il terzo parametro, se presente, specifica il codice di stato.</span><span class="sxs-lookup"><span data-stu-id="33d9a-176">The third parameter, if present, specifies the status code.</span></span> <span data-ttu-id="33d9a-177">Se il codice di stato non è specificato, assume il valore 302 (Trovato), che indica che la risorsa è stata temporaneamente spostata o sostituita.</span><span class="sxs-lookup"><span data-stu-id="33d9a-177">If you don't specify the status code, it defaults to 302 (Found), which indicates that the resource is temporarily moved or replaced.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=9)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-178">In un browser con gli strumenti di sviluppo abilitati, creare una richiesta all'app di esempio con il percorso `/redirect-rule/1234/5678`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-178">In a browser with developer tools enabled, make a request to the sample app with the path `/redirect-rule/1234/5678`.</span></span> <span data-ttu-id="33d9a-179">L'espressione regolare definisce la corrispondenza con il percorso di richiesta in `redirect-rule/(.*)` e il percorso viene sostituito con `/redirected/1234/5678`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-179">The regex matches the request path on `redirect-rule/(.*)`, and the path is replaced with `/redirected/1234/5678`.</span></span> <span data-ttu-id="33d9a-180">L'URL di reindirizzamento viene restituito al client con il codice di stato 302 (Trovato).</span><span class="sxs-lookup"><span data-stu-id="33d9a-180">The redirect URL is sent back to the client with a 302 (Found) status code.</span></span> <span data-ttu-id="33d9a-181">Il browser invia una nuova richiesta all'URL di reindirizzamento, che viene visualizzata nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="33d9a-181">The browser makes a new request at the redirect URL, which appears in the browser's address bar.</span></span> <span data-ttu-id="33d9a-182">Dato che nessuna regola dell'app di esempio presenta una corrispondenza con l'URL di reindirizzamento, la seconda richiesta riceve una risposta 200 (OK) dall'app e il corpo della risposta visualizza l'URL di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="33d9a-182">Since no rules in the sample app match on the redirect URL, the second request receives a 200 (OK) response from the app and the body of the response shows the redirect URL.</span></span> <span data-ttu-id="33d9a-183">Quando un URL viene *reindirizzato* viene eseguita una sequenza di andata e ritorno al server.</span><span class="sxs-lookup"><span data-stu-id="33d9a-183">A roundtrip is made to the server when a URL is *redirected*.</span></span>

> [!WARNING]
> <span data-ttu-id="33d9a-184">Prestare attenzione quando si definiscono le regole di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="33d9a-184">Be cautious when establishing your redirect rules.</span></span> <span data-ttu-id="33d9a-185">Le regole di reindirizzamento vengono valutate in ogni richiesta all'app, anche dopo un reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="33d9a-185">Your redirect rules are evaluated on each request to the app, including after a redirect.</span></span> <span data-ttu-id="33d9a-186">È facile creare inavvertitamente un ciclo di reindirizzamento infinito.</span><span class="sxs-lookup"><span data-stu-id="33d9a-186">It's easy to accidently create a loop of infinite redirects.</span></span>

<span data-ttu-id="33d9a-187">Richiesta originale: `/redirect-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="33d9a-187">Original Request: `/redirect-rule/1234/5678`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte](url-rewriting/_static/add_redirect.png)

<span data-ttu-id="33d9a-189">La parte dell'espressione racchiusa tra parentesi è denominata *gruppo Capture*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-189">The part of the expression contained within parentheses is called a *capture group*.</span></span> <span data-ttu-id="33d9a-190">Il punto (`.`) dell'espressione significa *corrispondenza con qualsiasi carattere*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-190">The dot (`.`) of the expression means *match any character*.</span></span> <span data-ttu-id="33d9a-191">L'asterisco (`*`) indica *corrispondenza con il carattere precedente per zero o più volte*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-191">The asterisk (`*`) indicates *match the preceding character zero or more times*.</span></span> <span data-ttu-id="33d9a-192">Di conseguenza gli ultimi due i segmenti di percorso dell'URL `1234/5678` vengono acquisiti tramite il gruppo Capture `(.*)`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-192">Therefore, the last two path segments of the URL, `1234/5678`, are captured by capture group `(.*)`.</span></span> <span data-ttu-id="33d9a-193">Qualsiasi valore visualizzato nell'URL della richiesta dopo `redirect-rule/` viene acquisito da questo gruppo Capture.</span><span class="sxs-lookup"><span data-stu-id="33d9a-193">Any value you provide in the request URL after `redirect-rule/` is captured by this single capture group.</span></span>

<span data-ttu-id="33d9a-194">Nella stringa di sostituzione i gruppi acquisiti vengono inseriti nella stringa con il simbolo di dollaro (`$`) seguito dal numero di sequenza dell'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="33d9a-194">In the replacement string, captured groups are injected into the string with the dollar sign (`$`) followed by the sequence number of the capture.</span></span> <span data-ttu-id="33d9a-195">Il primo valore del gruppo Capture viene ottenuto con `$1`, il secondo con `$2` e la procedura continua in sequenza per i gruppi Capture presenti nell'espressione regolare.</span><span class="sxs-lookup"><span data-stu-id="33d9a-195">The first capture group value is obtained with `$1`, the second with `$2`, and they continue in sequence for the capture groups in your regex.</span></span> <span data-ttu-id="33d9a-196">Nell'espressione regolare della regola di reindirizzamento dell'app di esempio è presente un solo gruppo acquisito, pertanto nella stringa di sostituzione è presente un solo gruppo inserito, ovvero `$1`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-196">There's only one captured group in the redirect rule regex in the sample app, so there's only one injected group in the replacement string, which is `$1`.</span></span> <span data-ttu-id="33d9a-197">Quando viene applicata la regola, l'URL diventa `/redirected/1234/5678`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-197">When the rule is applied, the URL becomes `/redirected/1234/5678`.</span></span>

### <a name="url-redirect-to-a-secure-endpoint"></a><span data-ttu-id="33d9a-198">Reindirizzamento URL a un endpoint protetto</span><span class="sxs-lookup"><span data-stu-id="33d9a-198">URL redirect to a secure endpoint</span></span>

<span data-ttu-id="33d9a-199">Usare `AddRedirectToHttps` per reindirizzare le richieste HTTP allo stesso host e allo stesso percorso mediante il protocollo HTTPS (`https://`).</span><span class="sxs-lookup"><span data-stu-id="33d9a-199">Use `AddRedirectToHttps` to redirect HTTP requests to the same host and path using HTTPS (`https://`).</span></span> <span data-ttu-id="33d9a-200">Se il codice di stato non viene specificato, il middleware imposta il valore predefinito 302 (Trovato).</span><span class="sxs-lookup"><span data-stu-id="33d9a-200">If the status code isn't supplied, the middleware defaults to 302 (Found).</span></span> <span data-ttu-id="33d9a-201">Se la porta non viene specificata, il middleware imposta il valore predefinito `null`, che indica che il protocollo diventa `https://` e il client accede alla risorsa sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="33d9a-201">If the port isn't supplied, the middleware defaults to `null`, which means the protocol changes to `https://` and the client accesses the resource on port 443.</span></span> <span data-ttu-id="33d9a-202">L'esempio indica come impostare il codice di stato su 301 (Spostato permanentemente) e come cambiare il numero di porta in 5001.</span><span class="sxs-lookup"><span data-stu-id="33d9a-202">The example shows how to set the status code to 301 (Moved Permanently) and change the port to 5001.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttps(301, 5001);

    app.UseRewriter(options);
}
```

<span data-ttu-id="33d9a-203">Usare `AddRedirectToHttpsPermanent` per reindirizzare le richieste non protette allo stesso host e allo stesso percorso con il protocollo di protezione HTTPS (`https://` sulla porta 443).</span><span class="sxs-lookup"><span data-stu-id="33d9a-203">Use `AddRedirectToHttpsPermanent` to redirect insecure requests to the same host and path with secure HTTPS protocol (`https://` on port 443).</span></span> <span data-ttu-id="33d9a-204">Il middleware imposta il codice stato su 301 (Spostato permanentemente).</span><span class="sxs-lookup"><span data-stu-id="33d9a-204">The middleware sets the status code to 301 (Moved Permanently).</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttpsPermanent();

    app.UseRewriter(options);
}
```

> [!NOTE]
> <span data-ttu-id="33d9a-205">Per il reindirizzamento a HTTPS quando non sono richieste regole di reindirizzamento aggiuntive, si consiglia di usare il middleware di reindirizzamento HTTPS.</span><span class="sxs-lookup"><span data-stu-id="33d9a-205">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware.</span></span> <span data-ttu-id="33d9a-206">Per altre informazioni, vedere l'argomento [Imporre HTTPS](xref:security/enforcing-ssl#require-https).</span><span class="sxs-lookup"><span data-stu-id="33d9a-206">For more information, see the [Enforce HTTPS](xref:security/enforcing-ssl#require-https) topic.</span></span>

<span data-ttu-id="33d9a-207">L'app di esempio indica come usare `AddRedirectToHttps` o `AddRedirectToHttpsPermanent`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-207">The sample app is capable of demonstrating how to use `AddRedirectToHttps` or `AddRedirectToHttpsPermanent`.</span></span> <span data-ttu-id="33d9a-208">Aggiungere il metodo di estensione a `RewriteOptions`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-208">Add the extension method to the `RewriteOptions`.</span></span> <span data-ttu-id="33d9a-209">Eseguire una richiesta non sicura all'app su qualsiasi URL.</span><span class="sxs-lookup"><span data-stu-id="33d9a-209">Make an insecure request to the app at any URL.</span></span> <span data-ttu-id="33d9a-210">Ignorare l'avviso di sicurezza del browser indicante che il certificato autofirmato non è attendibile oppure creare un'eccezione per rendere affidabile il certificato.</span><span class="sxs-lookup"><span data-stu-id="33d9a-210">Dismiss the browser security warning that the self-signed certificate is untrusted or create an exception to trust the certificate.</span></span>

<span data-ttu-id="33d9a-211">Richiesta originale con `AddRedirectToHttps(301, 5001)`: `http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="33d9a-211">Original Request using `AddRedirectToHttps(301, 5001)`: `http://localhost:5000/secure`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte](url-rewriting/_static/add_redirect_to_https.png)

<span data-ttu-id="33d9a-213">Richiesta originale con `AddRedirectToHttpsPermanent`: `http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="33d9a-213">Original Request using `AddRedirectToHttpsPermanent`: `http://localhost:5000/secure`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a><span data-ttu-id="33d9a-215">Riscrittura URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-215">URL rewrite</span></span>

<span data-ttu-id="33d9a-216">Usare `AddRewrite` per creare una regola di riscrittura URL.</span><span class="sxs-lookup"><span data-stu-id="33d9a-216">Use `AddRewrite` to create a rule for rewriting URLs.</span></span> <span data-ttu-id="33d9a-217">Il primo parametro contiene l'espressione regolare per la corrispondenza in base al percorso dell'URL in ingresso.</span><span class="sxs-lookup"><span data-stu-id="33d9a-217">The first parameter contains your regex for matching on the incoming URL path.</span></span> <span data-ttu-id="33d9a-218">Il secondo parametro è la stringa di sostituzione.</span><span class="sxs-lookup"><span data-stu-id="33d9a-218">The second parameter is the replacement string.</span></span> <span data-ttu-id="33d9a-219">Il terzo parametro, `skipRemainingRules: {true|false}`, indica al middleware se ignorare le regole di riscrittura aggiuntive quando viene applicata la regola corrente.</span><span class="sxs-lookup"><span data-stu-id="33d9a-219">The third parameter, `skipRemainingRules: {true|false}`, indicates to the middleware whether or not to skip additional rewrite rules if the current rule is applied.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=10-11)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true);

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-220">Richiesta originale: `/rewrite-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="33d9a-220">Original Request: `/rewrite-rule/1234/5678`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richiesta e risposta](url-rewriting/_static/add_rewrite.png)

<span data-ttu-id="33d9a-222">Il primo elemento che si nota nell'espressione regolare è l'accento circonflesso (`^`) all'inizio dell'espressione.</span><span class="sxs-lookup"><span data-stu-id="33d9a-222">The first thing you notice in the regex is the carat (`^`) at the beginning of the expression.</span></span> <span data-ttu-id="33d9a-223">Questo carattere indica che la corrispondenza inizia all'inizio del percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="33d9a-223">This means that matching starts at the beginning of the URL path.</span></span>

<span data-ttu-id="33d9a-224">Nell'esempio precedente con la regola di reindirizzamento, `redirect-rule/(.*)`, non è presente un accento circonflesso all'inizio dell'espressione regolare, pertanto nel percorso può essere presente qualsiasi carattere prima di `redirect-rule/` e la corrispondenza viene comunque rilevata.</span><span class="sxs-lookup"><span data-stu-id="33d9a-224">In the earlier example with the redirect rule, `redirect-rule/(.*)`, there's no carat at the start of the regex; therefore, any characters may precede `redirect-rule/` in the path for a successful match.</span></span>

| <span data-ttu-id="33d9a-225">Path</span><span class="sxs-lookup"><span data-stu-id="33d9a-225">Path</span></span>                               | <span data-ttu-id="33d9a-226">Corrispondenza con</span><span class="sxs-lookup"><span data-stu-id="33d9a-226">Match</span></span> |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | <span data-ttu-id="33d9a-227">Yes</span><span class="sxs-lookup"><span data-stu-id="33d9a-227">Yes</span></span>   |
| `/my-cool-redirect-rule/1234/5678` | <span data-ttu-id="33d9a-228">Yes</span><span class="sxs-lookup"><span data-stu-id="33d9a-228">Yes</span></span>   |
| `/anotherredirect-rule/1234/5678`  | <span data-ttu-id="33d9a-229">Yes</span><span class="sxs-lookup"><span data-stu-id="33d9a-229">Yes</span></span>   |

<span data-ttu-id="33d9a-230">La regola di riscrittura, `^rewrite-rule/(\d+)/(\d+)`, rileva la corrispondenza dei percorsi solo se iniziano con `rewrite-rule/`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-230">The rewrite rule, `^rewrite-rule/(\d+)/(\d+)`, only matches paths if they start with `rewrite-rule/`.</span></span> <span data-ttu-id="33d9a-231">Osservare la differenza nella corrispondenza tra la regola di riscrittura in basso e la regola di reindirizzamento in alto.</span><span class="sxs-lookup"><span data-stu-id="33d9a-231">Notice the difference in matching between the rewrite rule below and the redirect rule above.</span></span>

| <span data-ttu-id="33d9a-232">Path</span><span class="sxs-lookup"><span data-stu-id="33d9a-232">Path</span></span>                              | <span data-ttu-id="33d9a-233">Corrispondenza con</span><span class="sxs-lookup"><span data-stu-id="33d9a-233">Match</span></span> |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | <span data-ttu-id="33d9a-234">Yes</span><span class="sxs-lookup"><span data-stu-id="33d9a-234">Yes</span></span>   |
| `/my-cool-rewrite-rule/1234/5678` | <span data-ttu-id="33d9a-235">No</span><span class="sxs-lookup"><span data-stu-id="33d9a-235">No</span></span>    |
| `/anotherrewrite-rule/1234/5678`  | <span data-ttu-id="33d9a-236">No</span><span class="sxs-lookup"><span data-stu-id="33d9a-236">No</span></span>    |

<span data-ttu-id="33d9a-237">Dopo la parte `^rewrite-rule/` dell'espressione sono presenti due gruppi Capture, `(\d+)/(\d+)`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-237">Following the `^rewrite-rule/` portion of the expression, there are two capture groups, `(\d+)/(\d+)`.</span></span> <span data-ttu-id="33d9a-238">`\d` indica *corrispondenza con una cifra (numero)*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-238">The `\d` signifies *match a digit (number)*.</span></span> <span data-ttu-id="33d9a-239">Il segno più (`+`) indica *corrispondenza con uno o più dei caratteri precedenti*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-239">The plus sign (`+`) means *match one or more of the preceding character*.</span></span> <span data-ttu-id="33d9a-240">Di conseguenza l'URL deve contenere un numero seguito da una barra seguita a sua volta da un altro numero.</span><span class="sxs-lookup"><span data-stu-id="33d9a-240">Therefore, the URL must contain a number followed by a forward-slash followed by another number.</span></span> <span data-ttu-id="33d9a-241">Questi gruppi Capture vengono inseriti nell'URL riscritto come `$1` e `$2`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-241">These capture groups are injected into the rewritten URL as `$1` and `$2`.</span></span> <span data-ttu-id="33d9a-242">La stringa di sostituzione della regola di riscrittura inserisce i gruppi acquisiti nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="33d9a-242">The rewrite rule replacement string places the captured groups into the querystring.</span></span> <span data-ttu-id="33d9a-243">Il percorso richiesto `/rewrite-rule/1234/5678` viene riscritto per ottenere la risorsa in `/rewritten?var1=1234&var2=5678`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-243">The requested path of `/rewrite-rule/1234/5678` is rewritten to obtain the resource at `/rewritten?var1=1234&var2=5678`.</span></span> <span data-ttu-id="33d9a-244">Se nella richiesta originale è presente una stringa di query, la stringa viene mantenuta quando l'URL viene riscritto.</span><span class="sxs-lookup"><span data-stu-id="33d9a-244">If a querystring is present on the original request, it's preserved when the URL is rewritten.</span></span>

<span data-ttu-id="33d9a-245">Non viene eseguita nessuna sequenza di andata e ritorno al server per ottenere la risorsa.</span><span class="sxs-lookup"><span data-stu-id="33d9a-245">There's no roundtrip to the server to obtain the resource.</span></span> <span data-ttu-id="33d9a-246">Se la risorsa esiste viene recuperata e restituita al client con il codice stato 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="33d9a-246">If the resource exists, it's fetched and returned to the client with a 200 (OK) status code.</span></span> <span data-ttu-id="33d9a-247">Poiché il client non è reindirizzato, l'URL nella barra degli indirizzi del browser non cambia.</span><span class="sxs-lookup"><span data-stu-id="33d9a-247">Because the client isn't redirected, the URL in the browser address bar doesn't change.</span></span> <span data-ttu-id="33d9a-248">Dal punto di vista del client, l'operazione di riscrittura URL non si è verificata.</span><span class="sxs-lookup"><span data-stu-id="33d9a-248">As far as the client is concerned, the URL rewrite operation never occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="33d9a-249">Se possibile, usare sempre `skipRemainingRules: true`, perché la corrispondenza tra le regole è un processo dispendioso che rallenta il tempo di risposta dell'app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-249">Use `skipRemainingRules: true` whenever possible, because matching rules is an expensive process and reduces app response time.</span></span> <span data-ttu-id="33d9a-250">Per velocizzare il tempo di risposta dell'app:</span><span class="sxs-lookup"><span data-stu-id="33d9a-250">For the fastest app response:</span></span>
> * <span data-ttu-id="33d9a-251">Ordinare le regole di riscrittura dalla regola che origina più corrispondenze a quella che origina meno corrispondenze.</span><span class="sxs-lookup"><span data-stu-id="33d9a-251">Order your rewrite rules from the most frequently matched rule to the least frequently matched rule.</span></span>
> * <span data-ttu-id="33d9a-252">Quando viene rilevata una corrispondenza e non sono necessarie altre operazioni di elaborazione delle regole, ignorare l'elaborazione delle regole rimanenti.</span><span class="sxs-lookup"><span data-stu-id="33d9a-252">Skip the processing of the remaining rules when a match occurs and no additional rule processing is required.</span></span>

### <a name="apache-modrewrite"></a><span data-ttu-id="33d9a-253">Modulo Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="33d9a-253">Apache mod_rewrite</span></span>

<span data-ttu-id="33d9a-254">Applicare le regole del modulo Apache mod_rewrite con `AddApacheModRewrite`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-254">Apply Apache mod_rewrite rules with `AddApacheModRewrite`.</span></span> <span data-ttu-id="33d9a-255">Assicurarsi che il file delle regole venga distribuito con l'app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-255">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="33d9a-256">Per altre informazioni ed esempi di regole mod_rewrite, vedere [Modulo Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span><span class="sxs-lookup"><span data-stu-id="33d9a-256">For more information and examples of mod_rewrite rules, see [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="33d9a-257">`StreamReader` viene usato per leggere le regole del file di regole *ApacheModRewrite.txt*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-257">A `StreamReader` is used to read the rules from the *ApacheModRewrite.txt* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=3-4,12)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="33d9a-258">Il primo parametro accetta `IFileProvider`, che viene reso disponibile tramite [Dependency Injection](dependency-injection.md) (Inserimento di dipendenze).</span><span class="sxs-lookup"><span data-stu-id="33d9a-258">The first parameter takes an `IFileProvider`, which is provided via [Dependency Injection](dependency-injection.md).</span></span> <span data-ttu-id="33d9a-259">`IHostingEnvironment` viene inserito per specificare `ContentRootFileProvider`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-259">The `IHostingEnvironment` is injected to provide the `ContentRootFileProvider`.</span></span> <span data-ttu-id="33d9a-260">Il secondo parametro è il percorso del file di regole, ovvero *ApacheModRewrite.txt* nell'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="33d9a-260">The second parameter is the path to your rules file, which is *ApacheModRewrite.txt* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-261">L'app di esempio reindirizza le richieste da `/apache-mod-rules-redirect/(.\*)` a `/redirected?id=$1`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-261">The sample app redirects requests from `/apache-mod-rules-redirect/(.\*)` to `/redirected?id=$1`.</span></span> <span data-ttu-id="33d9a-262">Il codice di stato della risposta è 302 (Trovato).</span><span class="sxs-lookup"><span data-stu-id="33d9a-262">The response status code is 302 (Found).</span></span>

[!code[](url-rewriting/sample/ApacheModRewrite.txt)]

<span data-ttu-id="33d9a-263">Richiesta originale: `/apache-mod-rules-redirect/1234`</span><span class="sxs-lookup"><span data-stu-id="33d9a-263">Original Request: `/apache-mod-rules-redirect/1234`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte](url-rewriting/_static/add_apache_mod_redirect.png)

<span data-ttu-id="33d9a-265">Il middleware supporta le seguenti variabili server del modulo Apache mod_rewrite:</span><span class="sxs-lookup"><span data-stu-id="33d9a-265">The middleware supports the following Apache mod_rewrite server variables:</span></span>

* <span data-ttu-id="33d9a-266">CONN_REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="33d9a-266">CONN_REMOTE_ADDR</span></span>
* <span data-ttu-id="33d9a-267">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="33d9a-267">HTTP_ACCEPT</span></span>
* <span data-ttu-id="33d9a-268">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="33d9a-268">HTTP_CONNECTION</span></span>
* <span data-ttu-id="33d9a-269">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="33d9a-269">HTTP_COOKIE</span></span>
* <span data-ttu-id="33d9a-270">HTTP_FORWARDED</span><span class="sxs-lookup"><span data-stu-id="33d9a-270">HTTP_FORWARDED</span></span>
* <span data-ttu-id="33d9a-271">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="33d9a-271">HTTP_HOST</span></span>
* <span data-ttu-id="33d9a-272">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="33d9a-272">HTTP_REFERER</span></span>
* <span data-ttu-id="33d9a-273">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="33d9a-273">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="33d9a-274">HTTPS</span><span class="sxs-lookup"><span data-stu-id="33d9a-274">HTTPS</span></span>
* <span data-ttu-id="33d9a-275">IPV6</span><span class="sxs-lookup"><span data-stu-id="33d9a-275">IPV6</span></span>
* <span data-ttu-id="33d9a-276">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="33d9a-276">QUERY_STRING</span></span>
* <span data-ttu-id="33d9a-277">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="33d9a-277">REMOTE_ADDR</span></span>
* <span data-ttu-id="33d9a-278">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="33d9a-278">REMOTE_PORT</span></span>
* <span data-ttu-id="33d9a-279">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="33d9a-279">REQUEST_FILENAME</span></span>
* <span data-ttu-id="33d9a-280">REQUEST_METHOD</span><span class="sxs-lookup"><span data-stu-id="33d9a-280">REQUEST_METHOD</span></span>
* <span data-ttu-id="33d9a-281">REQUEST_SCHEME</span><span class="sxs-lookup"><span data-stu-id="33d9a-281">REQUEST_SCHEME</span></span>
* <span data-ttu-id="33d9a-282">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="33d9a-282">REQUEST_URI</span></span>
* <span data-ttu-id="33d9a-283">SCRIPT_FILENAME</span><span class="sxs-lookup"><span data-stu-id="33d9a-283">SCRIPT_FILENAME</span></span>
* <span data-ttu-id="33d9a-284">SERVER_ADDR</span><span class="sxs-lookup"><span data-stu-id="33d9a-284">SERVER_ADDR</span></span>
* <span data-ttu-id="33d9a-285">SERVER_PORT</span><span class="sxs-lookup"><span data-stu-id="33d9a-285">SERVER_PORT</span></span>
* <span data-ttu-id="33d9a-286">SERVER_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="33d9a-286">SERVER_PROTOCOL</span></span>
* <span data-ttu-id="33d9a-287">TIME</span><span class="sxs-lookup"><span data-stu-id="33d9a-287">TIME</span></span>
* <span data-ttu-id="33d9a-288">TIME_DAY</span><span class="sxs-lookup"><span data-stu-id="33d9a-288">TIME_DAY</span></span>
* <span data-ttu-id="33d9a-289">TIME_HOUR</span><span class="sxs-lookup"><span data-stu-id="33d9a-289">TIME_HOUR</span></span>
* <span data-ttu-id="33d9a-290">TIME_MIN</span><span class="sxs-lookup"><span data-stu-id="33d9a-290">TIME_MIN</span></span>
* <span data-ttu-id="33d9a-291">TIME_MON</span><span class="sxs-lookup"><span data-stu-id="33d9a-291">TIME_MON</span></span>
* <span data-ttu-id="33d9a-292">TIME_SEC</span><span class="sxs-lookup"><span data-stu-id="33d9a-292">TIME_SEC</span></span>
* <span data-ttu-id="33d9a-293">TIME_WDAY</span><span class="sxs-lookup"><span data-stu-id="33d9a-293">TIME_WDAY</span></span>
* <span data-ttu-id="33d9a-294">TIME_YEAR</span><span class="sxs-lookup"><span data-stu-id="33d9a-294">TIME_YEAR</span></span>

### <a name="iis-url-rewrite-module-rules"></a><span data-ttu-id="33d9a-295">Regole di IIS URL Rewrite Module</span><span class="sxs-lookup"><span data-stu-id="33d9a-295">IIS URL Rewrite Module rules</span></span>

<span data-ttu-id="33d9a-296">Per usare regole valide per IIS URL Rewrite Module, usare `AddIISUrlRewrite`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-296">To use rules that apply to the IIS URL Rewrite Module, use `AddIISUrlRewrite`.</span></span> <span data-ttu-id="33d9a-297">Assicurarsi che il file delle regole venga distribuito con l'app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-297">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="33d9a-298">Non indirizzare il middleware all'uso del file *web.config* personalizzato quando è in esecuzione in Windows Server IIS.</span><span class="sxs-lookup"><span data-stu-id="33d9a-298">Don't direct the middleware to use your *web.config* file when running on Windows Server IIS.</span></span> <span data-ttu-id="33d9a-299">Con IIS queste regole devono essere archiviate fuori dal file *web.config*, per evitare conflitti con il modulo IIS Rewrite.</span><span class="sxs-lookup"><span data-stu-id="33d9a-299">With IIS, these rules should be stored outside of your *web.config* to avoid conflicts with the IIS Rewrite module.</span></span> <span data-ttu-id="33d9a-300">Per altre informazioni ed esempi di regole di IIS URL Rewrite Module, vedere [Using URL Rewrite Module 2.0](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) (Uso di URL Rewrite Module 2.0) e [URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference) (Guida di riferimento per la configurazione di URL Rewrite Module).</span><span class="sxs-lookup"><span data-stu-id="33d9a-300">For more information and examples of IIS URL Rewrite Module rules, see [Using Url Rewrite Module 2.0](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) and [URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="33d9a-301">Un elemento `StreamReader` viene usato per leggere le regole del file di regole *IISUrlRewrite.xml*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-301">A `StreamReader` is used to read the rules from the *IISUrlRewrite.xml* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=5-6,13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="33d9a-302">Il primo parametro accetta `IFileProvider` e il secondo parametro è il percorso del file di regole XML, ovvero *IISUrlRewrite.xml* nell'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="33d9a-302">The first parameter takes an `IFileProvider`, while the second parameter is the path to your XML rules file, which is *IISUrlRewrite.xml* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-303">L'app di esempio riscrive le richieste da `/iis-rules-rewrite/(.*)` a `/rewritten?id=$1`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-303">The sample app rewrites requests from `/iis-rules-rewrite/(.*)` to `/rewritten?id=$1`.</span></span> <span data-ttu-id="33d9a-304">La risposta viene inviata al client con un codice di stato 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="33d9a-304">The response is sent to the client with a 200 (OK) status code.</span></span>

[!code-xml[](url-rewriting/sample/IISUrlRewrite.xml)]

<span data-ttu-id="33d9a-305">Richiesta originale: `/iis-rules-rewrite/1234`</span><span class="sxs-lookup"><span data-stu-id="33d9a-305">Original Request: `/iis-rules-rewrite/1234`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richiesta e risposta](url-rewriting/_static/add_iis_url_rewrite.png)

<span data-ttu-id="33d9a-307">Se è presente un modulo IIS Rewrite attivo con regole di livello server configurate che possono avere effetti indesiderati nell'app, è possibile disabilitare il modulo IIS Rewrite per un'app.</span><span class="sxs-lookup"><span data-stu-id="33d9a-307">If you have an active IIS Rewrite Module with server-level rules configured that would impact your app in undesirable ways, you can disable the IIS Rewrite Module for an app.</span></span> <span data-ttu-id="33d9a-308">Per altre informazioni, vedere [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules) (Disabilitazione di moduli IIS).</span><span class="sxs-lookup"><span data-stu-id="33d9a-308">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

#### <a name="unsupported-features"></a><span data-ttu-id="33d9a-309">Funzionalità non supportate</span><span class="sxs-lookup"><span data-stu-id="33d9a-309">Unsupported features</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="33d9a-310">Il middleware rilasciato con ASP.NET Core 2.x non supporta le seguenti funzionalità di IIS URL Rewrite Module:</span><span class="sxs-lookup"><span data-stu-id="33d9a-310">The middleware released with ASP.NET Core 2.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="33d9a-311">Regole in uscita</span><span class="sxs-lookup"><span data-stu-id="33d9a-311">Outbound Rules</span></span>
* <span data-ttu-id="33d9a-312">Variabili server personalizzate</span><span class="sxs-lookup"><span data-stu-id="33d9a-312">Custom Server Variables</span></span>
* <span data-ttu-id="33d9a-313">Caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="33d9a-313">Wildcards</span></span>
* <span data-ttu-id="33d9a-314">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="33d9a-314">LogRewrittenUrl</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="33d9a-315">Il middleware rilasciato con ASP.NET Core 1.x non supporta le seguenti funzionalità di IIS URL Rewrite Module:</span><span class="sxs-lookup"><span data-stu-id="33d9a-315">The middleware released with ASP.NET Core 1.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="33d9a-316">Regole globali</span><span class="sxs-lookup"><span data-stu-id="33d9a-316">Global Rules</span></span>
* <span data-ttu-id="33d9a-317">Regole in uscita</span><span class="sxs-lookup"><span data-stu-id="33d9a-317">Outbound Rules</span></span>
* <span data-ttu-id="33d9a-318">Mapping di riscrittura</span><span class="sxs-lookup"><span data-stu-id="33d9a-318">Rewrite Maps</span></span>
* <span data-ttu-id="33d9a-319">Azione CustomResponse</span><span class="sxs-lookup"><span data-stu-id="33d9a-319">CustomResponse Action</span></span>
* <span data-ttu-id="33d9a-320">Variabili server personalizzate</span><span class="sxs-lookup"><span data-stu-id="33d9a-320">Custom Server Variables</span></span>
* <span data-ttu-id="33d9a-321">Caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="33d9a-321">Wildcards</span></span>
* <span data-ttu-id="33d9a-322">Action:CustomResponse</span><span class="sxs-lookup"><span data-stu-id="33d9a-322">Action:CustomResponse</span></span>
* <span data-ttu-id="33d9a-323">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="33d9a-323">LogRewrittenUrl</span></span>

::: moniker-end

#### <a name="supported-server-variables"></a><span data-ttu-id="33d9a-324">Variabili server supportate</span><span class="sxs-lookup"><span data-stu-id="33d9a-324">Supported server variables</span></span>

<span data-ttu-id="33d9a-325">Il middleware supporta le seguenti variabili server di IIS URL Rewrite Module:</span><span class="sxs-lookup"><span data-stu-id="33d9a-325">The middleware supports the following IIS URL Rewrite Module server variables:</span></span>

* <span data-ttu-id="33d9a-326">CONTENT_LENGTH</span><span class="sxs-lookup"><span data-stu-id="33d9a-326">CONTENT_LENGTH</span></span>
* <span data-ttu-id="33d9a-327">CONTENT_TYPE</span><span class="sxs-lookup"><span data-stu-id="33d9a-327">CONTENT_TYPE</span></span>
* <span data-ttu-id="33d9a-328">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="33d9a-328">HTTP_ACCEPT</span></span>
* <span data-ttu-id="33d9a-329">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="33d9a-329">HTTP_CONNECTION</span></span>
* <span data-ttu-id="33d9a-330">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="33d9a-330">HTTP_COOKIE</span></span>
* <span data-ttu-id="33d9a-331">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="33d9a-331">HTTP_HOST</span></span>
* <span data-ttu-id="33d9a-332">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="33d9a-332">HTTP_REFERER</span></span>
* <span data-ttu-id="33d9a-333">HTTP_URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-333">HTTP_URL</span></span>
* <span data-ttu-id="33d9a-334">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="33d9a-334">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="33d9a-335">HTTPS</span><span class="sxs-lookup"><span data-stu-id="33d9a-335">HTTPS</span></span>
* <span data-ttu-id="33d9a-336">LOCAL_ADDR</span><span class="sxs-lookup"><span data-stu-id="33d9a-336">LOCAL_ADDR</span></span>
* <span data-ttu-id="33d9a-337">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="33d9a-337">QUERY_STRING</span></span>
* <span data-ttu-id="33d9a-338">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="33d9a-338">REMOTE_ADDR</span></span>
* <span data-ttu-id="33d9a-339">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="33d9a-339">REMOTE_PORT</span></span>
* <span data-ttu-id="33d9a-340">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="33d9a-340">REQUEST_FILENAME</span></span>
* <span data-ttu-id="33d9a-341">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="33d9a-341">REQUEST_URI</span></span>

> [!NOTE]
> <span data-ttu-id="33d9a-342">È anche possibile ottenere un `IFileProvider` tramite un `PhysicalFileProvider`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-342">You can also obtain an `IFileProvider` via a `PhysicalFileProvider`.</span></span> <span data-ttu-id="33d9a-343">Questo approccio può garantire maggior flessibilità per la posizione dei file delle regole di riscrittura.</span><span class="sxs-lookup"><span data-stu-id="33d9a-343">This approach may provide greater flexibility for the location of your rewrite rules files.</span></span> <span data-ttu-id="33d9a-344">Assicurarsi che i file di regole di riscrittura vengano distribuiti nel server in corrispondenza del percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="33d9a-344">Make sure that your rewrite rules files are deployed to the server at the path you provide.</span></span>
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a><span data-ttu-id="33d9a-345">Regola basata su metodo</span><span class="sxs-lookup"><span data-stu-id="33d9a-345">Method-based rule</span></span>

<span data-ttu-id="33d9a-346">Usare `Add(Action<RewriteContext> applyRule)` per implementare logica della regola personalizzata in un metodo.</span><span class="sxs-lookup"><span data-stu-id="33d9a-346">Use `Add(Action<RewriteContext> applyRule)` to implement your own rule logic in a method.</span></span> <span data-ttu-id="33d9a-347">`RewriteContext` espone `HttpContext` per l'uso nel metodo.</span><span class="sxs-lookup"><span data-stu-id="33d9a-347">The `RewriteContext` exposes the `HttpContext` for use in your method.</span></span> <span data-ttu-id="33d9a-348">`RewriteContext.Result` determina la modalità di gestione dell'elaborazione pipeline aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="33d9a-348">The `RewriteContext.Result` determines how additional pipeline processing is handled.</span></span>

| `RewriteContext.Result`              | <span data-ttu-id="33d9a-349">Operazione</span><span class="sxs-lookup"><span data-stu-id="33d9a-349">Action</span></span>                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| <span data-ttu-id="33d9a-350">`RuleResult.ContinueRules` (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="33d9a-350">`RuleResult.ContinueRules` (default)</span></span> | <span data-ttu-id="33d9a-351">Continuare ad applicare le regole</span><span class="sxs-lookup"><span data-stu-id="33d9a-351">Continue applying rules</span></span>                                         |
| `RuleResult.EndResponse`             | <span data-ttu-id="33d9a-352">Interrompere l'applicazione delle regole e inviare la risposta</span><span class="sxs-lookup"><span data-stu-id="33d9a-352">Stop applying rules and send the response</span></span>                       |
| `RuleResult.SkipRemainingRules`      | <span data-ttu-id="33d9a-353">Interrompere l'applicazione delle regole e inviare il contesto al middleware seguente</span><span class="sxs-lookup"><span data-stu-id="33d9a-353">Stop applying rules and send the context to the next middleware</span></span> |

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=14)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(RedirectXMLRequests);

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-354">L'app di esempio visualizza un metodo che reindirizza le richieste per i percorsi che terminano con *.xml*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-354">The sample app demonstrates a method that redirects requests for paths that end with *.xml*.</span></span> <span data-ttu-id="33d9a-355">Se si esegue una richiesta per `/file.xml`, questa viene reindirizzata a `/xmlfiles/file.xml`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-355">If you make a request for `/file.xml`, it's redirected to `/xmlfiles/file.xml`.</span></span> <span data-ttu-id="33d9a-356">Il codice di stato è 301 (Spostato permanentemente).</span><span class="sxs-lookup"><span data-stu-id="33d9a-356">The status code is set to 301 (Moved Permanently).</span></span> <span data-ttu-id="33d9a-357">Per un reindirizzamento è necessario impostare in modo esplicito il codice di stato della risposta; in caso contrario viene restituito il codice di stato 200 (OK) e il reindirizzamento non viene eseguito sul client.</span><span class="sxs-lookup"><span data-stu-id="33d9a-357">For a redirect, you must explicitly set the status code of the response; otherwise, a 200 (OK) status code is returned and the redirect won't occur on the client.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet1)]

<span data-ttu-id="33d9a-358">Richiesta originale: `/file.xml`</span><span class="sxs-lookup"><span data-stu-id="33d9a-358">Original Request: `/file.xml`</span></span>

![Finestra del browser con strumenti di sviluppo per il rilevamento di richieste e risposte per file.xml](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a><span data-ttu-id="33d9a-360">Regola basata su IRule</span><span class="sxs-lookup"><span data-stu-id="33d9a-360">IRule-based rule</span></span>

<span data-ttu-id="33d9a-361">Usare `Add(IRule)` per incapsulare la logica della propria regola in una classe che implementa l'interfaccia `IRule`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-361">Use `Add(IRule)` to encapsulate your own rule logic in a class that implements the `IRule` interface.</span></span> <span data-ttu-id="33d9a-362">L'uso di un elemento `IRule` garantisce maggiore flessibilità rispetto all'approccio con una regola basata su un metodo.</span><span class="sxs-lookup"><span data-stu-id="33d9a-362">Using an `IRule` provides greater flexibility over using the method-based rule approach.</span></span> <span data-ttu-id="33d9a-363">La classe di implementazione può includere un costruttore, in cui è possibile passare parametri per il metodo `ApplyRule`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-363">Your implementaion class may include a constructor, where you can pass in parameters for the `ApplyRule` method.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=15-16)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="33d9a-364">I valori dei parametri nell'app di esempio per `extension` e `newPath` vengono verificati e devono soddisfare diverse condizioni.</span><span class="sxs-lookup"><span data-stu-id="33d9a-364">The values of the parameters in the sample app for the `extension` and the `newPath` are checked to meet several conditions.</span></span> <span data-ttu-id="33d9a-365">`extension` deve contenere un valore e tale valore deve essere *.png*, *.jpg* o *.gif*.</span><span class="sxs-lookup"><span data-stu-id="33d9a-365">The `extension` must contain a value, and the value must be *.png*, *.jpg*, or *.gif*.</span></span> <span data-ttu-id="33d9a-366">Se `newPath` non è valido, viene generato un evento `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-366">If the `newPath` isn't valid, an `ArgumentException` is thrown.</span></span> <span data-ttu-id="33d9a-367">Se si esegue una richiesta per *image.png*, questa viene reindirizzata a `/png-images/image.png`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-367">If you make a request for *image.png*, it's redirected to `/png-images/image.png`.</span></span> <span data-ttu-id="33d9a-368">Se si esegue una richiesta per *image.jpg*, questa viene reindirizzata a `/jpg-images/image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="33d9a-368">If you make a request for *image.jpg*, it's redirected to `/jpg-images/image.jpg`.</span></span> <span data-ttu-id="33d9a-369">Il codice di stato viene impostato su 301 (Spostato permanentemente) e l'elemento `context.Result` viene impostato per l'interruzione dell'elaborazione delle regole e l'invio della risposta.</span><span class="sxs-lookup"><span data-stu-id="33d9a-369">The status code is set to 301 (Moved Permanently), and the `context.Result` is set to stop processing rules and send the response.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet2)]

<span data-ttu-id="33d9a-370">Richiesta originale: `/image.png`</span><span class="sxs-lookup"><span data-stu-id="33d9a-370">Original Request: `/image.png`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte per image.png](url-rewriting/_static/add_redirect_png_requests.png)

<span data-ttu-id="33d9a-372">Richiesta originale: `/image.jpg`</span><span class="sxs-lookup"><span data-stu-id="33d9a-372">Original Request: `/image.jpg`</span></span>

![Finestra del browser con gli strumenti di sviluppo per il rilevamento di richieste e risposte per image.jpg](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a><span data-ttu-id="33d9a-374">Esempi di espressioni regolari</span><span class="sxs-lookup"><span data-stu-id="33d9a-374">Regex examples</span></span>

| <span data-ttu-id="33d9a-375">Obiettivo</span><span class="sxs-lookup"><span data-stu-id="33d9a-375">Goal</span></span> | <span data-ttu-id="33d9a-376">Esempio di stringa espressione regolare</span><span class="sxs-lookup"><span data-stu-id="33d9a-376">Regex String &</span></span><br><span data-ttu-id="33d9a-377">e corrispondenza</span><span class="sxs-lookup"><span data-stu-id="33d9a-377">Match Example</span></span> | <span data-ttu-id="33d9a-378">Esempio di stringa di sostituzione</span><span class="sxs-lookup"><span data-stu-id="33d9a-378">Replacement String &</span></span><br><span data-ttu-id="33d9a-379">e output</span><span class="sxs-lookup"><span data-stu-id="33d9a-379">Output Example</span></span> |
| ---- | :-----------------------------: | :------------------------------------: |
| <span data-ttu-id="33d9a-380">Riscrivere il percorso nella stringa di query</span><span class="sxs-lookup"><span data-stu-id="33d9a-380">Rewrite path into querystring</span></span> | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| <span data-ttu-id="33d9a-381">Rimuovere la barra finale</span><span class="sxs-lookup"><span data-stu-id="33d9a-381">Strip trailing slash</span></span> | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| <span data-ttu-id="33d9a-382">Applicare la barra finale</span><span class="sxs-lookup"><span data-stu-id="33d9a-382">Enforce trailing slash</span></span> | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| <span data-ttu-id="33d9a-383">Evitare la riscrittura di richieste specifiche</span><span class="sxs-lookup"><span data-stu-id="33d9a-383">Avoid rewriting specific requests</span></span> | <span data-ttu-id="33d9a-384">`^(.*)(?<!\.axd)$` o `^(?!.*\.axd$)(.*)$`</span><span class="sxs-lookup"><span data-stu-id="33d9a-384">`^(.*)(?<!\.axd)$` or `^(?!.*\.axd$)(.*)$`</span></span><br><span data-ttu-id="33d9a-385">Sì: `/resource.htm`</span><span class="sxs-lookup"><span data-stu-id="33d9a-385">Yes: `/resource.htm`</span></span><br><span data-ttu-id="33d9a-386">No: `/resource.axd`</span><span class="sxs-lookup"><span data-stu-id="33d9a-386">No: `/resource.axd`</span></span> | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| <span data-ttu-id="33d9a-387">Ridisporre i segmenti di URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-387">Rearrange URL segments</span></span> | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| <span data-ttu-id="33d9a-388">Sostituire un segmento di URL</span><span class="sxs-lookup"><span data-stu-id="33d9a-388">Replace a URL segment</span></span> | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a><span data-ttu-id="33d9a-389">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="33d9a-389">Additional resources</span></span>

* [<span data-ttu-id="33d9a-390">Avvio dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="33d9a-390">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="33d9a-391">Middleware</span><span class="sxs-lookup"><span data-stu-id="33d9a-391">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="33d9a-392">Espressioni regolari in .NET</span><span class="sxs-lookup"><span data-stu-id="33d9a-392">Regular expressions in .NET</span></span>](/dotnet/articles/standard/base-types/regular-expressions)
* [<span data-ttu-id="33d9a-393">Linguaggio di espressioni regolari - Riferimento rapido</span><span class="sxs-lookup"><span data-stu-id="33d9a-393">Regular expression language - quick reference</span></span>](/dotnet/articles/standard/base-types/quick-ref)
* [<span data-ttu-id="33d9a-394">Modulo Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="33d9a-394">Apache mod_rewrite</span></span>](https://httpd.apache.org/docs/2.4/rewrite/)
* <span data-ttu-id="33d9a-395">[Using Url Rewrite Module 2.0 (for IIS)](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) (Uso di URL Rewrite Module 2.0 per IIS)</span><span class="sxs-lookup"><span data-stu-id="33d9a-395">[Using Url Rewrite Module 2.0 (for IIS)](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)</span></span>
* <span data-ttu-id="33d9a-396">[URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference) (Guida di riferimento per la configurazione di URL Rewrite Module)</span><span class="sxs-lookup"><span data-stu-id="33d9a-396">[URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)</span></span>
* [<span data-ttu-id="33d9a-397">Forum di IIS URL Rewrite Module</span><span class="sxs-lookup"><span data-stu-id="33d9a-397">IIS URL Rewrite Module Forum</span></span>](https://forums.iis.net/1152.aspx)
* <span data-ttu-id="33d9a-398">[Keep a simple URL structure](https://support.google.com/webmasters/answer/76329?hl=en) (Mantenere una struttura URL semplice)</span><span class="sxs-lookup"><span data-stu-id="33d9a-398">[Keep a simple URL structure](https://support.google.com/webmasters/answer/76329?hl=en)</span></span>
* <span data-ttu-id="33d9a-399">[10 URL Rewriting Tips and Tricks](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/) (10 suggerimenti e consigli per la riscrittura URL)</span><span class="sxs-lookup"><span data-stu-id="33d9a-399">[10 URL Rewriting Tips and Tricks](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)</span></span>
* <span data-ttu-id="33d9a-400">[To slash or not to slash](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html) (Uso del carattere barra)</span><span class="sxs-lookup"><span data-stu-id="33d9a-400">[To slash or not to slash](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)</span></span>
