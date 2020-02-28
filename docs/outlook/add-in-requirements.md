---
title: Conditions requises pour les compléments Outlook
description: Pour que les compléments Outlook se chargent et fonctionnent correctement, les serveurs et les clients doivent répondre à plusieurs conditions.
ms.date: 10/09/2019
localization_priority: Priority
ms.openlocfilehash: 67aebd1fae19811797c07d33a5f6cac8907550f9
ms.sourcegitcommit: a3ddfdb8a95477850148c4177e20e56a8673517c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "42166230"
---
# <a name="outlook-add-in-requirements"></a><span data-ttu-id="c7935-103">Conditions requises pour les compléments Outlook</span><span class="sxs-lookup"><span data-stu-id="c7935-103">Outlook add-in requirements</span></span>

<span data-ttu-id="c7935-104">Pour que les compléments Outlook se chargent et fonctionnent correctement, les serveurs et les clients doivent répondre à plusieurs conditions.</span><span class="sxs-lookup"><span data-stu-id="c7935-104">For Outlook add-ins to load and function properly, there are a number of requirements for both the servers and the clients.</span></span>

## <a name="client-requirements"></a><span data-ttu-id="c7935-105">Configuration requise du client</span><span class="sxs-lookup"><span data-stu-id="c7935-105">Client requirements</span></span>

- <span data-ttu-id="c7935-106">Le client doit être l’un des hôtes pris en charge pour les compléments Outlook. Les clients suivants prennent en charge les compléments :</span><span class="sxs-lookup"><span data-stu-id="c7935-106">The client must be one of the supported hosts for Outlook add-ins. The following clients support add-ins:</span></span>

   - <span data-ttu-id="c7935-107">Outlook 2013 ou version ultérieure sur Windows</span><span class="sxs-lookup"><span data-stu-id="c7935-107">Outlook 2013 or later on Windows</span></span>
   - <span data-ttu-id="c7935-108">Outlook 2016 ou version ultérieure sur Mac</span><span class="sxs-lookup"><span data-stu-id="c7935-108">Outlook 2016 or later on Mac</span></span>
   - <span data-ttu-id="c7935-109">Outlook sur iOS</span><span class="sxs-lookup"><span data-stu-id="c7935-109">Outlook on iOS</span></span>
   - <span data-ttu-id="c7935-110">Outlook sur Android</span><span class="sxs-lookup"><span data-stu-id="c7935-110">Outlook on Android</span></span>
   - <span data-ttu-id="c7935-111">Outlook sur le web pour Exchange 2016 ou une version ultérieure et Office 365</span><span class="sxs-lookup"><span data-stu-id="c7935-111">Outlook on the web for Exchange 2016 or later and Office 365</span></span>
   - <span data-ttu-id="c7935-112">Outlook sur le web pour Exchange 2013</span><span class="sxs-lookup"><span data-stu-id="c7935-112">Outlook on the web for Exchange 2013</span></span>
   - <span data-ttu-id="c7935-113">Outlook.com</span><span class="sxs-lookup"><span data-stu-id="c7935-113">Outlook.com</span></span>

- <span data-ttu-id="c7935-p101">Le client doit être connecté à un serveur Exchange ou Office 365 via une connexion directe. Lors de la configuration du client, l’utilisateur doit sélectionner un compte de type **Exchange**, **Office 365** ou **Outlook.com**. Si le client est configuré pour se connecter avec POP3 ou IMAP, les compléments ne seront pas chargés.</span><span class="sxs-lookup"><span data-stu-id="c7935-p101">The client must be connected to an Exchange server or Office 365 using a direct connection. When configuring the client, the user must choose an **Exchange**, **Office 365**, or **Outlook.com** account type. If the client is configured to connect with POP3 or IMAP, add-ins will not load.</span></span>

## <a name="mail-server-requirements"></a><span data-ttu-id="c7935-117">Configuration requise pour le serveur de messagerie</span><span class="sxs-lookup"><span data-stu-id="c7935-117">Mail server requirements</span></span>

<span data-ttu-id="c7935-p102">Si l’utilisateur est connecté à Office 365 ou à Outlook.com, le serveur de messagerie a déjà la configuration requise. En revanche, pour les utilisateurs connectés à des installations locales de Microsoft Exchange Server, les conditions suivantes s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="c7935-p102">If the user is connected to Office 365 or Outlook.com, mail server requirements are all taken care of already. However, for users connected to on-premises installations of Exchange Server, the following requirements apply.</span></span>

