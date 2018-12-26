---
title: Novità di ASP.NET Core 2.2
author: tdykstra
description: Informazioni sulle nuove funzionalità di ASP.NET Core 2.2.
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/03/2018
uid: aspnetcore-2.2
ms.openlocfilehash: d0bb0698526e2f7af8f0e99b0393f3ce48657b34
ms.sourcegitcommit: a3a15d3ad4d6e160a69614a29c03bbd50db110a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2018
ms.locfileid: "52952057"
---
# <a name="whats-new-in-aspnet-core-22"></a><span data-ttu-id="1d85d-103">Novità di ASP.NET Core 2.2</span><span class="sxs-lookup"><span data-stu-id="1d85d-103">What's new in ASP.NET Core 2.2</span></span>

<span data-ttu-id="1d85d-104">Questo articolo evidenzia le modifiche più significative apportate ad ASP.NET Core 2.2, con collegamenti alla relativa documentazione.</span><span class="sxs-lookup"><span data-stu-id="1d85d-104">This article highlights the most significant changes in ASP.NET Core 2.2, with links to relevant documentation.</span></span>

## <a name="open-api-analyzers--conventions"></a><span data-ttu-id="1d85d-105">Convenzioni e analizzatori di OpenAPI</span><span class="sxs-lookup"><span data-stu-id="1d85d-105">Open API Analyzers & Conventions</span></span>

