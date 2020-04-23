---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Criando um recurso de DSC em C#
ms.openlocfilehash: a19559c225dd91eceed397df91dd584a577cd7d4
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "74417686"
---
# <a name="authoring-a-dsc-resource-in-c"></a><span data-ttu-id="ee20e-103">Criando um recurso de DSC em C\#</span><span class="sxs-lookup"><span data-stu-id="ee20e-103">Authoring a DSC resource in C\#</span></span>

> <span data-ttu-id="ee20e-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ee20e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ee20e-105">Normalmente, um recurso personalizado de Configuração de Estado Desejado (DSC) do Windows PowerShell é implementado em um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee20e-105">Typically, a Windows PowerShell Desired State Configuration (DSC) custom resource is implemented in a PowerShell script.</span></span> <span data-ttu-id="ee20e-106">No entanto, também é possível implementar a funcionalidade de um recurso personalizado de DSC escrevendo cmdlets em C#.</span><span class="sxs-lookup"><span data-stu-id="ee20e-106">However, you can also implement the functionality of a DSC custom resource by writing cmdlets in C#.</span></span> <span data-ttu-id="ee20e-107">Para obter uma introdução sobre como escrever cmdlets em C#, consulte [Escrevendo um Cmdlet do Windows PowerShell](/powershell/scripting/developer/windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="ee20e-107">For an introduction on writing cmdlets in C#, see [Writing a Windows PowerShell Cmdlet](/powershell/scripting/developer/windows-powershell).</span></span>

<span data-ttu-id="ee20e-108">Além de implementar o recurso em C# como cmdlets, o processo de criar o esquema MOF, criando a estrutura de pastas, importar e usar o recurso personalizado de DSC é igual ao descrito em [Escrevendo um recurso personalizado de DSC com MOF](authoringResourceMOF.md).</span><span class="sxs-lookup"><span data-stu-id="ee20e-108">Aside from implementing the resource in C# as cmdlets, the process of creating the MOF schema, creating the folder structure, importing and using your custom DSC resource are the same as described in [Writing a custom DSC resource with MOF](authoringResourceMOF.md).</span></span>

## <a name="writing-a-cmdlet-based-resource"></a><span data-ttu-id="ee20e-109">Escrevendo um recurso baseado em cmdlet</span><span class="sxs-lookup"><span data-stu-id="ee20e-109">Writing a cmdlet-based resource</span></span>
<span data-ttu-id="ee20e-110">Para este exemplo, vamos implementar um recurso simples que gerencia um arquivo de texto e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ee20e-110">For this example, we will implement a simple resource that manages a text file and its contents.</span></span>

### <a name="writing-the-mof-schema"></a><span data-ttu-id="ee20e-111">Escrevendo o esquema MOF</span><span class="sxs-lookup"><span data-stu-id="ee20e-111">Writing the MOF schema</span></span>

<span data-ttu-id="ee20e-112">Segue uma definição de recurso MOF.</span><span class="sxs-lookup"><span data-stu-id="ee20e-112">The following is the MOF resource definition.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("xDemoFile")]
class MSFT_XDemoFile : OMI_BaseResource
{
                [Key, Description("path")] String Path;
                [Write, Description("Should the file be present"), ValueMap{"Present","Absent"}, Values{"Present","Absent"}] String Ensure;
                [Write, Description("Contentof file.")] String Content;
};
```

### <a name="setting-up-the-visual-studio-project"></a><span data-ttu-id="ee20e-113">Configurando o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee20e-113">Setting up the Visual Studio project</span></span>
#### <a name="setting-up-a-cmdlet-project"></a><span data-ttu-id="ee20e-114">Configurando um projeto de cmdlet</span><span class="sxs-lookup"><span data-stu-id="ee20e-114">Setting up a cmdlet project</span></span>

1. <span data-ttu-id="ee20e-115">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee20e-115">Open Visual Studio.</span></span>
1. <span data-ttu-id="ee20e-116">Crie um projeto em C# e forneça o nome.</span><span class="sxs-lookup"><span data-stu-id="ee20e-116">Create a C# project and provide the name.</span></span>
1. <span data-ttu-id="ee20e-117">Selecione **Biblioteca de Classes** nos modelos de projeto disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ee20e-117">Select **Class Library** from the available project templates.</span></span>
1. <span data-ttu-id="ee20e-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee20e-118">Click **Ok**.</span></span>
1. <span data-ttu-id="ee20e-119">Adicione uma referência de assembly a System.Automation.Management.dll ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="ee20e-119">Add an assembly reference to System.Automation.Management.dll to your project.</span></span>
1. <span data-ttu-id="ee20e-120">Altere o nome do assembly para corresponder ao nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="ee20e-120">Change the assembly name to match the resource name.</span></span> <span data-ttu-id="ee20e-121">Nesse caso, o assembly deve se chamar **MSFT_XDemoFile**.</span><span class="sxs-lookup"><span data-stu-id="ee20e-121">In this case, the assembly should be named **MSFT_XDemoFile**.</span></span>

### <a name="writing-the-cmdlet-code"></a><span data-ttu-id="ee20e-122">Escrevendo o código do cmdlet</span><span class="sxs-lookup"><span data-stu-id="ee20e-122">Writing the cmdlet code</span></span>

<span data-ttu-id="ee20e-123">O código C# a seguir implementa os cmdlets **Get-TargetResource**, **Set-TargetResource** e **Test-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="ee20e-123">The following C# code implements the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** cmdlets.</span></span>

```C#


