---
ms.openlocfilehash: c9fb7269969b0ef4e0300b8884c3ed168216b6cc
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446964"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="370aa-101">Dans cet exercice, vous allez créer une inscription d’application web Azure AD à l’aide Azure Active Directory centre d’administration.</span><span class="sxs-lookup"><span data-stu-id="370aa-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="370aa-102">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="370aa-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="370aa-103">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="370aa-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="370aa-104">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="370aa-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="370aa-105">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="370aa-105">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="370aa-106">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="370aa-106">Select **New registration**.</span></span> <span data-ttu-id="370aa-107">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="370aa-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="370aa-108">Définissez le **Nom** sur `Blazor Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="370aa-108">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="370aa-109">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="370aa-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="370aa-110">Sous **URI de redirection,** définissez la première drop-down sur **Application mono-page (SPA)** et définissez la valeur sur `https://localhost:5001/authentication/login-callback` .</span><span class="sxs-lookup"><span data-stu-id="370aa-110">Under **Redirect URI**, set the first drop-down to **Single-page application (SPA)** and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![Capture d’écran de la page Inscrire une application](./images/aad-register-an-app.png)

1. <span data-ttu-id="370aa-112">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="370aa-112">Select **Register**.</span></span> <span data-ttu-id="370aa-113">Dans la page Didacticiel **Graph,** copiez la valeur de l’ID de **l’application (client)** et enregistrez-la. Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="370aa-113">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](./images/aad-application-id.png)
