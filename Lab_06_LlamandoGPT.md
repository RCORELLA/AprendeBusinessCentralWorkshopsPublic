# Lab-06: Extensión de Business Central con IA - Integración OpenAI

## Objetivo
Crear una extensión para Microsoft Dynamics 365 Business Central que integre OpenAI desde la ficha de clientes, utilizando una Prompt Dialog Page con guías de preguntas (Prompt Guides).

Rellena los TODOs para que podamos mostrar la página.

## Requisitos Previos

- Visual Studio Code instalado
- Extensión AL Language para VS Code
- Business Central Development Environment (Sandbox)
- Conocimientos básicos de AL Language
- Tener realizado el lab 5

## Estructura del Proyecto
```
Lab-05-BC-OpenAI/
├── .vscode/
│   └── launch.json
├── src/
│   ├── page/
│   │   ├── CustomerCardExt.PageExt.al
│   │   └── OpenAIPromptDialog.Page.al
│   ├── codeunit/
│   │   └── OpenAIIntegration.Codeunit.al
│   └── enum/
│       └── CopilotCapability.Enum.al
├── app.json
└── README.md
```

## Paso 1: Rellenar OpenAIIntegration.Codeunit.al
```al
codeunit 81101 "ABC AI Module"
{

    procedure Generate(UserPrompt: Text): Text
    var
        AzureOpenAI: Codeunit "Azure OpenAI";
        AOAIOperationResponse: Codeunit "AOAI Operation Response";
        AOAIChatCompletionParams: Codeunit "AOAI Chat Completion Params";
        AOAIChatMessages: Codeunit "AOAI Chat Messages";

        Result: Text;
    begin
        // Initialize the Azure OpenAI service
        // endpoint: https://your-openai-endpoint
        // apiKey: your-api-key
        // Deployment: gpt-4.1
        SetAuthorization(AzureOpenAI);

        // Set up the chat completion parameters
        // temperature 
        // maxTokens

        SetParameters(AOAIChatCompletionParams);

        // Set the Copilot capability for the Azure OpenAI service
        AzureOpenAI.SetCopilotCapability(Enum::"Copilot Capability"::"ABC Ask Me AnyThing");

        // Set the system meta prompt        
        AOAIChatMessages.SetPrimarySystemMessage(GetSystemMetaPrompt());

        // Add the user message to the chat messages
        AOAIChatMessages.AddUserMessage(GetUserPrompt(UserPrompt));

        // Add the tone option if it is set

        AzureOpenAI.GenerateChatCompletion(AOAIChatMessages, AOAIChatCompletionParams, AOAIOperationResponse);
        if AOAIOperationResponse.IsSuccess() then
            Result := AOAIChatMessages.GetLastMessage()
        else
            Result := AOAIOperationResponse.GetError() + ' - ' +
                 AOAIOperationResponse.GetStatusCode().ToText();
        exit(Result);
    end;



    // Add the parameters for the chat completion request

    local procedure SetParameters(var AOAIChatCompletionParams: Codeunit "AOAI Chat Completion Params")
    begin
        AOAIChatCompletionParams.SetMaxTokens(3500);
        AOAIChatCompletionParams.SetTemperature(0);
    end;


    local procedure GetSystemMetaPrompt(): Text
    var
        MetaPrompt: Text;
    begin
        Metaprompt := 'You are a helpful Business Central Support agent. Please provide only information related to Business Central. ' +
                      'If you do not know the answer, say "I do not know" and do not provide any other information. ' +
                      'Do not include any disclaimers or additional information. ' +
                      'Your responses should be concise and to the point.';
        exit(Metaprompt);
    end;


    local procedure GetUserPrompt(Prompt: Text): Text
    var
        DataTextBuilder: TextBuilder;

    begin
        // generating the prompt for the AI
        DataTextBuilder.AppendLine('You are an expert Business Central Support agent.');
        DataTextBuilder.AppendLine('You can review the information from the website https://learn.microsoft.com/es-es/dynamics365/business-central/');

        DataTextBuilder.AppendLine('This is the user question:');
        DataTextBuilder.AppendLine(Prompt);
        DataTextBuilder.AppendLine('You need to generate a step to step guide to help the user with their question.');

        exit(DataTextBuilder.ToText());
    end;

    local procedure SetAuthorization(var AzureOpenAI: Codeunit "Azure OpenAI")
    var
        Endpoint: Text;
        Deployment: Text;
        Apikey: Text;
    begin
        if not recAISetup.get() then
            Error('No has configurado el acceso');

        Endpoint := recAISetup.EndPoint;
        Deployment := recAISetup.Deployment;
        Apikey := recAISetup."API Key";

        AzureOpenAI.SetAuthorization(Enum::"AOAI Model Type"::"Chat Completions", Endpoint, Deployment, Apikey);
    end;



    var
        recAISetup: Record "ABC AI Setup";
        EndPoint: Text;
        Deployment: Text;
        ApiKey: Text;

}
```


## Paso 2: Crear el Enum para Registrar la App

### 2.1 Archivo `CopilotCapability.Enum.al`
```al
enumextension 50100 "Copilot Capability extensions" extends "Copilot Capability"
{
    value(50100; "ABC Ask Me AnyThing")
    {
        Caption = 'ABC Ask Me AnyThing';
    }
}
```

## Paso 3: Actualizar la Prompt Dialog Page


## Paso 4: Compilar y Desplegar


1. Presiona `F5` en Visual Studio Code
2. La extensión se compilará y publicará en tu entorno de desarrollo
3. Accede a Business Central y navega a la ficha de un cliente
4. Verás el nuevo botón "Asistente IA"



 



## Troubleshooting

| Error | Solución |
|-------|----------|
| "API Key no configurada" | Configura la API Key en el método `GetOpenAIApiKey()` |
| "Error al parsear respuesta" | Verifica el formato JSON de OpenAI |
| "Cliente no encontrado" | Asegúrate de abrir desde una ficha válida |

## Recursos Adicionales

- [Documentación AL Language](https://docs.microsoft.com/dynamics365/business-central/dev-itpro/developer/)
- [OpenAI API Documentation](https://platform.openai.com/docs/)
- [BC PromptDialog Pages](https://docs.microsoft.com/dynamics365/business-central/dev-itpro/developer/devenv-page-type-promptdialog)

## Licencia

Este proyecto es un laboratorio educativo para aprender integración con IA en Business Central.

---

**Autor:** Roberto Corella
**Fecha:** Octubre 2025  
**Versión:** 1.0.0
