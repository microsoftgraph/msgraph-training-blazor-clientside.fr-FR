---
ms.openlocfilehash: 4c021fe8aac9b42ee0984a15e73366ead847ee06
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446976"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="36519-101">Commencez par créer une application WebAssembly Blazor.</span><span class="sxs-lookup"><span data-stu-id="36519-101">Start by creating a Blazor WebAssembly app.</span></span>

1. <span data-ttu-id="36519-102">Ouvrez votre interface de ligne de commande (CLI) dans un répertoire où vous souhaitez créer le projet.</span><span class="sxs-lookup"><span data-stu-id="36519-102">Open your command-line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="36519-103">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="36519-103">Run the following command.</span></span>

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    <span data-ttu-id="36519-104">Ce `--auth SingleOrg` paramètre entraîne l’inclut dans le projet généré la configuration de l’authentification avec le Plateforme d’identités Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36519-104">The `--auth SingleOrg` parameter causes the generated project to include configuration for authentication with the Microsoft identity platform.</span></span>

1. <span data-ttu-id="36519-105">Une fois le projet créé, vérifiez qu’il fonctionne en modifiant le répertoire actuel en répertoire **GraphTutorial** et en exécutant la commande suivante dans votre CLI.</span><span class="sxs-lookup"><span data-stu-id="36519-105">Once the project is created, verify that it works by changing the current directory to the **GraphTutorial** directory and running the following command in your CLI.</span></span>

    ```Shell
    dotnet watch run
    ```

1. <span data-ttu-id="36519-106">Ouvrez votre navigateur et accédez à `https://localhost:5001` .</span><span class="sxs-lookup"><span data-stu-id="36519-106">Open your browser and browse to `https://localhost:5001`.</span></span> <span data-ttu-id="36519-107">Si tout fonctionne, vous devriez voir un « Hello, world! »</span><span class="sxs-lookup"><span data-stu-id="36519-107">If everything is working, you should see a "Hello, world!"</span></span> <span data-ttu-id="36519-108">Message.</span><span class="sxs-lookup"><span data-stu-id="36519-108">message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36519-109">Si vous recevez un avertissement signalant que le certificat pour **localhost** n’est pas approuvé, vous pouvez utiliser l’CLI .NET Core pour installer et faire confiance au certificat de développement.</span><span class="sxs-lookup"><span data-stu-id="36519-109">If you receive a warning that the certificate for **localhost** is un-trusted you can use the .NET Core CLI to install and trust the development certificate.</span></span> <span data-ttu-id="36519-110">Voir [Appliquer HTTPS dans ASP.NET Core](/aspnet/core/security/enforcing-ssl) pour obtenir des instructions pour des systèmes d’exploitation spécifiques.</span><span class="sxs-lookup"><span data-stu-id="36519-110">See [Enforce HTTPS in ASP.NET Core](/aspnet/core/security/enforcing-ssl) for instructions for specific operating systems.</span></span>

## <a name="add-nuget-packages"></a><span data-ttu-id="36519-111">Ajouter des packages NuGet</span><span class="sxs-lookup"><span data-stu-id="36519-111">Add NuGet packages</span></span>

