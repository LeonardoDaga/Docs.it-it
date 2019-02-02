---
title: Esempi di autenticazione per ASP.NET Core
author: rick-anderson
description: Vengono forniti collegamenti agli esempi di autenticazione nel repository di ASP.NET Core.
ms.author: riande
ms.date: 01/31/2019
uid: security/authentication/samples
ms.openlocfilehash: 7b3c911d60ad4737ebd12ce6f7628ad624b11658
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236675"
---
# <a name="authentication-samples-for-aspnet-core"></a><span data-ttu-id="e72bc-103">Esempi di autenticazione per ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e72bc-103">Authentication samples for ASP.NET Core</span></span>

<span data-ttu-id="e72bc-104">Di [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e72bc-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e72bc-105">Il [repository di ASP.NET Core](https://github.com/aspnet/AspNetCore) contiene i seguenti esempi di autenticazione nella *AspNetCore/src/Security/samples* cartella:</span><span class="sxs-lookup"><span data-stu-id="e72bc-105">The [ASP.NET Core repository](https://github.com/aspnet/AspNetCore) contains the following authentication samples in the *AspNetCore/src/Security/samples* folder:</span></span>

* [<span data-ttu-id="e72bc-106">Trasformazione delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="e72bc-106">Claims transformation</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/ClaimsTransformation)
* [<span data-ttu-id="e72bc-107">Autenticazione tramite cookie</span><span class="sxs-lookup"><span data-stu-id="e72bc-107">Cookie authentication</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Cookies)
* [<span data-ttu-id="e72bc-108">Provider di criteri personalizzati - IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="e72bc-108">Custom policy provider - IAuthorizationPolicyProvider</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider)
* [<span data-ttu-id="e72bc-109">Opzioni e gli schemi di autenticazione dinamica</span><span class="sxs-lookup"><span data-stu-id="e72bc-109">Dynamic authentication schemes and options</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/DynamicSchemes)
* [<span data-ttu-id="e72bc-110">Attestazioni esterno</span><span class="sxs-lookup"><span data-stu-id="e72bc-110">External claims</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Identity.ExternalClaims)
* [<span data-ttu-id="e72bc-111">Selezione di un altro schema di autenticazione basate sulla richiesta e senza cookie</span><span class="sxs-lookup"><span data-stu-id="e72bc-111">Selecting between cookie and another authentication scheme based on the request</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/PathSchemeSelection)
* [<span data-ttu-id="e72bc-112">Limita l'accesso ai file statici</span><span class="sxs-lookup"><span data-stu-id="e72bc-112">Restricts access to static files</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/StaticFilesAuth)

## <a name="run-the-samples"></a><span data-ttu-id="e72bc-113">Eseguire gli esempi</span><span class="sxs-lookup"><span data-stu-id="e72bc-113">Run the samples</span></span>

* <span data-ttu-id="e72bc-114">Selezionare una [ramo](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="e72bc-114">Select a [branch](https://github.com/aspnet/AspNetCore).</span></span> <span data-ttu-id="e72bc-115">Ad esempio, `release/2.2`.</span><span class="sxs-lookup"><span data-stu-id="e72bc-115">For example, `release/2.2`</span></span>
* <span data-ttu-id="e72bc-116">Clonare o scaricare il [repository di ASP.NET Core](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="e72bc-116">Clone or download the [ASP.NET Core repository](https://github.com/aspnet/AspNetCore).</span></span>
* <span data-ttu-id="e72bc-117">Verificare di aver installato il [.NET Core SDK](https://www.microsoft.com/net/download/all) versione che corrisponde il clone del repository ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e72bc-117">Verify you have installed the [.NET Core SDK](https://www.microsoft.com/net/download/all) version matching the clone of the ASP.NET Core repository.</span></span>
* <span data-ttu-id="e72bc-118">Passare a un esempio nella *AspNetCore/src/Security/samples* ed eseguire l'esempio con `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="e72bc-118">Navigate to a sample in *AspNetCore/src/Security/samples* and run the sample with `dotnet run`.</span></span>