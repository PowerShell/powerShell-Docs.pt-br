---
ms.date: 06/12/2017
contributor: JKeithB
keywords: galeria,powershell,cmdlet,psgallery
title: Excluir pacotes
ms.openlocfilehash: 6bfb43b95e51d38bd606198cb8d2d9af0aa0be1e
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71327927"
---
# <a name="deleting-packages"></a>Excluir pacotes

A Galeria do PowerShell não dá suporte à exclusão permanente de pacotes porque isso interromperia qualquer usuário que dependesse da disponibilidade desses pacotes.

Em vez disso, a Galeria de PowerShell dá suporte a uma maneira de "remover um pacote da lista", o que pode ser feito na página de gerenciamento dos pacotes no site.
Quando um pacote é removido da lista, ele não aparece mais na pesquisa e em nenhuma listagem de pacotes, tanto na Galeria do PowerShell quanto por meio dos comandos PowerShellGet.
No entanto, ele permanece disponível para download, pela especificação da versão exata, o que permite que os scripts automatizados continuem funcionando.

Se você estiver em uma situação excepcional em que acredita que um de seus pacotes precise ser excluído, isso poderá ser feito manualmente pela equipe da Galeria do PowerShell.
Por exemplo, se houver um problema de violação de direitos autorais ou conteúdo potencialmente perigoso, isso poderá ser um motivo válido para excluí-lo.
Nesse caso, você deve enviar uma solicitação de suporte por meio da [Galeria do PowerShell](https://www.PowerShellGallery.com).
