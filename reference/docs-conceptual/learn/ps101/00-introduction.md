---
title: Introdução
ms.date: 06/02/2020
ms.custom: Contributor-mikefrobbins
ms.reviewer: mirobb
description: Esta é a introdução do livro PowerShell 101, de Mike F. Robbins.
ms.openlocfilehash: bb6ab1a95404b5d6d5595d62df136a937a1faee4
ms.sourcegitcommit: df5e6f032ee2d4b556d50406832732d2f7dc2502
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "99595958"
---
# <a name="introduction"></a><span data-ttu-id="803dd-103">Introdução</span><span class="sxs-lookup"><span data-stu-id="803dd-103">Introduction</span></span>

<table>
  <tr><td>
  <a href="https://leanpub.com/powershell101">
  <img src="media/powershell101-150x194.png" alt="PowerShell 101 (the book)" />
  </a>
  </td>
  <td colspan=2>
<span data-ttu-id="803dd-104">Esse conteúdo apareceu originalmente no livro <em>PowerShell 101</em> por Mike F Robbins.</span><span class="sxs-lookup"><span data-stu-id="803dd-104">This content originally appeared in the book <em>PowerShell 101</em> by Mike F Robbins.</span></span> <span data-ttu-id="803dd-105">Agradecemos a Mike por conceder permissão para reutilizar seu conteúdo aqui.</span><span class="sxs-lookup"><span data-stu-id="803dd-105">We thank Mike for granting us permission to reuse his content here.</span></span> <span data-ttu-id="803dd-106">O conteúdo foi editado da publicação original.</span><span class="sxs-lookup"><span data-stu-id="803dd-106">The content has been edited from the original publication.</span></span> <span data-ttu-id="803dd-107">Você ainda pode obter o livro original do Leanpub em <a href="https://leanpub.com/powershell101">PowerShell 101</a>.</span><span class="sxs-lookup"><span data-stu-id="803dd-107">You can still get the original book from Leanpub at <a href="https://leanpub.com/powershell101">PowerShell 101</a>.</span></span>
  </td></tr>
</table>

## <a name="who-is-this-book-for"></a><span data-ttu-id="803dd-108">Para quem é este livro?</span><span class="sxs-lookup"><span data-stu-id="803dd-108">Who is this book for?</span></span>

<span data-ttu-id="803dd-109">Este é um livro de nível de entrada para qualquer pessoa que queira aprender sobre o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="803dd-109">This is an entry-level book for anyone wanting to learn PowerShell.</span></span>

<span data-ttu-id="803dd-110">Este livro se concentra na versão 5.1 do PowerShell em execução no Windows 10 e no Windows Server 2016 em um ambiente de domínio do Microsoft Active Directory.</span><span class="sxs-lookup"><span data-stu-id="803dd-110">This book focuses on PowerShell version 5.1 running on Windows 10 and Windows Server 2016 in a Microsoft Active Directory domain environment.</span></span> <span data-ttu-id="803dd-111">No entanto, os conceitos básicos se aplicam a todas as versões do PowerShell em execução em qualquer plataforma compatível.</span><span class="sxs-lookup"><span data-stu-id="803dd-111">However, the basic concepts apply to all versions of PowerShell running on any supported platform.</span></span>

## <a name="about-this-book"></a><span data-ttu-id="803dd-112">Sobre este livro</span><span class="sxs-lookup"><span data-stu-id="803dd-112">About this book</span></span>

<span data-ttu-id="803dd-113">Este livro é uma coleção do que eu gostaria que alguém tivesse me dito quando comecei a aprender o PowerShell, junto com dicas, truques e melhores práticas que aprendi usando o PowerShell nos últimos 10 anos.</span><span class="sxs-lookup"><span data-stu-id="803dd-113">This book is a collection of what I wish someone would have told me when I started learning PowerShell, along with the tips, tricks, and best practices that I've learned while using PowerShell during the past 10 years.</span></span>

<span data-ttu-id="803dd-114">Em vez de fornecer uma enorme quantidade de informações, esse livro tenta equilibrar a quantidade suficiente de informações para alguém que está apenas começando a usar o PowerShell ser bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="803dd-114">Instead of providing an enormous amount of information, this book attempts to provide a balance of enough information to be successful for someone who is just getting started with PowerShell.</span></span> <span data-ttu-id="803dd-115">Cada capítulo contém links para tópicos de ajuda específicos para quem deseja obter mais informações sobre os tópicos abordados nesse capítulo.</span><span class="sxs-lookup"><span data-stu-id="803dd-115">Each chapter contains links to specific help topics for those who want more information about the topics covered in that chapter.</span></span>

## <a name="about-the-author"></a><span data-ttu-id="803dd-116">Sobre o autor</span><span class="sxs-lookup"><span data-stu-id="803dd-116">About the author</span></span>

<span data-ttu-id="803dd-117">Mike F Robbins é ex-Microsoft MVP, coautor de _Windows PowerShell TFM 4ª Edition_ e autor colaborador do livro _PowerShell Deep Dives_.</span><span class="sxs-lookup"><span data-stu-id="803dd-117">Mike F Robbins is a former Microsoft MVP, co-author of _Windows PowerShell TFM 4th Edition_, and a contributing author in the _PowerShell Deep Dives_ book.</span></span> <span data-ttu-id="803dd-118">Mike é um forte apoiador da comunidade do PowerShell e agora é o escritor principal do [PowerShell do Azure][] na Microsoft.</span><span class="sxs-lookup"><span data-stu-id="803dd-118">Mike has been a strong supporter of the PowerShell community and is now the lead writer for [Azure PowerShell][] at Microsoft.</span></span> <span data-ttu-id="803dd-119">Ele tem um blog em [mikefrobbins.com][] e pode ser encontrado no Twitter em [@mikefrobbins][].</span><span class="sxs-lookup"><span data-stu-id="803dd-119">He blogs at [mikefrobbins.com][] and can be found on twitter [@mikefrobbins][].</span></span>

## <a name="lab-environment"></a><span data-ttu-id="803dd-120">Ambiente de laboratório</span><span class="sxs-lookup"><span data-stu-id="803dd-120">Lab environment</span></span>

<span data-ttu-id="803dd-121">Os exemplos neste livro foram projetados e testados na Edição de Aniversário do Windows 10 (Build 1607) e no Windows Server 2016 usando o PowerShell versão 5.1.</span><span class="sxs-lookup"><span data-stu-id="803dd-121">The examples in this book were designed and tested on Windows 10 Anniversary Edition (build 1607) and Windows Server 2016 using PowerShell version 5.1.</span></span> <span data-ttu-id="803dd-122">Se você estiver usando uma versão diferente do PowerShell ou do sistema operacional, seus resultados poderão ser diferentes daqueles mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="803dd-122">If you're using a different version of PowerShell or operating system, your results may differ from those shown here.</span></span>

<!-- link references -->
[@mikefrobbins]: https://twitter.com/mikefrobbins
[mikefrobbins.com]: http://mikefrobbins.com/
[PowerShell 101]: https://leanpub.com/powershell101
[PowerShell do Azure]: /powershell/azure
[Azure PowerShell]: /powershell/azure
