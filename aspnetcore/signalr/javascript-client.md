---
title: ASP.NET Core SignalR JavaScript client
author: tdykstra
description: Panoramica di ASP.NET Core SignalR JavaScript client.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: 02844c35d1933d36576c25ff335a572fb65eff5c
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2018
ms.locfileid: "50208018"
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET Core SignalR JavaScript client

[Rachel Appel](http://twitter.com/rachelappel)

La libreria client di ASP.NET Core SignalR JavaScript consente agli sviluppatori di chiamare il codice dell'hub sul lato server.

[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([procedura per il download](xref:index#how-to-download-a-sample))

## <a name="install-the-signalr-client-package"></a>Installare il pacchetto client di SignalR

La libreria client SignalR JavaScript viene fornita come un [npm](https://www.npmjs.com/) pacchetto. Se si usa Visual Studio, eseguire `npm install` dal **Console di gestione pacchetti** mentre si trovano nella cartella radice. Per Visual Studio Code, eseguire il comando dal **terminale integrato**.

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

Monitoraggio prestazioni rete consente di installare il contenuto del pacchetto nel *node_modules\\@aspnet\signalr\dist\browser* cartella. Creare una nuova cartella denominata *signalr* sotto il *wwwroot\\lib* cartella. Copia il *signalr.js* del file per il *wwwroot\lib\signalr* cartella.

## <a name="use-the-signalr-javascript-client"></a>Usare il client SignalR JavaScript

Fare riferimento a client SignalR JavaScript il `<script>` elemento.

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>Connettersi a un hub

Il codice seguente crea e avvia una connessione. Nome dell'hub è maiuscole e minuscole.

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a>Connessioni cross-origin

In genere, i browser il carico delle connessioni appartenenti allo stesso dominio della pagina richiesta. Tuttavia, esistono alcuni casi quando è necessaria una connessione a un altro dominio.

Per impedire la lettura dei dati sensibili da un altro sito, di un sito dannoso [le connessioni cross-origin](xref:security/cors) sono disabilitati per impostazione predefinita. Per consentire a una richiesta multiorigine, abilitarla nel `Startup` classe.

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a>Chiamare i metodi dell'hub da client

Client JavaScript chiamano metodi pubblici in hub tramite il [richiamare](/javascript/api/%40aspnet/signalr/hubconnection#invoke) metodo per il [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection). Il `invoke` metodo accetta due argomenti:

* Il nome del metodo dell'hub. Nell'esempio seguente, è il nome del metodo dell'hub `SendMessage`.
* Eventuali argomenti definiti nel metodo dell'hub. Nell'esempio seguente, è il nome dell'argomento `message`.

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a>Chiamare i metodi client hub

Per ricevere messaggi dall'hub, definire un metodo usando il [sul](/javascript/api/%40aspnet/signalr/hubconnection#on) metodo del `HubConnection`.

* Il nome del metodo client JavaScript. Nell'esempio seguente, è il nome del metodo `ReceiveMessage`.
* Argomenti che dell'hub viene passata al metodo. Nell'esempio seguente, il valore dell'argomento è `message`.

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

Il codice precedente in `connection.on` viene eseguito quando viene chiamato codice lato server usando il [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) (metodo).

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR determina quale metodo di client per chiamare creando una corrispondenza tra il nome del metodo e gli argomenti definiti nella `SendAsync` e `connection.on`.

> [!NOTE]
> Come procedura consigliata, chiamare il [avviare](/javascript/api/%40aspnet/signalr/hubconnection#start) metodo sulle `HubConnection` dopo `on`. In tal modo che i gestori registrati prima di tutti i messaggi vengono ricevuti.

## <a name="error-handling-and-logging"></a>La registrazione e la gestione degli errori

Catena di una `catch` alla fine del metodo di `start` metodo per gestire gli errori lato client. Usare `console.error` agli errori di output alla console del browser.

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

Analisi di log lato client installazione passando un logger e il tipo di evento per registrare quando viene stabilita la connessione. I messaggi vengono registrati con il livello di log specificato e versioni successive. Livelli di log disponibili sono i seguenti:

* `signalR.LogLevel.Error` &ndash; Messaggi di errore. I log `Error` solo i messaggi.
* `signalR.LogLevel.Warning` &ndash; Messaggi di avviso sui potenziali errori. I log `Warning`, e `Error` messaggi.
* `signalR.LogLevel.Information` &ndash; Messaggi di stato senza errori. I log `Information`, `Warning`, e `Error` messaggi.
* `signalR.LogLevel.Trace` &ndash; I messaggi di traccia. Registra tutti gli elementi, inclusi i dati trasportati tra l'hub e client.

Usare la [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) metodo sul [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) per configurare il livello di registrazione. I messaggi vengono registrati nella console del browser.

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="additional-resources"></a>Risorse aggiuntive

* [Informazioni di riferimento sulle API JavaScript](/javascript/api/?view=signalr-js-latest)
* [Hub](xref:signalr/hubs)
* [Client .NET](xref:signalr/dotnet-client)
* [Pubblicare in Azure](xref:signalr/publish-to-azure-web-app)
* [Abilitare le richieste Multiorigine (CORS) in ASP.NET Core](xref:security/cors)
