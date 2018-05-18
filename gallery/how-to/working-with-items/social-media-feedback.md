---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: Отправка отзывов через социальные сети или комментарии
ms.openlocfilehash: 79f1450337b9ed5bb0687494fe1ed7c2d87f1bb5
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="providing-feedback-via-social-media-or-comments"></a><span data-ttu-id="0f55c-103">Отправка отзывов через социальные сети или комментарии</span><span class="sxs-lookup"><span data-stu-id="0f55c-103">Providing Feedback via social media or comments</span></span>

<span data-ttu-id="0f55c-104">Коллекция Powershell предоставляет пользователям два способа отправки общедоступных отзывов по элементу:</span><span class="sxs-lookup"><span data-stu-id="0f55c-104">The Powershell Gallery supports two approaches for users to provide public feedback on an item:</span></span>

- <span data-ttu-id="0f55c-105">Ссылки слева на странице, чтобы поделиться элементом в социальных сетях Facebook, LinkedIn и Twitter.</span><span class="sxs-lookup"><span data-stu-id="0f55c-105">Use the links on the left edge to "share" an item in Facebook, LinkedIn, or Twitter social media sites;</span></span>
- <span data-ttu-id="0f55c-106">Функция комментариев, чтобы опубликовать комментарии к элементу и сделать их доступными для авторов опубликованных компонентов.</span><span class="sxs-lookup"><span data-stu-id="0f55c-106">Use the Comment feature to post comments on an item, and to allow Authors to watch for comments on items they publish.</span></span>

## <a name="social-media-feedback"></a><span data-ttu-id="0f55c-107">Отзывы в социальных сетях</span><span class="sxs-lookup"><span data-stu-id="0f55c-107">Social Media Feedback</span></span>

<span data-ttu-id="0f55c-108">На каждый элемент в коллекции PowerShell есть ссылки для Facebook, LinkedIn и Twitter в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="0f55c-108">On the left side of the page for each item in the PowerShell Gallery there are links for Facebook, LinkedIn, and Twitter.</span></span>
<span data-ttu-id="0f55c-109">Если вы щелкнете их, откроется сайт социальной сети и вы сможете быстро поделиться ссылкой на этот элемент.</span><span class="sxs-lookup"><span data-stu-id="0f55c-109">Clicking on these links will open the social media site, and allow quickly sharing a link to the item.</span></span>

<span data-ttu-id="0f55c-110">Пользователям необходимо войти на сайт, на котором они хотят поделиться элементом коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f55c-110">Users must log in to the site they have chosen in order to share the PowerShell Gallery item.</span></span>

<span data-ttu-id="0f55c-111">Мы рекомендуем делать это, если пользователь считает, что следует посоветовать этот элемент другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="0f55c-111">Users are encouraged to do this if they find that an item is something they would recommend to others.</span></span>
<span data-ttu-id="0f55c-112">Коллекция PowerShell проверяет, сколько раз элемент был "рекомендован" на каждом сайте социальной сети, и отображает эти данные по элементу для каждого сайта социальной сети.</span><span class="sxs-lookup"><span data-stu-id="0f55c-112">The PowerShell Gallery will check each social media site for "shares" of the item, and display how many times that item has been shared in each of the social media sites.</span></span>
<span data-ttu-id="0f55c-113">Так как отображается только количество рекомендаций, другие пользователи воспримут это как отметку "Нравится".</span><span class="sxs-lookup"><span data-stu-id="0f55c-113">Since this shows only the count of times something has been shared, it will be intepreted other users as "liking" the item.</span></span>


## <a name="comments"></a><span data-ttu-id="0f55c-114">Комментарии</span><span class="sxs-lookup"><span data-stu-id="0f55c-114">Comments</span></span>

