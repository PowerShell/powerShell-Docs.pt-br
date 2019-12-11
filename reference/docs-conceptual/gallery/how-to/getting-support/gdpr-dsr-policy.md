---
ms.date: 03/27/2018
contributor: JKeithB
keywords: galeria,powershell,psgallery,GDPR
title: Conformidade da Galeria do PowerShell com o GDPR
ms.openlocfilehash: fb1191d8a1cd12d5994e41238c384eb504d0c261
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71328317"
---
# <a name="powershell-gallery-gdpr-compliance"></a><span data-ttu-id="524b0-103">Conformidade da Galeria do PowerShell com o GDPR</span><span class="sxs-lookup"><span data-stu-id="524b0-103">PowerShell Gallery GDPR compliance</span></span>

## <a name="overview"></a><span data-ttu-id="524b0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="524b0-104">Overview</span></span>

<span data-ttu-id="524b0-105">Em maio de 2018, uma lei de privacidade europeia, o RGPD (Regulamento Geral sobre a Proteção de Dados), entrou em vigor.</span><span class="sxs-lookup"><span data-stu-id="524b0-105">In May 2018, a European privacy law, the General Data Protection Regulation (GDPR), took effect.</span></span>
<span data-ttu-id="524b0-106">O GDPR impõe novas regras para empresas, agências governamentais, organizações sem fins lucrativos e outras entidades que oferecem produtos e serviços a pessoas da EU (União Europeia) ou que coletam e analisam dados vinculados a residentes da UE.</span><span class="sxs-lookup"><span data-stu-id="524b0-106">The GDPR imposes new rules on companies, government agencies, non-profits, and other organizations that offer goods and services to people in the European Union (EU), or that collect and analyze data tied to EU residents.</span></span>
<span data-ttu-id="524b0-107">O GDPR aplica-se independentemente de onde você esteja localizado.</span><span class="sxs-lookup"><span data-stu-id="524b0-107">The GDPR applies no matter where you are located.</span></span>

