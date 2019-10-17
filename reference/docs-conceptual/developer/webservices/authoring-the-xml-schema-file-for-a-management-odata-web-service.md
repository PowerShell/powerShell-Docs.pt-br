---
title: Criando o arquivo de esquema XML para um serviço Web do Management OData | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e83c9d9-6d06-4247-94d9-e3bfd4013b11
caps.latest.revision: 4
ms.openlocfilehash: a806d012097d107b6cc35710b9a93f2b27dd1ace
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359795"
---
# <a name="authoring-the-xml-schema-file-for-a-management-odata-web-service"></a><span data-ttu-id="78088-102">Criação do arquivo de esquema XML para um serviço Web OData de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="78088-102">Authoring the XML schema file for a Management OData web service</span></span>

<span data-ttu-id="78088-103">Depois de definir os recursos que o serviço Web irá expor (consulte [criando o arquivo de esquema MOF para um serviço Web do Management OData](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)), você mapeia esses recursos para os cmdlets subjacentes do Windows PowerShell que implementam as operações com suporte para cada um recurso criando um arquivo XML que está de acordo com o [esquema de mapeamento de recursos](./resource-mapping-schema.md).</span><span class="sxs-lookup"><span data-stu-id="78088-103">After you define the resources your web service will expose (see [Authoring the MOF schema file for a Management OData web service](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)), you map those resources to the underlying Windows PowerShell cmdlets that implement the supported operations for each resource by creating an XML file that conforms to the [Resource Mapping Schema](./resource-mapping-schema.md).</span></span> <span data-ttu-id="78088-104">O arquivo XML também especifica as URLs que são usadas pelo cliente para acessar os recursos.</span><span class="sxs-lookup"><span data-stu-id="78088-104">The XML file also specifies the URLs that are used by the client to access the resources.</span></span>

## <a name="mappng-resources-to-urls"></a><span data-ttu-id="78088-105">Mappng recursos para URLs</span><span class="sxs-lookup"><span data-stu-id="78088-105">Mappng resources to URLs</span></span>

<span data-ttu-id="78088-106">A primeira parte do arquivo XML mapeia os recursos definidos no arquivo de esquema MOF para as URLs que são usadas para acessá-los.</span><span class="sxs-lookup"><span data-stu-id="78088-106">The first part of the XML file maps the resources defined in the MOF schema file to the URLs that are used to access them.</span></span> <span data-ttu-id="78088-107">O exemplo a seguir mostra esse mapeamento.</span><span class="sxs-lookup"><span data-stu-id="78088-107">The following example shows that mapping.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ResourceMetadata xmlns="http://schemas.microsoft.com/powershell-web-services/2010/09">
    <SchemaNamespace>PswsTest</SchemaNamespace>
    <ContainerName>PSWSEntityContainer</ContainerName>
    <Resources>
        <Resource>
            <RelativeUrl>Service</RelativeUrl>
            <Class>PswsTest_Service</Class>
        </Resource>
        <Resource>
            <RelativeUrl>Process</RelativeUrl>
            <Class>PswsTest_Process</Class>
        </Resource>
    </Resources>
