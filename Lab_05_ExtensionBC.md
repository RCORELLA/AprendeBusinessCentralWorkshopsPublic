# Lab-05: Extensión de Business Central con IA - Integración OpenAI

## Objetivo
Crear una extensión para Microsoft Dynamics 365 Business Central que integre OpenAI desde la ficha de clientes, utilizando una Prompt Dialog Page con guías de preguntas (Prompt Guides).

## Requisitos Previos

- Visual Studio Code instalado
- Extensión AL Language para VS Code
- Business Central Development Environment (Sandbox)
- Cuenta de OpenAI con API Key
- Conocimientos básicos de AL Language

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
│       └── PromptGuideType.Enum.al
├── app.json
└── README.md
```

## Paso 1: Configuración Inicial

### 1.1 Crear el archivo `app.json`
```json
{
  "id": "12345678-1234-1234-1234-123456789012",
  "name": "OpenAI Customer Assistant",
  "publisher": "Tu Nombre",
  "version": "1.0.0.0",
  "brief": "Integración de OpenAI en ficha de clientes",
  "description": "Extensión que permite realizar consultas a OpenAI desde la ficha de clientes",
  "privacyStatement": "",
  "EULA": "",
  "help": "",
  "url": "",
  "logo": "",
  "dependencies": [],
  "screenshots": [],
  "platform": "1.0.0.0",
  "application": "26.0.0.0",
  "idRanges": [
    {
      "from": 50100,
      "to": 50149
    }
  ],
  "features": [
    "TranslationFile"
  ],
  "runtime": "15.0"
}
```

## Paso 2: Crear el Enum para Prompt Guides

### 2.1 Archivo `PromptGuideType.Enum.al`
```al
enum 50100 "Prompt Guide Type"
{
    Extensible = true;

