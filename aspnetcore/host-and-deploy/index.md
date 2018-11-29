---
title: Hosting e distribuzione di ASP.NET Core
author: rick-anderson
description: Informazioni sulla configurazione degli ambienti host e sulla distribuzione delle app ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 11/26/2018
uid: host-and-deploy/index
ms.openlocfilehash: f70b05df6bf710e2ab54a1eaafb71b4f9b306cbe
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450619"
---
# <a name="host-and-deploy-aspnet-core"></a>Hosting e distribuzione di ASP.NET Core

In generale, per distribuire un'app ASP.NET Core in un ambiente host:

* Pubblicare l'app in una cartella nel server host.
* Configurare un gestore processi che avvia l'app quando arrivano richieste e la riavvia quando si blocca o quando il server viene riavviato.
* Se è necessario eseguire la configurazione di un proxy inverso, configurare un proxy inverso che inoltra le richieste all'app.

## <a name="publish-to-a-folder"></a>Pubblicare in una cartella

Il comando CLI [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) compila il codice dell'app e copia i file necessari per eseguire l'app in una cartella *publish*. Quando si esegue la distribuzione da Visual Studio, il passaggio [dotnet publish](/dotnet/core/tools/dotnet-publish) viene eseguito automaticamente prima della copia dei file nella destinazione di distribuzione.

### <a name="folder-contents"></a>Contenuto della cartella

La cartella *publish* contiene i file dell'app con estensione *exe* e *dll*, le relative dipendenze e facoltativamente il runtime .NET.

È possibile pubblicare un'app .NET Core come app *indipendente* o come app *dipendente dal framework*. Se l'app è indipendente i file con estensione *DLL* che contengono il runtime .NET sono inclusi nella cartella *publish*. Se l'app è dipendente dal framework, i file di runtime .NET non sono inclusi, perché l'app contiene un riferimento a una versione di .NET installata nel server. Il modello di distribuzione predefinito è il modello dipendente dal framework. Per altre informazioni, vedere [Distribuzione di applicazioni .NET Core](/dotnet/articles/core/deploying/index).

Oltre ai file con estensione *EXE* e *DLL* la cartella *publish* di un'app ASP.NET Core contiene in genere i file di configurazione, gli asset statici e le visualizzazioni MVC. Per ulteriori informazioni, vedere <xref:host-and-deploy/directory-structure>.

## <a name="set-up-a-process-manager"></a>Configurare un gestore processi

Un'app ASP.NET Core è un'app console che deve essere avviata all'avvio di un server e riavviata in caso di arresto anomalo del server stesso. Per automatizzare le operazioni di avvio e riavvio, deve essere presente un gestore processi. I gestori processi più comuni per ASP.NET Core sono:

* Linux
  * [Nginx](xref:host-and-deploy/linux-nginx)
  * [Apache](xref:host-and-deploy/linux-apache)
* WINDOWS
  * [IIS](xref:host-and-deploy/iis/index)
  * [Servizio Windows](xref:host-and-deploy/windows-service)

## <a name="set-up-a-reverse-proxy"></a>Configurare un proxy inverso

::: moniker range=">= aspnetcore-2.0"

Se l'app usa il servizio Web [Kestrel](xref:fundamentals/servers/kestrel) è possibile usare come server proxy inverso [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) o [IIS](xref:host-and-deploy/iis/index). Un server proxy inverso riceve le richieste HTTP da Internet e le inoltra a Kestrel dopo alcune operazioni di gestione preliminari.

Entrambe le configurazioni (con o senza un server proxy inverso) sono configurazioni di hosting valide e supportate per le app ASP.NET Core 2.0 o versioni successive. Per altre informazioni, vedere [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy) (Quando usare Kestrel con un proxy inverso).

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Se l'app usa il server Web [Kestrel](xref:fundamentals/servers/kestrel) ed è esposta a Internet, usare [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) o [IIS](xref:host-and-deploy/iis/index) come server proxy inverso. Un server proxy inverso riceve le richieste HTTP da Internet e le inoltra a Kestrel dopo alcune operazioni di gestione preliminari. Il motivo principale per l'uso di un proxy inverso è la sicurezza. Per altre informazioni, vedere [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel?tabs=aspnetcore1x#when-to-use-kestrel-with-a-reverse-proxy) (Quando usare Kestrel con un proxy inverso).

::: moniker-end

## <a name="proxy-server-and-load-balancer-scenarios"></a>Scenari con server proxy e servizi di bilanciamento del carico

Potrebbero essere necessari interventi di configurazione aggiuntivi per le app ospitate dietro a server proxy e a servizi di bilanciamento del carico. Senza alcuna configurazione aggiuntiva, un'app potrebbe non avere accesso allo schema (HTTP/HTTPS) e all'indirizzo IP remoto di origine di una richiesta. Per altre informazioni, vedere [Configurare ASP.NET Core per l'utilizzo di server proxy e servizi di bilanciamento del carico](xref:host-and-deploy/proxy-load-balancer).

## <a name="use-visual-studio-and-msbuild-to-automate-deployments"></a>Usare Visual Studio e MSBuild per automatizzare le distribuzioni

In molti casi la distribuzione richiede attività aggiuntive oltre alla copia dell'output da [dotnet publish](/dotnet/core/tools/dotnet-publish) a un server. Ad esempio è possibile che nella cartella *publish* siano necessari file aggiuntivi o vengano esclusi uno o più file. Per la distribuzione Web, Visual Studio usa MSBuild, che può essere personalizzato per eseguire molte altre attività durante la distribuzione. Per altre informazioni, vedere <xref:host-and-deploy/visual-studio-publish-profiles> e il libro [Using MSBuild and Team Foundation Build](http://msbuildbook.com/) (Uso di MSBuild e Team Foundation Build).

Mediante la [funzionalità Pubblica sito Web](xref:tutorials/publish-to-azure-webapp-using-vs) o il [supporto di Git incorporato](xref:host-and-deploy/azure-apps/azure-continuous-deployment) è possibile eseguire direttamente la distribuzione di app da Visual Studio al Servizio app di Azure. Azure DevOps Services supporta la [distribuzione continua al Servizio app di Azure](/azure/devops/pipelines/targets/webapp).

## <a name="publish-to-azure"></a>Pubblicare in Azure

Vedere <xref:tutorials/publish-to-azure-webapp-using-vs> per istruzioni su come pubblicare un'app in Azure usando Visual Studio. L'app può essere pubblicata in Azure anche dalla [riga di comando](/azure/app-service/app-service-web-get-started-dotnet).

## <a name="host-in-a-web-farm"></a>Hosting in una Web farm

Per informazioni sulla configurazione per ospitare app ASP.NET Core in un ambiente Web farm (ad esempio, distribuzione di più istanze di un'app per la scalabilità), vedere <xref:host-and-deploy/web-farm>.

## <a name="additional-resources"></a>Risorse aggiuntive

* <xref:host-and-deploy/docker/index>
* <xref:test/troubleshoot>