```

## <a name="mapping-cmdlets-to-crud-operations"></a><span data-ttu-id="78088-108">Mapeando cmdlets para operações CRUD</span><span class="sxs-lookup"><span data-stu-id="78088-108">Mapping cmdlets to CRUD operations</span></span>

<span data-ttu-id="78088-109">Em seguida, você especifica os cmdlets que correspondem às operações CRUD (criar, ler, atualizar e excluir) para as quais os recursos dão suporte.</span><span class="sxs-lookup"><span data-stu-id="78088-109">You then specify the cmdlets that correspond to the CRUD (create, read, update, and delete) operations that the resources support.</span></span> <span data-ttu-id="78088-110">No [esquema de mapeamento de recursos](./resource-mapping-schema.md)do OData de gerenciamento, as operações CRUD são mapeadas da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="78088-110">In the Management OData [Resource Mapping Schema](./resource-mapping-schema.md), the CRUD operations are mapped as follows.</span></span>

|<span data-ttu-id="78088-111">Comando CRUD</span><span class="sxs-lookup"><span data-stu-id="78088-111">CRUD command</span></span>|<span data-ttu-id="78088-112">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="78088-112">XML element</span></span>|
|------------------|-----------------|
|<span data-ttu-id="78088-113">Criar</span><span class="sxs-lookup"><span data-stu-id="78088-113">Create</span></span>|<span data-ttu-id="78088-114">Criar</span><span class="sxs-lookup"><span data-stu-id="78088-114">Create</span></span>|
|<span data-ttu-id="78088-115">Leitura</span><span class="sxs-lookup"><span data-stu-id="78088-115">Read</span></span>|<span data-ttu-id="78088-116">Consulta</span><span class="sxs-lookup"><span data-stu-id="78088-116">Query</span></span>|
|<span data-ttu-id="78088-117">Atualizar</span><span class="sxs-lookup"><span data-stu-id="78088-117">Update</span></span>|<span data-ttu-id="78088-118">Atualizar</span><span class="sxs-lookup"><span data-stu-id="78088-118">Update</span></span>|
|<span data-ttu-id="78088-119">Excluir</span><span class="sxs-lookup"><span data-stu-id="78088-119">Delete</span></span>|<span data-ttu-id="78088-120">Excluir</span><span class="sxs-lookup"><span data-stu-id="78088-120">Delete</span></span>|

<span data-ttu-id="78088-121">O exemplo a seguir mostra os mapeamentos para as operações de criação, leitura e atualização no recurso `Service`.</span><span class="sxs-lookup"><span data-stu-id="78088-121">The following example shows the mappings for the Create, Read, and Update operations on the `Service` resource.</span></span>

```xml
<ClassImplementations>
        <Class>
            <Name>PswsTest_Service</Name>
            <CmdletImplementation>
                <Query>
                    <Cmdlet>Get-Service</Cmdlet>
                        <FieldParameterMap>
                            <Field>
                                <FieldName>ServiceName</FieldName>
                                <ParameterName>Name</ParameterName>
                            </Field>
                        </FieldParameterMap>
                        <ParameterSets>
                            <ParameterSet>
                                <Name>Default</Name>
                                <Parameter><Name>Name</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                            </ParameterSet>
                            <ParameterSet>
                                <Name>DisplayName</Name>
                                <Parameter><Name>DisplayName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                            </ParameterSet>
                            <ParameterSet>
                                <Name>InputObject</Name>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Query>
                <Update>
                    <Cmdlet>Set-Service</Cmdlet>
                    <FieldParameterMap>
                        <Field>
                            <FieldName>ServiceName</FieldName>
                            <ParameterName>Name</ParameterName>
                        </Field>
                    </FieldParameterMap>
                    <ParameterSets>
                        <ParameterSet>
                            <Name>Name</Name>
                            <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                            <Parameter><Name>Name</Name></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                            <Parameter><Name>Status</Name></Parameter>
                            <Parameter><Name>ErrorVariable</Name></Parameter>
                            <Parameter><Name>WarningVariable</Name></Parameter>
                            <Parameter><Name>OutVariable</Name></Parameter>
                            <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                        <ParameterSet>
                            <Name>InputObject</Name>
                            <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Update>
                <Create>
                    <Cmdlet>New-Service</Cmdlet>
                    <FieldParameterMap>
                        <Field>
                            <FieldName>ServiceName</FieldName>
                            <ParameterName>Name</ParameterName>
                        </Field>
                    </FieldParameterMap>
                    <ParameterSets>
                        <ParameterSet>
                            <Name>__AllParameterSets</Name>
                            <Parameter><Name>BinaryPathName</Name></Parameter>
                            <Parameter><Name>Name</Name></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                            <Parameter><Name>DependsOn</Name></Parameter>
                            <Parameter><Name>ErrorVariable</Name></Parameter>
                            <Parameter><Name>WarningVariable</Name></Parameter>
                            <Parameter><Name>OutVariable</Name></Parameter>
                            <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Create>
            </CmdletImplementation>
        </Class>
```

## <a name="see-also"></a><span data-ttu-id="78088-122">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="78088-122">See Also</span></span>

[<span data-ttu-id="78088-123">Criando o arquivo de esquema MOF para um serviço Web do Management OData</span><span class="sxs-lookup"><span data-stu-id="78088-123">Authoring the MOF schema file for a Management OData web service</span></span>](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

[<span data-ttu-id="78088-124">Esquema de mapeamento de recursos</span><span class="sxs-lookup"><span data-stu-id="78088-124">Resource Mapping Schema</span></span>](./resource-mapping-schema.md)

[<span data-ttu-id="78088-125">Criando um serviço Web do Management OData</span><span class="sxs-lookup"><span data-stu-id="78088-125">Creating a Management OData Web Service</span></span>](./creating-a-management-odata-web-service.md)