    value(0; " ")
    {
        Caption = ' ';
    }
    value(1; "Customer Analysis")
    {
        Caption = 'Análisis de Cliente';
    }
    value(2; "Sales Prediction")
    {
        Caption = 'Predicción de Ventas';
    }
    value(3; "Marketing Suggestions")
    {
        Caption = 'Sugerencias de Marketing';
    }
    value(4; "Credit Risk Assessment")
    {
        Caption = 'Evaluación de Riesgo Crediticio';
    }
    value(5; "Custom Question")
    {
        Caption = 'Pregunta Personalizada';
    }
}
```

## Paso 3: Crear la Codeunit de Integración con OpenAI

### 3.1 Archivo `OpenAIIntegration.Codeunit.al`
```al
codeunit 50100 "OpenAI Integration"
{
    procedure CallOpenAI(CustomerNo: Code[20]; PromptType: Enum "Prompt Guide Type"; CustomPrompt: Text): Text
    var
        Client: HttpClient;
        RequestMessage: HttpRequestMessage;
        ResponseMessage: HttpResponseMessage;
        RequestContent: HttpContent;
        Headers: HttpHeaders;
        ResponseText: Text;
        RequestBody: Text;
        ApiKey: Text;
        ApiUrl: Text;
    begin
        // Configuración de la API
        ApiKey := GetOpenAIApiKey();
        ApiUrl := 'https://api.openai.com/v1/chat/completions';

        if ApiKey = '' then
            Error('La API Key de OpenAI no está configurada.');

        // Construir el prompt según el tipo
        RequestBody := BuildRequestBody(CustomerNo, PromptType, CustomPrompt);

        // Configurar headers
        RequestContent.WriteFrom(RequestBody);
        RequestContent.GetHeaders(Headers);
        Headers.Clear();
        Headers.Add('Content-Type', 'application/json');

        Client.DefaultRequestHeaders.Add('Authorization', 'Bearer ' + ApiKey);

        // Realizar la petición
        if Client.Post(ApiUrl, RequestContent, ResponseMessage) then begin
            if ResponseMessage.IsSuccessStatusCode() then begin
                ResponseMessage.Content.ReadAs(ResponseText);
                exit(ParseOpenAIResponse(ResponseText));
            end else
                Error('Error en la llamada a OpenAI: %1', ResponseMessage.ReasonPhrase);
        end else
            Error('No se pudo conectar con OpenAI.');
    end;

    local procedure BuildRequestBody(CustomerNo: Code[20]; PromptType: Enum "Prompt Guide Type"; CustomPrompt: Text): Text
    var
        Customer: Record Customer;
        PromptText: Text;
        JsonBody: Text;
    begin
        if not Customer.Get(CustomerNo) then
            Error('Cliente no encontrado.');

        // Construir el prompt según el tipo seleccionado
        case PromptType of
            PromptType::"Customer Analysis":
                PromptText := StrSubstNo('Analiza el siguiente cliente y proporciona insights: Nombre: %1, Saldo: %2, Límite de crédito: %3',
                    Customer.Name, Customer."Balance (LCY)", Customer."Credit Limit (LCY)");
            PromptType::"Sales Prediction":
                PromptText := StrSubstNo('Basándote en el historial, predice las ventas futuras para el cliente: %1', Customer.Name);
            PromptType::"Marketing Suggestions":
                PromptText := StrSubstNo('Proporciona sugerencias de marketing para el cliente: %1 del sector: %2',
                    Customer.Name, Customer."Customer Posting Group");
            PromptType::"Credit Risk Assessment":
                PromptText := StrSubstNo('Evalúa el riesgo crediticio del cliente: %1 con saldo: %2 y límite: %3',
                    Customer.Name, Customer."Balance (LCY)", Customer."Credit Limit (LCY)");
            PromptType::"Custom Question":
                PromptText := CustomPrompt;
        end;

        // Construir el JSON para OpenAI
        JsonBody := '{' +
            '"model": "gpt-4",' +
            '"messages": [' +
            '{"role": "system", "content": "Eres un asistente experto en análisis de clientes para Business Central."},' +
            '{"role": "user", "content": "' + PromptText + '"}' +
            '],' +
            '"temperature": 0.7,' +
            '"max_tokens": 500' +
            '}';

        exit(JsonBody);
    end;

    local procedure ParseOpenAIResponse(ResponseText: Text): Text
    var
        JsonObject: JsonObject;
        JsonToken: JsonToken;
        ChoicesArray: JsonArray;
        MessageContent: Text;
    begin
        if not JsonObject.ReadFrom(ResponseText) then
            Error('Error al parsear la respuesta de OpenAI.');

        if JsonObject.Get('choices', JsonToken) then begin
            ChoicesArray := JsonToken.AsArray();
            if ChoicesArray.Get(0, JsonToken) then begin
                JsonObject := JsonToken.AsObject();
                if JsonObject.Get('message', JsonToken) then begin
                    JsonObject := JsonToken.AsObject();
                    if JsonObject.Get('content', JsonToken) then
                        MessageContent := JsonToken.AsValue().AsText();
                end;
            end;
        end;

        exit(MessageContent);
    end;

    local procedure GetOpenAIApiKey(): Text
    begin
        // Aquí deberías implementar un método seguro para obtener la API Key
        // Por ejemplo, desde una tabla de configuración o Azure Key Vault
        exit('tu-api-key-aqui');
    end;
}
```

## Paso 4: Crear la Prompt Dialog Page

### 4.1 Archivo `OpenAIPromptDialog.Page.al`
```al
page 50100 "OpenAI Prompt Dialog"
{
    PageType = PromptDialog;
    Caption = 'Asistente IA para Clientes';
    Extensible = false;
    IsPreview = true;

    PromptMode = Prompt;

    layout
    {
        area(Prompt)
        {
            field(PromptGuide; PromptGuideType)
            {
                ApplicationArea = All;
                Caption = 'Guía de Preguntas';
                ToolTip = 'Selecciona una guía predefinida o personaliza tu pregunta';

                trigger OnValidate()
                begin
                    if PromptGuideType <> PromptGuideType::"Custom Question" then
                        UserPrompt := '';
                end;
            }

            field(UserPrompt; UserPrompt)
            {
                ApplicationArea = All;
                Caption = 'Tu Pregunta';
                MultiLine = true;
                ToolTip = 'Escribe tu pregunta personalizada';
                Enabled = PromptGuideType = PromptGuideType::"Custom Question";
            }
        }

        area(Content)
        {
            field(AIResponse; AIResponse)
            {
                ApplicationArea = All;
                Caption = 'Respuesta de IA';
                MultiLine = true;
                Editable = false;
                ToolTip = 'Respuesta generada por OpenAI';
            }
        }
    }

    actions
    {
        area(SystemActions)
        {
            systemaction(Generate)
            {
                Caption = 'Generar';
                ToolTip = 'Genera la respuesta usando OpenAI';

                trigger OnAction()
                var
                    OpenAIIntegration: Codeunit "OpenAI Integration";
                begin
                    if CustomerNo = '' then
                        Error('No se ha especificado un cliente.');

                    if (PromptGuideType = PromptGuideType::"Custom Question") and (UserPrompt = '') then
                        Error('Debes escribir una pregunta personalizada.');

                    AIResponse := OpenAIIntegration.CallOpenAI(CustomerNo, PromptGuideType, UserPrompt);
                end;
            }

            systemaction(OK)
            {
                Caption = 'Aceptar';
            }

            systemaction(Cancel)
            {
                Caption = 'Cancelar';
            }
        }
    }

    var
        PromptGuideType: Enum "Prompt Guide Type";
        UserPrompt: Text;
        AIResponse: Text;
        CustomerNo: Code[20];

    procedure SetCustomer(NewCustomerNo: Code[20])
    begin
        CustomerNo := NewCustomerNo;
    end;
}
```

## Paso 5: Extender la Customer Card

### 5.1 Archivo `CustomerCardExt.PageExt.al`
```al
pageextension 50100 "Customer Card AI Ext" extends "Customer Card"
{
    actions
    {
        addlast(processing)
        {
            action(OpenAIAssistant)
            {
                ApplicationArea = All;
                Caption = 'Asistente IA';
                ToolTip = 'Abre el asistente de IA para consultas sobre este cliente';
                Image = Sparkle;
                Promoted = true;
                PromotedCategory = Process;
                PromotedIsBig = true;

                trigger OnAction()
                var
                    PromptDialog: Page "OpenAI Prompt Dialog";
                begin
                    PromptDialog.SetCustomer(Rec."No.");
                    PromptDialog.RunModal();
                end;
            }
        }
    }
}
```

## Paso 6: Configuración y Despliegue

### 6.1 Archivo `launch.json`
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Your own server",
            "type": "al",
            "request": "launch",
            "server": "http://localhost",
            "serverInstance": "BC220",
            "port": 7049,
            "tenant": "default",
            "authentication": "UserPassword"
        }
    ]
}
```

