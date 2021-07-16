---
ms.openlocfilehash: 4c021fe8aac9b42ee0984a15e73366ead847ee06
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446976"
---
<!-- markdownlint-disable MD002 MD041 -->

Commencez par créer une application WebAssembly Blazor.

1. Ouvrez votre interface de ligne de commande (CLI) dans un répertoire où vous souhaitez créer le projet. Exécutez la commande suivante :

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    Ce `--auth SingleOrg` paramètre entraîne l’inclut dans le projet généré la configuration de l’authentification avec le Plateforme d’identités Microsoft.

1. Une fois le projet créé, vérifiez qu’il fonctionne en modifiant le répertoire actuel en répertoire **GraphTutorial** et en exécutant la commande suivante dans votre CLI.

    ```Shell
    dotnet watch run
    ```

1. Ouvrez votre navigateur et accédez à `https://localhost:5001` . Si tout fonctionne, vous devriez voir un « Hello, world! » Message.

> [!IMPORTANT]
> Si vous recevez un avertissement signalant que le certificat pour **localhost** n’est pas approuvé, vous pouvez utiliser l’CLI .NET Core pour installer et faire confiance au certificat de développement. Voir [Appliquer HTTPS dans ASP.NET Core](/aspnet/core/security/enforcing-ssl) pour obtenir des instructions pour des systèmes d’exploitation spécifiques.

## <a name="add-nuget-packages"></a>Ajouter des packages NuGet

Avant de passer à la suite, installez des packages NuGet supplémentaires que vous utiliserez ultérieurement.

- [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) pour effectuer des appels Microsoft Graph.
- [TimeZoneConverter pour](https://github.com/mj1856/TimeZoneConverter) la traduction Windows identificateurs de fuseau horaire en identificateurs IANA.

1. Exécutez les commandes suivantes dans votre CLI pour installer les dépendances.

    ```Shell
    dotnet add package Microsoft.Graph --version 4.0.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>Concevoir l’application

Dans cette section, vous allez créer la structure d’interface utilisateur de base de l’application.

1. Supprimez les exemples de pages générés par le modèle. Supprimez les fichiers suivants.

    - **./Pages/Counter.sous**
    - **./Pages/FetchData.sous**
    - **./Shared/SurveyPrompt.sous**
    - **./wwwroot/sample-data/weather.json**

1. Ouvrez **./wwwroot/index.html** et ajoutez le code suivant juste **avant** la balise `</body>` de fermeture.

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    Cela ajoute les fichiers JavaScript [Bootstrap.](https://getbootstrap.com/docs/4.5/getting-started/introduction/)

1. Ouvrez **./wwwroot/css/app.css** et ajoutez le code suivant.

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. Ouvrez **./Shared/NavMenu.en-us et** remplacez son contenu par ce qui suit.

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. Ouvrez **./Pages/Index.tsx** et remplacez son contenu par ce qui suit.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. Ouvrez **./Shared/LoginDisplay.login** et remplacez son contenu par ce qui suit.

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

1. Créez un répertoire dans **le répertoire ./wwwroot** nommé **img**. Ajoutez un fichier image de votre choix nommé **no-profile-photo.png** dans ce répertoire. Cette image est utilisée comme photo de l’utilisateur lorsque l’utilisateur n’a pas de photo dans Microsoft Graph.

    > [!TIP]
    > Vous pouvez télécharger l’image utilisée dans ces captures d’écran [à partir GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).

1. Enregistrez toutes vos modifications et actualisez la page.

    ![Capture d’écran de la page d’accueil repensée](./images/create-app-01.png)