<span data-ttu-id="0f55c-115">Коллекции PowerShell используют службу LiveFyre, чтобы позволить пользователям комментировать элементы.</span><span class="sxs-lookup"><span data-stu-id="0f55c-115">The PowerShell Gallery uses the LiveFyre service to allow users to comment on items.</span></span>
<span data-ttu-id="0f55c-116">Пользователи, у которых есть советы или отзывы, могут использовать эту функцию, чтобы предоставить отзыв, который виден всем, кто посещает страницу элемента.</span><span class="sxs-lookup"><span data-stu-id="0f55c-116">Users who have recommendations or feedback can use this feature to provide feedback that is visible to anyone who visits the item page.</span></span>
<span data-ttu-id="0f55c-117">Владельцы элемента могут подписаться на этот отзыв и получать уведомления, когда кто-то публикует комментарий.</span><span class="sxs-lookup"><span data-stu-id="0f55c-117">Item owners can Follow this feedback, and be notified when someone posts a comment.</span></span>

<span data-ttu-id="0f55c-118">Система комментариев основана на отдельной службе LiveFyre. Этой службой не управляет корпорация Майкрософт, и она требует использования уникального имени для входа.</span><span class="sxs-lookup"><span data-stu-id="0f55c-118">The Comment system is based on LiveFyre, which is a separate service that is not managed by Microsoft, and requires unique login to use.</span></span>
<span data-ttu-id="0f55c-119">Когда вы решите впервые оставить комментарий или подписаться на комментарии к одному из своих элементов, вам будет предложено создать учетную запись LiveFyre.</span><span class="sxs-lookup"><span data-stu-id="0f55c-119">The first time you choose to leave a comment or Follow comments on one of your items, you will be prompted to create a LiveFyre account.</span></span>

<span data-ttu-id="0f55c-120">Если вы создали учетную запись LiveFyre и вошли в систему, вы можете создать комментарий с отзывом об элементе, а затем щелкнуть "Опубликовать комментарий...". Комментарий появится не сразу.</span><span class="sxs-lookup"><span data-stu-id="0f55c-120">If you have created a LiveFyre account and logged in, you can craft a comment that provides feedback on the item, then click on "Post comment..." The comment will not be visible immediately.</span></span>
<span data-ttu-id="0f55c-121">Комментарии к элементам коллекции модерируют администраторы коллекции PowerShell. Модераторы просматривают все сообщения перед их публикацией и отображением для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="0f55c-121">Comments for gallery items are moderated by the PowerShell Gallery administrators, and all posts are reviewed by the moderators before being published and visible to others.</span></span>
<span data-ttu-id="0f55c-122">Наша цель при модерировании комментариев состоит в том, чтобы они соответствовали нормам общественного поведения согласно [условиям использования](https://www.powershellgallery.com/policies/Terms) коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f55c-122">Our purpose in moderating the comments is to ensure that they align with public behavior consistent with the PowerShell Gallery [Terms of Use](https://www.powershellgallery.com/policies/Terms).</span></span>

<span data-ttu-id="0f55c-123">Мы рекомендуем владельцам элементов подписываться на комментарии, которые публикуются в LiveFyre.</span><span class="sxs-lookup"><span data-stu-id="0f55c-123">Item owners are encouraged to Follow comments that are posted to LiveFyre.</span></span>
<span data-ttu-id="0f55c-124">Для этого необходима учетная запись LiveFyre. Мы советуем использовать тот же адрес электронной почты, который используется при публикации элемента в LiveFyre.</span><span class="sxs-lookup"><span data-stu-id="0f55c-124">A LiveFyre account is required, and it is recommended to use the same email address you use for publishing your item in LiveFyre.</span></span>
<span data-ttu-id="0f55c-125">Чтобы подписаться на комментарии, зайдите в LiveFyre и перейдите к любому элементу, где вы числитесь владельцем.</span><span class="sxs-lookup"><span data-stu-id="0f55c-125">To Follow comments, log into LiveFyre, and navigate to any item where you are listed as an Owner.</span></span>
<span data-ttu-id="0f55c-126">Под полем комментариев под каждым элементом вы увидите кнопку "+Подписаться".</span><span class="sxs-lookup"><span data-stu-id="0f55c-126">Below the Comment box at the bottom of each item you will see "+Follow".</span></span>
<span data-ttu-id="0f55c-127">После того как вы щелкните ее, LiveFyre будет отправлять письмо по зарегистрированному адресу электронной почты каждый раз, когда будут публиковаться новые комментарии к элементу.</span><span class="sxs-lookup"><span data-stu-id="0f55c-127">Once you click on this, LiveFyre will send an email to the registered email address any time new comments made on the item.</span></span>