### 6.2 Compilar y Publicar

1. Presiona `F5` en Visual Studio Code
2. La extensión se compilará y publicará en tu entorno de desarrollo
3. Accede a Business Central y navega a la ficha de un cliente
4. Verás el nuevo botón "Asistente IA"

## Paso 7: Configuración de Seguridad

### 7.1 Almacenamiento Seguro de API Key

**Importante:** Nunca almacenes la API Key directamente en el código. Implementa una de estas soluciones:

1. **Tabla de Configuración:**
```al
table 50100 "OpenAI Setup"
{
    DataClassification = CustomerContent;

    fields
    {
        field(1; "Primary Key"; Code[10])
        {
            DataClassification = SystemMetadata;
        }
        field(2; "API Key"; Text[250])
        {
            DataClassification = EndUserIdentifiableInformation;
            ExtendedDatatype = Masked;
        }
    }

    keys
    {
        key(PK; "Primary Key")
        {
            Clustered = true;
        }
    }
}
```

2. **Uso de Azure Key Vault** (recomendado para producción)

## Mejores Prácticas Aplicadas

✅ **Naming Conventions:** Objetos con nombres descriptivos y prefijos consistentes  
✅ **Object IDs:** Uso del rango asignado (50100-50149)  
✅ **Caption y ToolTip:** Todos los campos tienen descripción  
✅ **Error Handling:** Manejo de errores en llamadas HTTP  
✅ **Data Classification:** Campos clasificados correctamente  
✅ **Extensibility:** Uso de Enums extensibles  
✅ **User Experience:** Prompt Guides para facilitar el uso  

## Pruebas

### Casos de Prueba

1. **Análisis de Cliente:** Selecciona un cliente con datos completos y usa la guía "Análisis de Cliente"
2. **Pregunta Personalizada:** Escribe una pregunta específica sobre ventas o historial
3. **Validación de Errores:** Prueba sin API Key configurada
4. **Límites de Crédito:** Usa la guía de riesgo crediticio

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