namespace cSharpDSCResourceExample
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Management.Automation;  // Windows PowerShell assembly.

    #region Get-TargetResource

    [OutputType(typeof(System.Collections.Hashtable))]
    [Cmdlet(VerbsCommon.Get, "TargetResource")]
    public class GetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        /// <summary>
        /// Implement the logic to return the current state of the resource as a hashtable with keys being the resource properties
        /// and the values are the corresponding current value on the machine.
        /// </summary>
        protected override void ProcessRecord()
        {
            var currentResourceState = new Dictionary<string, string>();
            if (File.Exists(Path))
            {
                currentResourceState.Add("Ensure", "Present");

                // read current content
                string CurrentContent = "";
                using (var reader = new StreamReader(Path))
                {
                    CurrentContent = reader.ReadToEnd();
                }
                currentResourceState.Add("Content", CurrentContent);
            }
            else
            {
                currentResourceState.Add("Ensure", "Absent");
                currentResourceState.Add("Content", "");
            }
            // write the hashtable in the PS console.
            WriteObject(currentResourceState);
        }
    }

    # endregion

    #region Set-TargetResource
    [OutputType(typeof(void))]
    [Cmdlet(VerbsCommon.Set, "TargetResource")]
    public class SetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure {
            get
            {
                // set the default to present.
               return (this._ensure ?? "Present") ;
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Implement the logic to set the state of the machine to the desired state.
        /// </summary>
        protected override void ProcessRecord()
        {
            WriteVerbose(string.Format("Running set with parameters {0}{1}{2}", Path, Ensure, Content));
            if (File.Exists(Path))
            {
                if (Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    File.Delete(Path);
                }
                else
                {
                    // file already exist and ensure "present" is specified. start writing the content to a file
                    if (!string.IsNullOrEmpty(Content))
                    {
                        string existingContent = null;
                        using (var reader = new StreamReader(Path))
                        {
                            existingContent = reader.ReadToEnd();
                        }
                        // check if the content of the file mathes the content passed
                        if (!existingContent.Equals(Content, StringComparison.InvariantCultureIgnoreCase))
                        {
                            WriteVerbose("Existing content did not match with desired content updating the content of the file");
                            using (var writer = new StreamWriter(Path))
                            {
                                writer.Write(Content);
                                writer.Flush();
                            }
                        }
                    }
                }

            }
            else
            {
                if (Ensure.Equals("present", StringComparison.InvariantCultureIgnoreCase))
                {
                    // if nothing is passed for content just write "" otherwise write the content passed.
                    using (var writer = new StreamWriter(Path))
                    {
                        WriteVerbose(string.Format("Creating a file under path {0} with content {1}", Path, Content));
                        writer.Write(Content);
                    }
                }

            }

            /* if you need to reboot the VM. please add the following two line of code.
            PSVariable DscMachineStatus = new PSVariable("DSCMachineStatus", 1, ScopedItemOptions.AllScope);
            this.SessionState.PSVariable.Set(DscMachineStatus);
             */

        }

    }

    # endregion

    #region Test-TargetResource

    [Cmdlet("Test", "TargetResource")]
    [OutputType(typeof(Boolean))]
    public class TestTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure
        {
            get
            {
                // set the default to present.
                return (this._ensure ?? "Present");
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content
        {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Return a boolean value which indicates wheather the current machine is in desired state or not.
        /// </summary>
        protected override void ProcessRecord()
        {
            if (File.Exists(Path))
            {
                if( Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    WriteObject(false);
                }
                else
                {
                    // check if the content matches

                    string existingContent = null;
                    using (var stream = new StreamReader(Path))
                    {
                        existingContent = stream.ReadToEnd();
                    }

                    WriteObject(Content.Equals(existingContent, StringComparison.InvariantCultureIgnoreCase));
                }
            }
            else
            {
                WriteObject(Ensure.Equals("Absent", StringComparison.InvariantCultureIgnoreCase));
            }
        }
    }

    # endregion

}
```

### <a name="deploying-the-resource"></a><span data-ttu-id="ee20e-124">Implantando o recurso</span><span class="sxs-lookup"><span data-stu-id="ee20e-124">Deploying the resource</span></span>

<span data-ttu-id="ee20e-125">O arquivo dll compilado deve ser salvo em uma estrutura de arquivos semelhante a um recurso baseado em script.</span><span class="sxs-lookup"><span data-stu-id="ee20e-125">The compiled dll file should be saved in a file structure similar to a script-based resource.</span></span> <span data-ttu-id="ee20e-126">Esta é a estrutura de pastas para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ee20e-126">The following is the folder structure for this resource.</span></span>

```
$env: psmodulepath (folder)
    |- MyDscResources (folder)
        |- MyDscResources.psd1 (file, required)
        |- DSCResources (folder)
            |- MSFT_XDemoFile (folder)
                |- MSFT_XDemoFile.psd1 (file, optional)
                |- MSFT_XDemoFile.dll (file, required)
                |- MSFT_XDemoFile.schema.mof (file, required)
```

### <a name="see-also"></a><span data-ttu-id="ee20e-127">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="ee20e-127">See Also</span></span>
#### <a name="concepts"></a><span data-ttu-id="ee20e-128">Conceitos</span><span class="sxs-lookup"><span data-stu-id="ee20e-128">Concepts</span></span>
[<span data-ttu-id="ee20e-129">Escrevendo um recurso personalizado de DSC com MOF</span><span class="sxs-lookup"><span data-stu-id="ee20e-129">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
#### <a name="other-resources"></a><span data-ttu-id="ee20e-130">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="ee20e-130">Other Resources</span></span>
<span data-ttu-id="ee20e-131">[Writing a Windows PowerShell Cmdlet](/powershell/scripting/developer/windows-powershell) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ee20e-131">[Writing a Windows PowerShell Cmdlet](/powershell/scripting/developer/windows-powershell)</span></span>