> [!NOTE]
> <span data-ttu-id="524b0-108">Este artigo mostra as etapas para excluir dados pessoais da Galeria do PowerShell e pode ser usado para ajudá-lo a cumprir suas obrigações com o GDPR.</span><span class="sxs-lookup"><span data-stu-id="524b0-108">This article provides steps for how to delete personal data from the PowerShell Gallery and can be used to support your obligations under the GDPR.</span></span> <span data-ttu-id="524b0-109">Se você estiver buscando informações gerais sobre o GDPR, confira a [seção GDPR do portal do serviço de confiança](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span><span class="sxs-lookup"><span data-stu-id="524b0-109">If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span></span>

## <a name="personally-identifiable-data"></a><span data-ttu-id="524b0-110">Dados de identificação pessoal</span><span class="sxs-lookup"><span data-stu-id="524b0-110">Personally identifiable data</span></span>

<span data-ttu-id="524b0-111">A Galeria do PowerShell armazena as seguintes informações que podem ser fornecidas pelos usuários podendo conter informações pessoais:</span><span class="sxs-lookup"><span data-stu-id="524b0-111">The PowerShell Gallery stores the following information that may be provided by users, which may contain personal information:</span></span>

- <span data-ttu-id="524b0-112">Conta da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-112">PowerShell Gallery account</span></span>
- <span data-ttu-id="524b0-113">Pacotes publicados na Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-113">Packages published to the PowerShell Gallery</span></span>
- <span data-ttu-id="524b0-114">Correspondência de email com a equipe da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-114">Email correspondence with the PowerShell Gallery team</span></span>

<span data-ttu-id="524b0-115">A maioria dos usuários não cria uma conta da Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-115">Most users do not create a PowerShell Gallery account.</span></span>
<span data-ttu-id="524b0-116">Não é necessário ter uma conta, a menos que você pretenda publicar um pacote ou usar o recurso "Contatar Proprietário" na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-116">An account is not required unless you are going to publish a package or use the "Contact Owner" feature in the PowerShell Gallery.</span></span>
<span data-ttu-id="524b0-117">Além da correspondência de email iniciada pelo usuário, a Galeria do PowerShell não armazena dados de identificação pessoal de usuários que não criaram uma conta.</span><span class="sxs-lookup"><span data-stu-id="524b0-117">Other than email correspondence initiated by the user, the PowerShell Gallery does not store personally identifiable data for users who have not created an account.</span></span>

<span data-ttu-id="524b0-118">Os usuários que criam uma conta da Galeria do PowerShell podem publicar pacotes na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-118">Users who create a PowerShell Gallery account can publish packages to the PowerShell Gallery.</span></span>
<span data-ttu-id="524b0-119">Espera-se que esses pacotes sejam o código do PowerShell, mas eles podem conter outras informações, inclusive informações pessoais.</span><span class="sxs-lookup"><span data-stu-id="524b0-119">Those packages are expected to be PowerShell code, but may contain other information including personal information.</span></span>
<span data-ttu-id="524b0-120">As informações abaixo mostrarão como você pode obter todos os pacotes que já publicou na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-120">The information below will show how you can get all the packages you have published to the PowerShell Gallery.</span></span>

## <a name="dsr-export-of-powershell-gallery-data"></a><span data-ttu-id="524b0-121">Exportação de DSR de dados da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-121">DSR Export of PowerShell Gallery Data</span></span>

<span data-ttu-id="524b0-122">As seções a seguir descrevem como a Galeria do PowerShell permite DSR (solicitações de entidade de dados), explicando como exportar as informações armazenadas na Galeria do PowerShell e como solicitar a exclusão dessas informações.</span><span class="sxs-lookup"><span data-stu-id="524b0-122">The following sections describe how the PowerShell Gallery supports data subject requests (DSR), by explaining how to export information stored in the PowerShell Gallery, and how to request deletion of this information.</span></span>

### <a name="email"></a><span data-ttu-id="524b0-123">Email</span><span class="sxs-lookup"><span data-stu-id="524b0-123">Email</span></span>

<span data-ttu-id="524b0-124">A correspondência de email a seguir pode incluir:</span><span class="sxs-lookup"><span data-stu-id="524b0-124">Email correspondence may include any of the following:</span></span>

- <span data-ttu-id="524b0-125">Email enviado aos proprietários de pacotes da Galeria do PowerShell, se as verificações de análise de código tiverem detectado algum problema em um pacote publicado por eles na Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-125">Email sent to the owners of PowerShell Gallery packages if the code analysis scans detected an issue with any package they have published to the PowerShell Gallery</span></span>
- <span data-ttu-id="524b0-126">Email enviado por qualquer pessoa para a equipe da Galeria do PowerShell usando o endereço de email na página "Fale Conosco" [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="524b0-126">Email sent by anyone to the PowerShell Gallery team using the email address in the "Contact Us" page [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span></span>
- <span data-ttu-id="524b0-127">Usuários registrados que usam o recurso "Contatar Proprietário" na Galeria do PowerShell para enviar email ao proprietário de um pacote da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-127">Registered users who use the "Contact Owner" feature in the PowerShell Gallery to send email to the owner of a package in the PowerShell Gallery</span></span>

<span data-ttu-id="524b0-128">Os emails enviados pela Galeria do PowerShell ou para ela têm uma política de retenção de 90 dias para embasar possíveis investigações de segurança caso seja descoberto algum código mal-intencionado na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-128">Emails sent by or to the PowerShell Gallery have a retention policy of 90 days to support possible security investigations should malicious code be discovered on the PowerShell Gallery.</span></span>
<span data-ttu-id="524b0-129">Os emails são excluídos pela política após 90 dias.</span><span class="sxs-lookup"><span data-stu-id="524b0-129">Emails are deleted by policy after 90 days.</span></span>

<span data-ttu-id="524b0-130">Você pode solicitar cópias de todos os emails enviados e recebidos entre o seu endereço de email e a Galeria do PowerShell nos últimos 90 dias.</span><span class="sxs-lookup"><span data-stu-id="524b0-130">You may request copies of all emails sent to or from your email address and the PowerShell Gallery within the previous 90 days.</span></span>
<span data-ttu-id="524b0-131">Para solicitar essa correspondência, envie um email para [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com) com o título: "Solicitar DSR para emails relacionados a essa conta".</span><span class="sxs-lookup"><span data-stu-id="524b0-131">To request this correspondence, send an email to [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com), with the title: "DSR Request for emails relating to this account".</span></span>
<span data-ttu-id="524b0-132">No corpo da mensagem, indique quais informações você está solicitando (por exemplo: Envie todos os emails enviados ou recebidos neste endereço de email.) Todos os emails que envolverem o seu endereço de email nos 90 dias anteriores à solicitação serão enviados em até sete dias úteis.</span><span class="sxs-lookup"><span data-stu-id="524b0-132">In the body of the message, state what information you are requesting (for example: Please send all emails sent to or received from this email address.) All emails involving your email address within 90 days of the request will be sent within 7 business days.</span></span>

### <a name="powershell-gallery-account-information"></a><span data-ttu-id="524b0-133">Informações de conta da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-133">PowerShell Gallery Account Information</span></span>

<span data-ttu-id="524b0-134">Se você tiver criado uma conta da Galeria do PowerShell, encontre todas as informações pessoais que foram armazenadas na Galeria do PowerShell executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="524b0-134">If you have created a PowerShell Gallery account, you can find all personal information that has been stored in PowerShell Gallery by taking the following steps:</span></span>

1. <span data-ttu-id="524b0-135">Entre na Galeria do PowerShell e clique no seu nome de usuário</span><span class="sxs-lookup"><span data-stu-id="524b0-135">Sign in to the PowerShell Gallery, then click on your username</span></span>
2. <span data-ttu-id="524b0-136">A próxima página exibida é a página da Conta, que mostra o endereço de email usado para a conta da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-136">The next page displayed is the Account page, which shows the email address used for the PowerShell Gallery account</span></span>

<span data-ttu-id="524b0-137">Se você tiver criado mais de uma conta na Galeria do PowerShell, será necessário repetir essas etapas para cada conta.</span><span class="sxs-lookup"><span data-stu-id="524b0-137">If you have created more than one account in the PowerShell Gallery, you will need to repeat these steps for each account.</span></span>

### <a name="packages-in-the-powershell-gallery"></a><span data-ttu-id="524b0-138">Pacotes na Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-138">Packages in the PowerShell Gallery</span></span>

<span data-ttu-id="524b0-139">Para facilitar a exportação de pacotes publicados na Galeria do PowerShell, publicamos o script "GetPSGalleryItemsForAuthor" na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-139">To facilitate exporting packages published to the PowerShell Gallery, we have published the script "GetPSGalleryItemsForAuthor" to the PowerShell Gallery.</span></span>
<span data-ttu-id="524b0-140">Esse script exporta uma cópia de cada versão de cada pacote inserido na Galeria do PowerShell com base nas informações do autor armazenadas no pacote.</span><span class="sxs-lookup"><span data-stu-id="524b0-140">This script exports a copy of every version of every package put into the PowerShell Gallery based on the author information stored in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="524b0-141">O autor é armazenado no manifesto do pacote quando o item é publicado.</span><span class="sxs-lookup"><span data-stu-id="524b0-141">The Author is stored in the package manifest when you publish your package.</span></span>
> <span data-ttu-id="524b0-142">Não há nenhuma garantia de que o autor seja a mesma identidade que a da conta usada na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="524b0-142">There is no guarantee that the Author is the same identity as the account you use in the PowerShell Gallery.</span></span>
> <span data-ttu-id="524b0-143">Se você usar algum outro valor no campo Autor, será necessário fornecer esse valor ao usar esse script.</span><span class="sxs-lookup"><span data-stu-id="524b0-143">If you use some other value in the Author field, you will need to supply that value when using this script.</span></span>

<span data-ttu-id="524b0-144">Você pode baixar o script usando o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="524b0-144">You may download the script by using the following PowerShell command:</span></span>

```powershell
Save-Script Get-repository psgallery
```

<span data-ttu-id="524b0-145">Em seguida, você pode executar o script diretamente, executando os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="524b0-145">You can then run the script directly, by running the following PowerShell commands:</span></span>

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

<span data-ttu-id="524b0-146">Será solicitado que você forneça o autor e uma pasta no sistema na qual deseja que os pacotes sejam salvos.</span><span class="sxs-lookup"><span data-stu-id="524b0-146">You will be prompted to supply the Author and a folder on your system where you want the packages to be saved.</span></span>

## <a name="deleting-personal-data-from-the-powershell-gallery"></a><span data-ttu-id="524b0-147">Excluindo dados pessoais da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-147">Deleting Personal Data From The PowerShell Gallery</span></span>

<span data-ttu-id="524b0-148">Para excluir sua conta da Galeria do PowerShell ou quaisquer pacotes que você tenha na Galeria do PowerShell, envie um email para cgadmin@microsoft.com com o título: "Solicitação do RGPD para itens relacionados a essa conta".</span><span class="sxs-lookup"><span data-stu-id="524b0-148">To delete your PowerShell Gallery account or any package you own in the PowerShell Gallery, send email to cgadmin@microsoft.com with the title: "GDPR Request for items relating to this account".</span></span>
<span data-ttu-id="524b0-149">No corpo da mensagem indique quais informações você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="524b0-149">In the body of the message state what information you want deleted.</span></span> <span data-ttu-id="524b0-150">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="524b0-150">For example:</span></span>

- <span data-ttu-id="524b0-151">Exclua a versão x.y.z do meu pacote "nome do pacote"</span><span class="sxs-lookup"><span data-stu-id="524b0-151">Please delete version x.y.z of my package "package name"</span></span>
- <span data-ttu-id="524b0-152">Exclua todas as versões do meu pacote "nome do pacote"</span><span class="sxs-lookup"><span data-stu-id="524b0-152">Please delete all versions of my package "package name"</span></span>
- <span data-ttu-id="524b0-153">Exclua a minha conta da Galeria do PowerShell</span><span class="sxs-lookup"><span data-stu-id="524b0-153">Please delete my PowerShell Gallery account</span></span>

<span data-ttu-id="524b0-154">Os administradores da Galeria do PowerShell responderão em até sete dias úteis.</span><span class="sxs-lookup"><span data-stu-id="524b0-154">The PowerShell Gallery administrators will reply within 7 business days.</span></span>
<span data-ttu-id="524b0-155">Os pacotes especificados serão excluídos em até 30 dias após o envio da solicitação.</span><span class="sxs-lookup"><span data-stu-id="524b0-155">The packages specified will be deleted within 30 days after the request is sent.</span></span>