<span data-ttu-id="1d85d-106">OpenAPI, conosciuta anche come Swagger, è una specifica indipendente dal linguaggio per la descrizione delle API REST.</span><span class="sxs-lookup"><span data-stu-id="1d85d-106">Open API (also known as Swagger) is a language-agnostic specification for describing REST APIs.</span></span> <span data-ttu-id="1d85d-107">L'ecosistema OpenAPI include strumenti che consentono l'individuazione, il test e la produzione di codice client per mezzo della specifica.</span><span class="sxs-lookup"><span data-stu-id="1d85d-107">The Open API ecosystem has tools that allow for discovering, testing, and producing client code using the specification.</span></span> <span data-ttu-id="1d85d-108">Il supporto per la generazione e la visualizzazione di documenti OpenAPI in ASP.NET Core MVC è fornito tramite progetti gestiti dalla community, ad esempio [NSwag](https://github.com/RSuter/NSwag) e [Swashbuckle.AspNetCore](https://github.com/domaindrivendev/Swashbuckle.AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="1d85d-108">Support for generating and visualizing Open API documents in ASP.NET Core MVC is provided via community driven projects such as [NSwag](https://github.com/RSuter/NSwag), and [Swashbuckle.AspNetCore](https://github.com/domaindrivendev/Swashbuckle.AspNetCore).</span></span> <span data-ttu-id="1d85d-109">ASP.NET Core 2.2 offre strumenti ottimizzati e migliori esperienze con il runtime per la creazione di documenti OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="1d85d-109">ASP.NET Core 2.2 provides improved tooling and runtime experiences for creating Open API documents.</span></span>

<span data-ttu-id="1d85d-110">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="1d85d-110">For more information, see the following resources:</span></span>

* <xref:web-api/advanced/analyzers>
* <xref:web-api/advanced/conventions>
* [<span data-ttu-id="1d85d-111">ASP.NET Core 2.2.0-preview1: Convenzioni e analizzatori di OpenAPI</span><span class="sxs-lookup"><span data-stu-id="1d85d-111">ASP.NET Core 2.2.0-preview1: Open API Analyzers & Conventions</span></span>](https://blogs.msdn.microsoft.com/webdev/2018/08/23/asp-net-core-2-20-preview1-open-api-analyzers-conventions/)

## <a name="problem-details-support"></a><span data-ttu-id="1d85d-112">Assistenza per i dettagli del problema</span><span class="sxs-lookup"><span data-stu-id="1d85d-112">Problem details support</span></span>

<span data-ttu-id="1d85d-113">Con ASP.NET Core 2.1 è stata introdotta la classe `ProblemDetails`, basata sulla specifica RFC 7807, il cui compito è trasmettere i dettagli di un errore con una risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="1d85d-113">ASP.NET Core 2.1 introduced `ProblemDetails`, based on the RFC 7807 specification for carrying details of an error with an HTTP Response.</span></span> <span data-ttu-id="1d85d-114">Nella versione 2.2 `ProblemDetails` è la risposta standard per i codici di errore client nei controller a cui è stato attribuito `ApiControllerAttribute`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-114">In 2.2, `ProblemDetails` is the standard response for client error codes in controllers attributed with `ApiControllerAttribute`.</span></span> <span data-ttu-id="1d85d-115">Un'interfaccia `IActionResult` che restituisce un codice di stato per l'errore client (4xx) ora restituisce un corpo `ProblemDetails`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-115">An `IActionResult` returning a client error status code (4xx) now returns a `ProblemDetails` body.</span></span> <span data-ttu-id="1d85d-116">Il risultato include anche un ID di correlazione che può essere utilizzato per correlare l'errore usando i log richieste.</span><span class="sxs-lookup"><span data-stu-id="1d85d-116">The result also includes a correlation ID that can be used to correlate the error using request logs.</span></span> <span data-ttu-id="1d85d-117">Per gli errori client, per impostazione predefinita `ProducesResponseType` utilizza `ProblemDetails` come tipo di risposta.</span><span class="sxs-lookup"><span data-stu-id="1d85d-117">For client errors, `ProducesResponseType` defaults to using `ProblemDetails` as the response type.</span></span> <span data-ttu-id="1d85d-118">Ciò è documentato nell'output generato in OpenAPI/Swagger usando NSwag o Swashbuckle.AspNetCore.</span><span class="sxs-lookup"><span data-stu-id="1d85d-118">This is documented in Open API / Swagger output generated using NSwag or Swashbuckle.AspNetCore.</span></span>

## <a name="endpoint-routing"></a><span data-ttu-id="1d85d-119">Routing di endpoint</span><span class="sxs-lookup"><span data-stu-id="1d85d-119">Endpoint Routing</span></span>

<span data-ttu-id="1d85d-120">ASP.NET Core 2.2 prevede un nuovo sistema di *routing di endpoint* che rende più efficace l'invio delle richieste.</span><span class="sxs-lookup"><span data-stu-id="1d85d-120">ASP.NET Core 2.2 uses a new *endpoint routing* system for improved dispatching of requests.</span></span> <span data-ttu-id="1d85d-121">Le modifiche includono una nuova funzione di generazione dei collegamenti per i membri dell'API e l'aggiunta di trasformatori per i parametri di routing.</span><span class="sxs-lookup"><span data-stu-id="1d85d-121">The changes include new link generation API members and route parameter transformers.</span></span>

<span data-ttu-id="1d85d-122">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="1d85d-122">For more information, see the following resources:</span></span>

* <span data-ttu-id="1d85d-123">[Endpoint routing in 2.2](https://blogs.msdn.microsoft.com/webdev/2018/08/27/asp-net-core-2-2-0-preview1-endpoint-routing/) (Routing di endpoint in 2.2)</span><span class="sxs-lookup"><span data-stu-id="1d85d-123">[Endpoint routing in 2.2](https://blogs.msdn.microsoft.com/webdev/2018/08/27/asp-net-core-2-2-0-preview1-endpoint-routing/)</span></span>
* <span data-ttu-id="1d85d-124">[Parameter transformers](https://www.hanselman.com/blog/ASPNETCore22ParameterTransformersForCleanURLGenerationAndSlugsInRazorPagesOrMVC.aspx) (Trasformatori dei parametri), sezione **Routing**</span><span class="sxs-lookup"><span data-stu-id="1d85d-124">[Route parameter transformers](https://www.hanselman.com/blog/ASPNETCore22ParameterTransformersForCleanURLGenerationAndSlugsInRazorPagesOrMVC.aspx) (see **Routing** section)</span></span>
* [<span data-ttu-id="1d85d-125">Differenze tra IRouter e routing basati su endpoint</span><span class="sxs-lookup"><span data-stu-id="1d85d-125">Differences between IRouter- and endpoint-based routing</span></span>](xref:fundamentals/routing?view=aspnetcore-2.2#differences-from-earlier-versions-of-routing)

## <a name="health-checks"></a><span data-ttu-id="1d85d-126">Controlli di integrità</span><span class="sxs-lookup"><span data-stu-id="1d85d-126">Health checks</span></span>

<span data-ttu-id="1d85d-127">Un nuovo servizio di controllo di integrità rende più semplice usare ASP.NET Core in ambienti che richiedono controlli di integrità, ad esempio Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1d85d-127">A new health checks service makes it easier to use ASP.NET Core in environments that require health checks, such as Kubernetes.</span></span> <span data-ttu-id="1d85d-128">I controlli di integrità includono middleware e un set di librerie che definiscono il servizio e un'astrazione `IHealthCheck`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-128">Health checks includes middleware and a set of libraries that define an `IHealthCheck` abstraction and service.</span></span>

<span data-ttu-id="1d85d-129">Tramite i controlli di integrità, un agente di orchestrazione o un servizio di bilanciamento del carico determina rapidamente se un sistema risponde normalmente alle richieste.</span><span class="sxs-lookup"><span data-stu-id="1d85d-129">Health checks are used by a container orchestrator or load balancer to quickly determine if a system is responding to requests normally.</span></span> <span data-ttu-id="1d85d-130">Un agente di orchestrazione potrebbe rispondere a un controllo di integrità non superato arrestando una distribuzione in sequenza o riavviando un contenitore.</span><span class="sxs-lookup"><span data-stu-id="1d85d-130">A container orchestrator might respond to a failing health check by halting a rolling deployment or restarting a container.</span></span> <span data-ttu-id="1d85d-131">Un servizio di bilanciamento del carico potrebbe reagire a un controllo di integrità deviando il traffico dall'istanza con errori del servizio.</span><span class="sxs-lookup"><span data-stu-id="1d85d-131">A load balancer might respond to a health check by routing traffic away from the failing instance of the service.</span></span>

<span data-ttu-id="1d85d-132">I controlli di integrità vengono esposti da un'applicazione come endpoint HTTP utilizzato dai sistemi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="1d85d-132">Health checks are exposed by an application as an HTTP endpoint used by monitoring systems.</span></span> <span data-ttu-id="1d85d-133">È possibile configurare i controlli di integrità per svariati scenari di monitoraggio in tempo reale e sistemi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="1d85d-133">Health checks can be configured for a variety of real-time monitoring scenarios and monitoring systems.</span></span> <span data-ttu-id="1d85d-134">Il servizio dei controlli di integrità si integra con il [progetto BeatPulse](https://github.com/Xabaril/BeatPulse)</span><span class="sxs-lookup"><span data-stu-id="1d85d-134">The health checks service integrates with the [BeatPulse project](https://github.com/Xabaril/BeatPulse).</span></span> <span data-ttu-id="1d85d-135">che rende più semplice aggiungere controlli per decine di dipendenze e di sistemi più diffusi.</span><span class="sxs-lookup"><span data-stu-id="1d85d-135">which makes it easier to add checks for dozens of popular systems and dependencies.</span></span>

<span data-ttu-id="1d85d-136">Per altre informazioni, vedere [Controlli di integrità in ASP.NET Core](xref:host-and-deploy/health-checks).</span><span class="sxs-lookup"><span data-stu-id="1d85d-136">For more information, see [Health checks in ASP.NET Core](xref:host-and-deploy/health-checks).</span></span>

## <a name="http2-in-kestrel"></a><span data-ttu-id="1d85d-137">HTTP/2 in Kestrel</span><span class="sxs-lookup"><span data-stu-id="1d85d-137">HTTP/2 in Kestrel</span></span>

<span data-ttu-id="1d85d-138">In ASP.NET Core 2.2 è stato aggiunto il supporto per HTTP/2.</span><span class="sxs-lookup"><span data-stu-id="1d85d-138">ASP.NET Core 2.2 adds support for HTTP/2.</span></span> 

<span data-ttu-id="1d85d-139">HTTP/2 è una revisione principale del protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="1d85d-139">HTTP/2 is a major revision of the HTTP protocol.</span></span> <span data-ttu-id="1d85d-140">Alcune delle funzionalità degne di nota di HTTP/2 sono il supporto per la compressione delle intestazioni e la trasmissione di flussi multiplex completi con una singola connessione.</span><span class="sxs-lookup"><span data-stu-id="1d85d-140">Some of the notable features of HTTP/2 are support for header compression and fully multiplexed streams over a single connection.</span></span> <span data-ttu-id="1d85d-141">Pur conservando la semantica tipica di HTTP (intestazioni HTTP, metodi e così via), HTTP/2 presenta sostanziali novità rispetto a HTTP/1.x in merito al modo in cui questi dati vengono inseriti in un frame e trasmessi in rete.</span><span class="sxs-lookup"><span data-stu-id="1d85d-141">While HTTP/2 preserves HTTP’s semantics (HTTP headers, methods, etc) it's a breaking change from HTTP/1.x on how this data is framed and sent over the wire.</span></span>

<span data-ttu-id="1d85d-142">Come conseguenza di questa modifica del framing, i server e i client devono negoziare la versione del protocollo usata.</span><span class="sxs-lookup"><span data-stu-id="1d85d-142">As a consequence of this change in framing, servers and clients need to negotiate the protocol version used.</span></span> <span data-ttu-id="1d85d-143">ALPN (Application Layer Protocol Negotiation) è un'estensione TLS che consente al server e al client di negoziare la versione del protocollo usata nel corso dell'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="1d85d-143">Application-Layer Protocol Negotiation (ALPN) is a TLS extension that allows the server and client negotiate the protocol version used as part of their TLS handshake.</span></span> <span data-ttu-id="1d85d-144">Sebbene sia possibile che il server e il client dispongano di conoscenze precedenti rispetto al protocollo, tutti i principali browser supportano ALPN e la considerano l'unico modo per stabilire una connessione HTTP/2.</span><span class="sxs-lookup"><span data-stu-id="1d85d-144">While it is possible to have prior knowledge between the server and the client on the protocol, all major browsers support ALPN as the only way to establish an HTTP/2 connection.</span></span>

<span data-ttu-id="1d85d-145">Per altre informazioni, vedere [Supporto per HTTP/2](xref:fundamentals/servers/index?view=aspnetcore-2.2#http2-support).</span><span class="sxs-lookup"><span data-stu-id="1d85d-145">For more information, see [HTTP/2 support](xref:fundamentals/servers/index?view=aspnetcore-2.2#http2-support).</span></span>

## <a name="kestrel-configuration"></a><span data-ttu-id="1d85d-146">Configurazione di Kestrel</span><span class="sxs-lookup"><span data-stu-id="1d85d-146">Kestrel configuration</span></span>

<span data-ttu-id="1d85d-147">Nelle versioni precedenti di ASP.NET Core, le opzioni di Kestrel venivano configurate chiamando `UseKestrel`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-147">In earlier versions of ASP.NET Core, Kestrel options are configured by calling `UseKestrel`.</span></span> <span data-ttu-id="1d85d-148">Nella versione 2.2, le opzioni di Kestrel sono configurate chiamando `ConfigureKestrel` nel generatore di host.</span><span class="sxs-lookup"><span data-stu-id="1d85d-148">In 2.2, Kestrel options are configured by calling `ConfigureKestrel` on the host builder.</span></span> <span data-ttu-id="1d85d-149">Questa modifica risolve un problema legato all'ordine delle registrazioni `IServer` per l'hosting in-process.</span><span class="sxs-lookup"><span data-stu-id="1d85d-149">This change resolves an issue with the order of `IServer` registrations for in-process hosting.</span></span> <span data-ttu-id="1d85d-150">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="1d85d-150">For more information, see the following resources:</span></span>

* <span data-ttu-id="1d85d-151">[Mitigate UseIIS conflict](https://github.com/aspnet/KestrelHttpServer/issues/2760) (Ridurre i conflitti UseIIS)</span><span class="sxs-lookup"><span data-stu-id="1d85d-151">[Mitigate UseIIS conflict](https://github.com/aspnet/KestrelHttpServer/issues/2760)</span></span>
* [<span data-ttu-id="1d85d-152">Configurare le opzioni del server Kestrel con ConfigureKestrel</span><span class="sxs-lookup"><span data-stu-id="1d85d-152">Configure Kestrel server options with ConfigureKestrel</span></span>](xref:fundamentals/servers/kestrel?view=aspnetcore-2.2#how-to-use-kestrel-in-aspnet-core-apps)

## <a name="iis-in-process-hosting"></a><span data-ttu-id="1d85d-153">Hosting in-process IIS</span><span class="sxs-lookup"><span data-stu-id="1d85d-153">IIS in-process hosting</span></span>

<span data-ttu-id="1d85d-154">Nelle versioni precedenti di ASP.NET Core, IIS funge da proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="1d85d-154">In earlier versions of ASP.NET Core, IIS serves as a reverse proxy.</span></span> <span data-ttu-id="1d85d-155">Nella versione 2.2, il modulo ASP.NET Core può avviare CoreCLR e ospitare un'app all'interno del processo di lavoro IIS (*w3wp.exe*).</span><span class="sxs-lookup"><span data-stu-id="1d85d-155">In 2.2, the ASP.NET Core Module can boot the CoreCLR and host an app inside the IIS worker process (*w3wp.exe*).</span></span> <span data-ttu-id="1d85d-156">Durante l'esecuzione con IIS, l'hosting in-process offre prestazioni e risultati di diagnostica migliori.</span><span class="sxs-lookup"><span data-stu-id="1d85d-156">In-process hosting provides performance and diagnostic gains when running with IIS.</span></span>

<span data-ttu-id="1d85d-157">Per altre informazioni, vedere [Hosting in-process IIS](xref:fundamentals/servers/aspnet-core-module?view=aspnetcore-2.2#in-process-hosting-model).</span><span class="sxs-lookup"><span data-stu-id="1d85d-157">For more information, see [IIS in-process hosting](xref:fundamentals/servers/aspnet-core-module?view=aspnetcore-2.2#in-process-hosting-model).</span></span>

## <a name="signalr-java-client"></a><span data-ttu-id="1d85d-158">Client Java per SignalR</span><span class="sxs-lookup"><span data-stu-id="1d85d-158">SignalR Java client</span></span>

<span data-ttu-id="1d85d-159">ASP.NET Core 2.2 introduce un client Java per SignalR.</span><span class="sxs-lookup"><span data-stu-id="1d85d-159">ASP.NET Core 2.2 introduces a Java Client for SignalR.</span></span> <span data-ttu-id="1d85d-160">Questo client supporta la connessione a un server SignalR di ASP.NET Core dal codice Java, incluse le app Android.</span><span class="sxs-lookup"><span data-stu-id="1d85d-160">This client supports connecting to an ASP.NET Core SignalR Server from Java code, including Android apps.</span></span>

<span data-ttu-id="1d85d-161">Per altre informazioni, vedere [ASP.NET Core SignalR Java client](https://docs.microsoft.com/aspnet/core/signalr/java-client?view=aspnetcore-2.2) (Client Java per SignalR di ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="1d85d-161">For more information, see [ASP.NET Core SignalR Java client](https://docs.microsoft.com/aspnet/core/signalr/java-client?view=aspnetcore-2.2).</span></span>

## <a name="cors-improvements"></a><span data-ttu-id="1d85d-162">Miglioramenti a CORS</span><span class="sxs-lookup"><span data-stu-id="1d85d-162">CORS improvements</span></span>

<span data-ttu-id="1d85d-163">Nelle versioni precedenti di ASP.NET Core, middleware CORS consente l'invio delle intestazioni `Accept`, `Accept-Language`, `Content-Language` e `Origin` indipendentemente dai valori configurati in `CorsPolicy.Headers`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-163">In earlier versions of ASP.NET Core, CORS Middleware allows `Accept`, `Accept-Language`, `Content-Language`, and `Origin` headers to be sent regardless of the values configured in `CorsPolicy.Headers`.</span></span> <span data-ttu-id="1d85d-164">Nella versione 2.2 è possibile stabilire una corrispondenza dei criteri di middleware CORS solo quando le intestazioni inviate in `Access-Control-Request-Headers` corrispondono esattamente alle intestazioni indicate in `WithHeaders`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-164">In 2.2, a CORS Middleware policy match is only possible when the headers sent in `Access-Control-Request-Headers` exactly match the headers stated in `WithHeaders`.</span></span>

<span data-ttu-id="1d85d-165">Per altre informazioni, vedere [CORS Middleware](xref:security/cors?view=aspnetcore-2.2#set-the-allowed-request-headers).</span><span class="sxs-lookup"><span data-stu-id="1d85d-165">For more information, see [CORS Middleware](xref:security/cors?view=aspnetcore-2.2#set-the-allowed-request-headers).</span></span>

## <a name="response-compression"></a><span data-ttu-id="1d85d-166">Compressione delle risposte</span><span class="sxs-lookup"><span data-stu-id="1d85d-166">Response compression</span></span>

<span data-ttu-id="1d85d-167">Con ASP.NET Core 2.2 è possibile comprimere le risposte con il [formato di compressione Brotli](https://tools.ietf.org/html/rfc7932).</span><span class="sxs-lookup"><span data-stu-id="1d85d-167">ASP.NET Core 2.2 can compress responses with the [Brotli compression format](https://tools.ietf.org/html/rfc7932).</span></span>

<span data-ttu-id="1d85d-168">Per altre informazioni, vedere [Brotli Compression Provider](xref:performance/response-compression?view=aspnetcore-2.2#brotli-compression-provider) (Provider compressione Brotli).</span><span class="sxs-lookup"><span data-stu-id="1d85d-168">For more information, see [Response Compression Middleware supports Brotli compression](xref:performance/response-compression?view=aspnetcore-2.2#brotli-compression-provider).</span></span>

## <a name="project-templates"></a><span data-ttu-id="1d85d-169">Modelli di progetto</span><span class="sxs-lookup"><span data-stu-id="1d85d-169">Project templates</span></span>

<span data-ttu-id="1d85d-170">I modelli di progetto Web ASP.NET Core sono stati aggiornati a [Bootstrap 4](https://getbootstrap.com/docs/4.1/migration/) e [Angular 6](https://blog.angular.io/version-6-of-angular-now-available-cc56b0efa7a4).</span><span class="sxs-lookup"><span data-stu-id="1d85d-170">ASP.NET Core web project templates were updated to [Bootstrap 4](https://getbootstrap.com/docs/4.1/migration/) and [Angular 6](https://blog.angular.io/version-6-of-angular-now-available-cc56b0efa7a4).</span></span> <span data-ttu-id="1d85d-171">Il nuovo aspetto è visivamente più immediato e rende più facile visualizzare le strutture importanti dell'app.</span><span class="sxs-lookup"><span data-stu-id="1d85d-171">The new look is visually simpler and makes it easier to see the important structures of the app.</span></span>

![Pagina Home o di indice](~/tutorials/razor-pages/razor-pages-start/_static/home2.2.png)

## <a name="validation-performance"></a><span data-ttu-id="1d85d-173">Prestazioni della convalida</span><span class="sxs-lookup"><span data-stu-id="1d85d-173">Validation performance</span></span>

<span data-ttu-id="1d85d-174">Il sistema di convalida di MVC è progettato per essere estensibile e flessibile e per consentire di determinare quali validator sono applicabili a un dato modello per le singole richieste.</span><span class="sxs-lookup"><span data-stu-id="1d85d-174">MVC’s validation system is designed to be extensible and flexible, allowing you to determine on a per request basis which validators apply to a given model.</span></span> <span data-ttu-id="1d85d-175">Ciò è molto utile per la creazione di provider di convalida complessi.</span><span class="sxs-lookup"><span data-stu-id="1d85d-175">This is great for authoring complex validation providers.</span></span> <span data-ttu-id="1d85d-176">In genere, tuttavia, le applicazioni utilizzano solo i validator incorporati e non richiedono questa flessibilità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="1d85d-176">However, in the most common case an application only uses the built-in validators and don’t require this extra flexibility.</span></span> <span data-ttu-id="1d85d-177">I validator incorporati includono DataAnnotations, ad esempio [Required], [StringLength] e `IValidatableObject`.</span><span class="sxs-lookup"><span data-stu-id="1d85d-177">Built-in validators include DataAnnotations such as [Required] and [StringLength], and `IValidatableObject`.</span></span>

<span data-ttu-id="1d85d-178">In ASP.NET Core 2.2 MVC può bloccare la convalida se determina che un grafico del modello specifico non richiede la convalida.</span><span class="sxs-lookup"><span data-stu-id="1d85d-178">In ASP.NET Core 2.2, MVC can short-circuit validation if it determines that a given model graph doesn't require validation.</span></span> <span data-ttu-id="1d85d-179">Ignorando la convalida si ottengono miglioramenti significativi per i modelli che non hanno o non possono avere alcun validator.</span><span class="sxs-lookup"><span data-stu-id="1d85d-179">Skipping validation results in significant improvements when validating models that can't or don't have any validators.</span></span> <span data-ttu-id="1d85d-180">Ciò riguarda oggetti quali raccolte di primitive (`byte[]`, `string[]`, `Dictionary<string, string>` e così via) o oggetti grafici complessi senza molti validator.</span><span class="sxs-lookup"><span data-stu-id="1d85d-180">This includes objects such as collections of primitives (such as `byte[]`, `string[]`, `Dictionary<string, string>`), or complex object graphs without many validators.</span></span>

## <a name="http-client-performance"></a><span data-ttu-id="1d85d-181">Prestazioni del client HTTP</span><span class="sxs-lookup"><span data-stu-id="1d85d-181">HTTP Client performance</span></span>

<span data-ttu-id="1d85d-182">In ASP.NET Core 2.2 le prestazioni di `SocketsHttpHandler` sono state migliorate riducendo la contesa di blocco dei pool di connessioni.</span><span class="sxs-lookup"><span data-stu-id="1d85d-182">In ASP.NET Core 2.2, the performance of `SocketsHttpHandler` was improved by reducing connection pool locking contention.</span></span> <span data-ttu-id="1d85d-183">Per le app che generano molte richieste HTTP in uscita, ad esempio alcune architetture di microservizi, la velocità effettiva risulta migliorata.</span><span class="sxs-lookup"><span data-stu-id="1d85d-183">For apps that make many outgoing HTTP requests, such as some microservices architectures, throughput is improved.</span></span> <span data-ttu-id="1d85d-184">In condizioni di carico, la velocità effettiva di `HttpClient` può essere migliorata fino al 60% in Linux e al 20% in Windows.</span><span class="sxs-lookup"><span data-stu-id="1d85d-184">Under load, `HttpClient` throughput can be improved by up to 60% on Linux and 20% on Windows.</span></span>

<span data-ttu-id="1d85d-185">Per altre informazioni, vedere [la richiesta pull responsabile di questo miglioramento](https://github.com/dotnet/corefx/pull/32568).</span><span class="sxs-lookup"><span data-stu-id="1d85d-185">For more information, see [the pull request that made this improvement](https://github.com/dotnet/corefx/pull/32568).</span></span>

## <a name="additional-information"></a><span data-ttu-id="1d85d-186">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1d85d-186">Additional information</span></span>

<span data-ttu-id="1d85d-187">Per l'elenco completo delle modifiche, vedere le [Note sulla versione di ASP.NET Core 2.2](https://github.com/aspnet/Home/releases/tag/2.2.0).</span><span class="sxs-lookup"><span data-stu-id="1d85d-187">For the complete list of changes, see the [ASP.NET Core 2.2 Release Notes](https://github.com/aspnet/Home/releases/tag/2.2.0).</span></span>