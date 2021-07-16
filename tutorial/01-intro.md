---
ms.openlocfilehash: 25caea9275c57faa9c741e274ac90606959422c2
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446983"
---
<!-- markdownlint-disable MD002 MD041 -->

Ce didacticiel vous apprend à créer une application WebAssembly Blazor côté client qui utilise l’API Microsoft Graph pour récupérer les informations de calendrier d’un utilisateur.

> [!TIP]
> Si vous préférez simplement télécharger le didacticiel terminé, vous pouvez télécharger ou cloner [le référentiel GitHub terminé.](https://github.com/microsoftgraph/msgraph-training-blazor-clientside) Consultez le fichier README dans le dossier **de** démonstration pour obtenir des instructions sur la configuration de l’application avec un ID d’application et une secret.

## <a name="prerequisites"></a>Conditions préalables

Avant de commencer ce didacticiel, le [SDK .NET Core](https://dotnet.microsoft.com/download) doit être installé sur votre ordinateur de développement. Si vous n’avez pas le SDK, consultez le lien précédent pour obtenir les options de téléchargement.

Vous devez également avoir un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, ou un compte scolaire ou scolaire Microsoft. Si vous n’avez pas de compte Microsoft, deux options s’offrent à vous pour obtenir un compte gratuit :

- Vous pouvez [vous inscrire à un nouveau compte Microsoft personnel.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Vous pouvez [vous inscrire au programme Office 365 développeur](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement Office 365 gratuit.

> [!NOTE]
> Ce didacticiel a été écrit avec le SDK .NET Core version 5.0.302. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais elles n’ont pas été testées.

## <a name="feedback"></a>Commentaires

Veuillez fournir des commentaires sur ce didacticiel dans [GitHub référentiel.](https://github.com/microsoftgraph/msgraph-training-blazor-clientside)