<span data-ttu-id="36519-112">Avant de passer à la suite, installez des packages NuGet supplémentaires que vous utiliserez ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="36519-112">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="36519-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) pour effectuer des appels Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36519-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to Microsoft Graph.</span></span>
- <span data-ttu-id="36519-114">[TimeZoneConverter pour](https://github.com/mj1856/TimeZoneConverter) la traduction Windows identificateurs de fuseau horaire en identificateurs IANA.</span><span class="sxs-lookup"><span data-stu-id="36519-114">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) for translating Windows time zone identifiers to IANA identifiers.</span></span>

1. <span data-ttu-id="36519-115">Exécutez les commandes suivantes dans votre CLI pour installer les dépendances.</span><span class="sxs-lookup"><span data-stu-id="36519-115">Run the following commands in your CLI to install the dependencies.</span></span>

    ```Shell
    dotnet add package Microsoft.Graph --version 4.0.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a><span data-ttu-id="36519-116">Concevoir l’application</span><span class="sxs-lookup"><span data-stu-id="36519-116">Design the app</span></span>

<span data-ttu-id="36519-117">Dans cette section, vous allez créer la structure d’interface utilisateur de base de l’application.</span><span class="sxs-lookup"><span data-stu-id="36519-117">In this section you will create the basic UI structure of the application.</span></span>

1. <span data-ttu-id="36519-118">Supprimez les exemples de pages générés par le modèle.</span><span class="sxs-lookup"><span data-stu-id="36519-118">Remove sample pages generated by the template.</span></span> <span data-ttu-id="36519-119">Supprimez les fichiers suivants.</span><span class="sxs-lookup"><span data-stu-id="36519-119">Delete the following files.</span></span>

    - <span data-ttu-id="36519-120">**./Pages/Counter.sous**</span><span class="sxs-lookup"><span data-stu-id="36519-120">**./Pages/Counter.razor**</span></span>
    - <span data-ttu-id="36519-121">**./Pages/FetchData.sous**</span><span class="sxs-lookup"><span data-stu-id="36519-121">**./Pages/FetchData.razor**</span></span>
    - <span data-ttu-id="36519-122">**./Shared/SurveyPrompt.sous**</span><span class="sxs-lookup"><span data-stu-id="36519-122">**./Shared/SurveyPrompt.razor**</span></span>
    - <span data-ttu-id="36519-123">**./wwwroot/sample-data/weather.json**</span><span class="sxs-lookup"><span data-stu-id="36519-123">**./wwwroot/sample-data/weather.json**</span></span>

1. <span data-ttu-id="36519-124">Ouvrez **./wwwroot/index.html** et ajoutez le code suivant juste **avant** la balise `</body>` de fermeture.</span><span class="sxs-lookup"><span data-stu-id="36519-124">Open **./wwwroot/index.html** and add the following code just **before** the closing `</body>` tag.</span></span>

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    <span data-ttu-id="36519-125">Cela ajoute les fichiers JavaScript [Bootstrap.](https://getbootstrap.com/docs/4.5/getting-started/introduction/)</span><span class="sxs-lookup"><span data-stu-id="36519-125">This adds the [Bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/) javascript files.</span></span>

1. <span data-ttu-id="36519-126">Ouvrez **./wwwroot/css/app.css** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="36519-126">Open **./wwwroot/css/app.css** and add the following code.</span></span>

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. <span data-ttu-id="36519-127">Ouvrez **./Shared/NavMenu.en-us et** remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="36519-127">Open **./Shared/NavMenu.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. <span data-ttu-id="36519-128">Ouvrez **./Pages/Index.tsx** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="36519-128">Open **./Pages/Index.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. <span data-ttu-id="36519-129">Ouvrez **./Shared/LoginDisplay.login** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="36519-129">Open **./Shared/LoginDisplay.razor** and replace its contents with the following.</span></span>

    ```razor
    @using Microsoft.AspNetCore.Components.Authorization
    @using Microsoft.AspNetCore.Components.WebAssembly.Authentication

    @inject NavigationManager Navigation
    @inject SignOutSessionStateManager SignOutManager

    <AuthorizeView>
        <Authorized>
            <a class="text-decoration-none" data-toggle="dropdown" href="#" role="button">
                <img src="/img/no-profile-photo.png" class="nav-profile-photo rounded-circle align-self-center mr-2">
            </a>
            <div class="dropdown-menu dropdown-menu-right">
                <h5 class="dropdown-item-text mb-0">@context.User.Identity.Name</h5>
                <p class="dropdown-item-text text-muted mb-0">placeholder@contoso.com</p>
                <div class="dropdown-divider"></div>
                <button class="dropdown-item" @onclick="BeginLogout">Log out</button>
            </div>
        </Authorized>
        <NotAuthorized>
            <a href="authentication/login">Log in</a>
        </NotAuthorized>
    </AuthorizeView>

    @code{
        private async Task BeginLogout(MouseEventArgs args)
        {
            await SignOutManager.SetSignOutState();
            Navigation.NavigateTo("authentication/logout");
        }
    }
    ```

1. <span data-ttu-id="36519-130">Créez un répertoire dans **le répertoire ./wwwroot** nommé **img**.</span><span class="sxs-lookup"><span data-stu-id="36519-130">Create a new directory in the **./wwwroot** directory named **img**.</span></span> <span data-ttu-id="36519-131">Ajoutez un fichier image de votre choix nommé **no-profile-photo.png** dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="36519-131">Add an image file of your choosing named **no-profile-photo.png** in this directory.</span></span> <span data-ttu-id="36519-132">Cette image est utilisée comme photo de l’utilisateur lorsque l’utilisateur n’a pas de photo dans Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36519-132">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

    > [!TIP]
    > <span data-ttu-id="36519-133">Vous pouvez télécharger l’image utilisée dans ces captures d’écran [à partir GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span><span class="sxs-lookup"><span data-stu-id="36519-133">You can download the image used in these screenshots from [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span></span>

1. <span data-ttu-id="36519-134">Enregistrez toutes vos modifications et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="36519-134">Save all of your changes and refresh the page.</span></span>

    ![Capture d’écran de la page d’accueil repensée](./images/create-app-01.png)