- <span data-ttu-id="c7935-120">Le serveur doit être un serveur Exchange 2013 ou de version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c7935-120">The server must be Exchange 2013 or later.</span></span>
- <span data-ttu-id="c7935-121">Les services web Exchange doivent être activés et exposés sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c7935-121">Exchange Web Services (EWS) must be enabled and must be exposed to the Internet.</span></span> <span data-ttu-id="c7935-122">De nombreux compléments exigent que les services web Exchange fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="c7935-122">Many add-ins require EWS to function properly.</span></span>
- <span data-ttu-id="c7935-123">Le serveur doit avoir un certificat d’authentification valide pour émettre des jetons d’identité valides.</span><span class="sxs-lookup"><span data-stu-id="c7935-123">The server must have a valid authentication certificate in order for the server to issue valid identity tokens.</span></span> <span data-ttu-id="c7935-124">Les nouvelles installations du serveur Exchange incluent un certificat d’authentification par défaut.</span><span class="sxs-lookup"><span data-stu-id="c7935-124">New installations of Exchange Server include a default authentication certificate.</span></span> <span data-ttu-id="c7935-125">Pour plus d’informations, reportez-vous aux articles [Certificats numériques et chiffrement dans Exchange 2016](/Exchange/architecture/client-access/certificates) et [Set-AuthConfig](/powershell/module/exchange/organization/Set-AuthConfig).</span><span class="sxs-lookup"><span data-stu-id="c7935-125">For more information, see [Digital certificates and encryption in Exchange 2016](/Exchange/architecture/client-access/certificates) and [Set-AuthConfig](/powershell/module/exchange/organization/Set-AuthConfig).</span></span>
- <span data-ttu-id="c7935-126">Pour accéder à des compléments à partir d’[AppSource](https://appsource.microsoft.com/marketplace/apps?product=office&page=1&src=office&corrid=a35323d5-0e3d-4cc0-ba44-57537d74aae8&omexanonuid=581941df-1c6f-4eda-89e7-651af8aeaeb2), les serveurs d’accès au client doivent être en mesure de communiquer avec AppSource.</span><span class="sxs-lookup"><span data-stu-id="c7935-126">To access add-ins from [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office&page=1&src=office&corrid=a35323d5-0e3d-4cc0-ba44-57537d74aae8&omexanonuid=581941df-1c6f-4eda-89e7-651af8aeaeb2), the client access servers must be able to communicate with AppSource.</span></span>

## <a name="add-in-server-requirements"></a><span data-ttu-id="c7935-127">Conditions de serveur pour le complément</span><span class="sxs-lookup"><span data-stu-id="c7935-127">Add-in server requirements</span></span>

<span data-ttu-id="c7935-p105">Les fichiers du complément (HTML, JavaScript, etc.) peuvent être hébergés sur n’importe quelle plateforme de serveur web. Les seules conditions sont que le serveur doit être configuré de manière à utiliser le protocole HTTPS et que le certificat SSL doit être approuvé par le client.</span><span class="sxs-lookup"><span data-stu-id="c7935-p105">Add-in files (HTML, JavaScript, etc.) can be hosted on any web server platform desired. The only requirement is that the server must be configured to use HTTPS, and the SSL certificate must be trusted by the client.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7935-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c7935-130">See also</span></span>

- [<span data-ttu-id="c7935-131">Configuration requise pour exécuter des compléments Office</span><span class="sxs-lookup"><span data-stu-id="c7935-131">Requirements for running Office Add-ins</span></span>](../concepts/requirements-for-running-office-add-ins.md)
- [<span data-ttu-id="c7935-132">Disponibilité des compléments Office sur les plateformes et les hôtes (section Outlook)</span><span class="sxs-lookup"><span data-stu-id="c7935-132">Office Add-in host and platform availability (Outlook section)</span></span>](../overview/office-add-in-availability.md#outlook)
- [<span data-ttu-id="c7935-133">Prise en charge des ensembles de conditions requises de l’API JavaScript pour Outlook</span><span class="sxs-lookup"><span data-stu-id="c7935-133">Outlook JavaScript API requirement set support</span></span>](../reference/requirement-sets/outlook-api-requirement-sets.md#requirement-sets-supported-by-exchange-servers-and-outlook-clients)