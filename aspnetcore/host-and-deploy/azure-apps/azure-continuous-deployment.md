---
title: Distribuzione continua in Azure con Visual Studio e Git con ASP.NET Core
author: rick-anderson
description: Informazioni su come creare un'app Web ASP.NET Core tramite Visual Studio e distribuirla nel Servizio app di Azure usando Git per la distribuzione continua.
ms.author: riande
ms.custom: mvc
ms.date: 12/06/2018
uid: host-and-deploy/azure-apps/azure-continuous-deployment
ms.openlocfilehash: e12c2ee0b78db105b431770e8644e7d19d915765
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284433"
---
# <a name="continuous-deployment-to-azure-with-visual-studio-and-git-with-aspnet-core"></a>Distribuzione continua in Azure con Visual Studio e Git con ASP.NET Core

Di [Erik Reitan](https://github.com/Erikre)

[!INCLUDE [Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

Questa esercitazione mostra come creare un'app Web ASP.NET Core tramite Visual Studio e distribuirla da Visual Studio nel Servizio app di Azure, usando Git la distribuzione continua.

Vedere anche l'articolo [Creare la prima pipeline con Azure Pipelines](/azure/devops/pipelines/get-started-yaml), che illustra come configurare un flusso di lavoro di recapito continuo per il [Servizio app di Azure](/azure/app-service/app-service-web-overview) usando Azure DevOps Services. Azure Pipelines (un servizio di Azure DevOps Services) semplifica la configurazione di una pipeline di distribuzione solida per pubblicare gli aggiornamenti per le app ospitate nel Servizio app di Azure. È possibile configurare la pipeline dal portale di Azure per compilare, eseguire i test, distribuire in uno slot di staging e quindi distribuire nell'ambiente di produzione.

> [!NOTE]
> Per completare questa esercitazione, è necessario un account di Microsoft Azure. Per ottenere un account, [attivare i benefici per il sottoscrittore MSDN](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) o [iscriversi per una versione di valutazione gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Prerequisiti

In questa esercitazione si presuppone che sia stato installato il software seguente:

* [Visual Studio](https://www.visualstudio.com)
* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* [Git](https://git-scm.com/downloads) per Windows

## <a name="create-an-aspnet-core-web-app"></a>Creare un'app Web ASP.NET Core

1. Avviare Visual Studio.

1. Scegliere **Nuovo** > **Progetto** dal menu **File**.

1. Selezionare il modello di progetto **Applicazione Web ASP.NET Core**. Viene visualizzato in **Modelli** > **installati** > **Visual C#** > **.NET Core**. Denominare il progetto `SampleWebAppDemo`. Selezionare l'opzione **Crea nuovo repository Git** e fare clic su **OK**.

   ![Finestra di dialogo Nuovo progetto](azure-continuous-deployment/_static/01-new-project.png)

1. Nella finestra di dialogo **Nuovo progetto ASP.NET Core** selezionare il modello ASP.NET Core **Vuoto** e quindi fare clic su **OK**.

   ![Finestra di dialogo Nuovo progetto ASP.NET Core](azure-continuous-deployment/_static/02-web-site-template.png)

> [!NOTE]
> La versione più recente di .NET Core è la 2.0.

### <a name="running-the-web-app-locally"></a>Esecuzione dell'applicazione Web in locale

1. Una volta terminata la creazione dell'app da parte di Visual Studio, eseguire l'app selezionando **Debug** > **Avvia l'esecuzione del debug**. In alternativa, premere **F5**.

   L'inizializzazione di Visual Studio e della nuova app potrebbe richiedere tempo. Una volta completata, il browser visualizzerà l'app in esecuzione.

   ![La finestra del browser mostra l'applicazione in esecuzione che visualizza "Hello World!"](azure-continuous-deployment/_static/04-browser-runapp.png)

1. Dopo aver revisionato l'app Web in esecuzione, chiudere il browser e selezionare l'icona "Interrompi l'esecuzione del debug" nella barra degli strumenti di Visual Studio per arrestare l'app.

## <a name="create-a-web-app-in-the-azure-portal"></a>Creare un'app web nel portale di Azure

Eseguire i passaggi seguenti per creare un'app Web nel portale di Azure:

1. Accedere al [portale di Azure](https://portal.azure.com).

1. Selezionare **NUOVO** nella parte superiore sinistra dell'interfaccia del portale.

1. Selezionare **Web e dispositivi mobili** > **App Web**.

   ![Portale di Microsoft Azure: Pulsante Nuovo: Web e dispositivi mobili in Marketplace: Pulsante App Web in App in primo piano](azure-continuous-deployment/_static/05-azure-newwebapp.png)

1. Nel pannello **App Web** immettere un valore univoco per il **Nome del servizio App**.

   ![Pannello App Web](azure-continuous-deployment/_static/06-azure-newappblade.png)

   > [!NOTE]
   > Il nome **Nome del servizio app** deve essere univoco. Il portale applica questa regola quando viene specificato il nome. Se si specifica un valore diverso, sostituire tale valore per ogni occorrenza di **SampleWebAppDemo** in questa esercitazione.

   Anche nel pannello **App Web**, selezionare una **Posizione/piano di servizio App** o crearne uno nuovo. Se si crea un nuovo piano, selezionare il piano tariffario, la posizione e altre opzioni. Per altre informazioni sui piani di Servizio app, vedere [Panoramica di approfondimento dei piani del Servizio App di Azure](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).

1. Scegliere **Crea**. Azure eseguirà il provisioning e avvierà l'app Web.

   ![Portale di Azure: pannello Essentials di Sample Web App Demo 01](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a>Abilitare la pubblicazione di Git per la nuova app web

Git è un sistema di controllo della versione distribuito che è possibile usare per distribuire un'app Web di Servizio app di Azure. Il codice dell'app Web è archiviato in un repository Git locale e viene distribuito in Azure eseguendone il push in un repository remoto.

1. Accedere al [portale di Azure](https://portal.azure.com).

1. Selezionare **Servizi app** per visualizzare un elenco dei servizi app associati alla sottoscrizione di Azure.

1. Selezionare l'app Web che è stata creata nella sezione precedente di questa esercitazione.

1. Nel pannello **Distribuzione** selezionare **Opzioni di distribuzione** > **Scegli origine** > **Repository Git locale**.

   ![Pannello Impostazioni: pannello Origine distribuzione: pannello Scegli origine](azure-continuous-deployment/_static/deployment-options.png)

1. Scegliere **OK**.

1. Se le credenziali di distribuzione per la pubblicazione di un'app Web o di altri servizi app Web non sono state precedentemente configurate, impostarle ora:

   * Selezionare **Impostazioni** > **Credenziali per la distribuzione**. Verrà visualizzato il pannello **Imposta credenziali di distribuzione**.
   * Creare un nome utente e una password. Salvare la password per un uso successivo durante la configurazione di Git.
   * Selezionare **Salva**.

1. Nel pannello **App Web** selezionare **Impostazioni** > **Proprietà**. L'URL del repository Git remoto che verrà distribuito è visualizzato in **URL GIT**.

1. Copiare il valore **URL GIT** per un uso successivo nell'esercitazione.

   ![Portale di Azure: pannello Proprietà dell'applicazione](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-the-web-app-to-azure-app-service"></a>Pubblicare l'app Web nel servizio app di Azure

In questa sezione si creerà un repository Git locale tramite Visual Studio e si eseguirà il push da tale repository in Azure per distribuire l'app Web. La procedura coinvolta include quanto segue:

* Aggiungere l'impostazione del repository remoto tramite il valore di URL GIT, in modo da poter distribuire il repository locale in Azure.
* Eseguire il commit delle modifiche del progetto.
* Effettuare il push delle modifiche di progetto dal repository locale al repository remoto in Azure.

1. In **Esplora soluzioni** fare clic con il tasto destro del mouse su **Soluzione "SampleWebAppDemo"** e selezionare **Commit**. Verrà visualizzato **Team Explorer**.

   ![Scheda di connessione Team Explorer](azure-continuous-deployment/_static/10-team-explorer.png)

1. In **Team Explorer** selezionare la **Home** (icona home) > **Impostazioni** > **Impostazioni del Repository**.

1. Nella sezione **Elementi remoti** di **Impostazioni repository** selezionare **Aggiungi**. Verrà visualizzata la finestra di dialogo **Aggiungi elemento remoto**.

1. Impostare il **Nome** del repository remoto da **Azure SampleApp**.

1. Impostare il valore per **Recupero** sull'**URL Git** precedentemente copiato da Azure in questa esercitazione. Si noti che questo è l'URL che termina con **.git**.

   ![Modifica finestra di dialogo remota](azure-continuous-deployment/_static/11-add-remote.png)

   > [!NOTE]
   > In alternativa, specificare il repository remoto dalla **Finestra di comando** aprendo la **Finestra di comando**, passando alla directory del progetto e immettendo il comando. Esempio:
   >
   > `git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`

1. Selezionare la **Home** (icona home) > **Impostazioni** > **Impostazioni globali**. Verificare che il nome e l'indirizzo e-mail siano impostati. Selezionare **Aggiorna**, se necessario.

1. Selezionare **Home** > **Modifiche** da restituire alla vista **Modifiche**.

1. Immettere un messaggio di commit, ad esempio **Push iniziale #1** e selezionare **Commit**. Questa azione consente di creare un *commit* a livello locale.

   ![Scheda di connessione Team Explorer](azure-continuous-deployment/_static/12-initial-commit.png)

   > [!NOTE]
   > In alternativa, eseguire il commit delle modifiche dalla **Finestra di comando** aprendo la **Finestra di comando**, passando alla directory del progetto e immettendo i comandi Git. Esempio:
   >
   > `git add .`
   >
   > `git commit -am "Initial Push #1"`

1. Selezionare **Home** > **Sincronizzazione** > **Azioni** > **Aprire il prompt dei comandi**. Verrà aperto il prompt dei comandi nella directory del progetto.

1. Immettere il comando seguente nella finestra Comando:

   `git push -u Azure-SampleApp master`

1. Immettere la password delle **credenziali di distribuzione** di Azure creata precedentemente in Azure.

   Questo comando avvia il processo di esecuzione del push dei file di progetto locali in Azure. L'output del comando precedente termina con un messaggio che indica che la distribuzione ha avuto esito positivo.

   ```
   remote: Finished successfully.
   remote: Running post deployment command(s)...
   remote: Deployment successful.
   To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
   * [new branch]      master -> master
   Branch master set up to track remote branch master from Azure-SampleApp.
   ```

   > [!NOTE]
   > Se è necessaria la collaborazione sul progetto, valutare se eseguire il push in [GitHub](https://github.com) prima del push in Azure.
 
### <a name="verify-the-active-deployment"></a>Verificare la distribuzione attiva

Verificare che il trasferimento dell'app Web dall'ambiente locale in Azure abbia esito positivo.

Nel [portale di Azure](https://portal.azure.com) selezionare l'app Web. Selezionare **Distribuzione** > **Opzioni di distribuzione**.

![Portale di Azure: Pannello Impostazioni: pannello di distribuzione che visualizza la distribuzione completata](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a>Eseguire l'app in Azure

Ora che l'app Web è distribuita in Azure, eseguire l'app.

Questa operazione può essere eseguita in due modi:

* Nel portale di Azure individuare il pannello dell'app Web per l'app Web. Selezionare **Sfoglia** per visualizzare l'app nel browser predefinito.
* Aprire un browser e immettere l'URL per l'app Web. Esempio: `http://SampleWebAppDemo.azurewebsites.net`

## <a name="update-the-web-app-and-republish"></a>Aggiornare l'app Web e ripetere la pubblicazione

Dopo aver apportato modifiche al codice locale, ripetere la pubblicazione:

1. In **Esplora soluzioni** di Visual Studio aprire il file *Startup.cs*.

1. Nel metodo `Configure` modificare il metodo `Response.WriteAsync` in modo che venga visualizzato nel seguente modo:

   ```csharp
   await context.Response.WriteAsync("Hello World! Deploy to Azure.");
   ```

1. Salvare le modifiche a *Startup.cs*.

1. In **Esplora soluzioni** fare clic con il tasto destro del mouse su **Soluzione "SampleWebAppDemo"** e selezionare **Commit**. Verrà visualizzato **Team Explorer**.

1. Immettere un messaggio per il commit, ad esempio `Update #2`.

1. Premere il pulsante **Commit** per salvare le modifiche del progetto.

1. Selezionare **Home** > **Sincronizzazione** > **Azioni** > **Push**.

> [!NOTE]
> In alternativa, eseguire il push delle modifiche dalla **Finestra di comando** aprendo la **Finestra di comando**, passando alla directory del progetto e immettendo un comando Git. Esempio:
> 
> `git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a>Visualizzare l'app web aggiornata in Azure

Visualizzare l'app Web aggiornata selezionando **Sfoglia** dal pannello dell'app Web nel portale di Azure o aprendo un browser e immettendo l'URL per l'app Web. Esempio: `http://SampleWebAppDemo.azurewebsites.net`

## <a name="additional-resources"></a>Risorse aggiuntive

* [Creare la prima pipeline con Azure Pipelines](/azure/devops/pipelines/get-started-yaml)
* [Kudu del progetto](https://github.com/projectkudu/kudu/wiki)
* <xref:host-and-deploy/visual-studio-publish-profiles>
