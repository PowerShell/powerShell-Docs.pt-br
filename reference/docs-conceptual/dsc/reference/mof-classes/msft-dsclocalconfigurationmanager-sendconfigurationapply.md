---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método SendConfigurationApply
ms.openlocfilehash: 11b9d435bbaac1600d25ff074b6c55b236a8378b
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954883"
---
# <a name="sendconfigurationapply-method"></a>Método SendConfigurationApply

Envia o documento de configuração para o nó gerenciado e usa o Agente de Configuração para aplicar a configuração.

## <a name="syntax"></a>Sintaxe

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a>Parâmetros

*ConfigurationData* \[in\] Dados de ambiente da configuração.

*force* \[in\] **true** para forçar a configuração a parar.

## <a name="return-value"></a>Retornar valor

Retorna zero em caso de êxito; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários

Esse é um método estático.

## <a name="requirements"></a>Requisitos

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Consulte também

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
