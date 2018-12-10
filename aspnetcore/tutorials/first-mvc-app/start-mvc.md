---
title: Introduzione ad ASP.NET Core MVC e Visual Studio
author: rick-anderson
description: Informazioni introduttive su ASP.NET Core MVC e Visual Studio.
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 738c49272c2ae2b075866001f06ad09fe73969f9
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862200"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a>Introduzione ad ASP.NET Core MVC e Visual Studio

Di [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

Sono disponibili 3 versioni dell'esercitazione:

* macOS: [Creare un'app ASP.NET Core MVC con Visual Studio per Mac](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows: [Creare un'app ASP.NET Core MVC con Visual Studio](xref:tutorials/first-mvc-app/start-mvc)
* macOS, Linux e Windows: [Creare un'app ASP.NET Core MVC con Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)

> [!NOTE]
> È in corso un test di usabilità di una nuova proposta di struttura del sommario di ASP.NET Core.  Se si dispone di alcuni minuti per provare a cercare 7 argomenti diversi nel sommario corrente o proposto, [fare clic qui per partecipare al test](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).

## <a name="install-visual-studio-and-net-core"></a>Installare Visual Studio e .NET Core

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-web-app"></a>Creare un'app Web

In Visual Studio selezionare **File > Nuovo > Progetto**.

![File > Nuovo > Progetto](start-mvc/_static/alt_new_project.png)

Completare la finestra di dialogo **Nuovo progetto**:

* Nel riquadro a sinistra toccare **.NET Core**
* Nel riquadro al centro toccare **Applicazione Web ASP.NET Core (.NET Core)**
* Denominare il progetto "MvcMovie" (è importante denominare il progetto "MvcMovie" in modo che quando si copia il codice lo spazio dei nomi corrisponda).
* Toccare **OK**.

![Finestra di dialogo Nuovo progetto, .NET nel riquadro sinistro, Web ASP.NET Core ](start-mvc/_static/new_project2-21.png)

Completare la finestra di dialogo **Nuova Applicazione Web ASP.NET Core (.NET Core) - MvcMovie**:

* Nella casella di riepilogo a discesa del selettore di versione selezionare **ASP.NET Core 2.1**
* Selezionare **Applicazione Web (Model-View-Controller)**
* Toccare **OK**.

![Finestra di dialogo Nuovo progetto, .NET nel riquadro sinistro, Web ASP.NET Core ](start-mvc/_static/new_project22-21.png)

Visual Studio ha usato un modello predefinito per il progetto MVC appena creato. Ora è possibile disporre di un'app funzionante immettendo un nome progetto e selezionando alcune opzioni. Si tratta di un progetto iniziale di base che rappresenta un ottimo punto di partenza.

Toccare **F5** per eseguire l'app in modalità di debug o **CTRL+F5** per eseguirla in modalità non di debug.
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![app in esecuzione](start-mvc/_static/1.png)

* Visual Studio avvia [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) ed esegue l'app. Si noti che la barra degli indirizzi visualizza `localhost:port#` e non `example.com` o simili. Ciò accade perché `localhost` è il nome host standard per il computer locale. Quando Visual Studio crea un progetto Web, per il server Web viene usata una porta casuale. Nell'immagine precedente il numero di porta è 5000. Nell'URL nel browser viene visualizzato `localhost:5000`. Quando si esegue l'app verrà visualizzato un numero di porta diverso.
* Se si avvia l'app con **CTRL+F5** (modalità non di debug) sarà possibile apportare modifiche al codice, salvare il file, aggiornare il browser e visualizzare le modifiche del codice. Molti sviluppatori preferiscono usare la modalità non di debug per avviare l'app rapidamente e visualizzare le modifiche.
* È possibile scegliere se avviare l'app in modalità di debug o non di debug nella voce di menu **Debug**:

![Menu Debug](start-mvc/_static/debug_menu.png)

* È possibile eseguire il debug dell'app toccando il pulsante **IIS Express**.

![IIS Express](start-mvc/_static/iis_express.png)

Il modello predefinito include collegamenti **Home page, Informazioni su** e **Contatto**. L'immagine del browser visualizzata sopra non mostra questi collegamenti. A seconda delle dimensioni del browser, può essere necessario fare clic sull'icona di spostamento per visualizzarli.

![Icona di spostamento in alto a destra](start-mvc/_static/2.png)

Se l'esecuzione è in modalità di debug, toccare **MAIUSC+F5** per arrestare il debug.

Nella parte seguente di questa esercitazione vengono fornite informazioni su MVC e istruzioni per iniziare a creare codice.

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-web-app"></a>Creare un'app Web

In Visual Studio selezionare **File > Nuovo > Progetto**.

![File > Nuovo > Progetto](start-mvc/_static/alt_new_project.png)

Completare la finestra di dialogo **Nuovo progetto**:

* Nel riquadro a sinistra toccare **.NET Core**
* Nel riquadro al centro toccare **Applicazione Web ASP.NET Core (.NET Core)**
* Denominare il progetto "MvcMovie" (è importante denominare il progetto "MvcMovie" in modo che quando si copia il codice lo spazio dei nomi corrisponda).
* Toccare **OK**.

![Finestra di dialogo Nuovo progetto, .NET nel riquadro sinistro, Web ASP.NET Core ](start-mvc/_static/new_project2.png)

Completare la finestra di dialogo **Nuova Applicazione Web ASP.NET Core (.NET Core) - MvcMovie**:

* Nella casella di riepilogo a discesa del selettore di versione selezionare **ASP.NET Core 2.-**
* Selezionare **Web Application (Model-View-Controller)** (Applicazione Web (Model-View-Controller)).
* Toccare **OK**.

![Finestra di dialogo Nuovo progetto, .NET nel riquadro sinistro, Web ASP.NET Core ](start-mvc/_static/new_project22.png)

Visual Studio ha usato un modello predefinito per il progetto MVC appena creato. Ora è possibile disporre di un'app funzionante immettendo un nome progetto e selezionando alcune opzioni. Si tratta di un progetto iniziale di base che rappresenta un ottimo punto di partenza.

Toccare **F5** per eseguire l'app in modalità di debug o **CTRL+F5** per eseguirla in modalità non di debug.
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![app in esecuzione](start-mvc/_static/1.png)

* Visual Studio avvia [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) ed esegue l'app. Si noti che la barra degli indirizzi visualizza `localhost:port#` e non `example.com` o simili. Ciò accade perché `localhost` è il nome host standard per il computer locale. Quando Visual Studio crea un progetto Web, per il server Web viene usata una porta casuale. Nell'immagine precedente il numero di porta è 5000. Nell'URL nel browser viene visualizzato `localhost:5000`. Quando si esegue l'app verrà visualizzato un numero di porta diverso.
* Se si avvia l'app con **CTRL+F5** (modalità non di debug) sarà possibile apportare modifiche al codice, salvare il file, aggiornare il browser e visualizzare le modifiche del codice. Molti sviluppatori preferiscono usare la modalità non di debug per avviare l'app rapidamente e visualizzare le modifiche.
* È possibile scegliere se avviare l'app in modalità di debug o non di debug nella voce di menu **Debug**:

![Menu Debug](start-mvc/_static/debug_menu.png)

* È possibile eseguire il debug dell'app toccando il pulsante **IIS Express**.

![IIS Express](start-mvc/_static/iis_express.png)

Il modello predefinito include collegamenti **Home page, Informazioni su** e **Contatto**. L'immagine del browser visualizzata sopra non mostra questi collegamenti. A seconda delle dimensioni del browser, può essere necessario fare clic sull'icona di spostamento per visualizzarli.

![Icona di spostamento in alto a destra](start-mvc/_static/2.png)

Se l'esecuzione è in modalità di debug, toccare **MAIUSC+F5** per arrestare il debug.

Nella parte seguente di questa esercitazione vengono fornite informazioni su MVC e istruzioni per iniziare a creare codice.

::: moniker-end

> [!div class="step-by-step"]
> [avanti](adding-controller.md)  
