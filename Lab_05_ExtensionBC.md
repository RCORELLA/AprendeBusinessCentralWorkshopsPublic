# Lab-05: Extensión de Business Central con IA - Integración OpenAI

## Objetivo
Crear una extensión para Microsoft Dynamics 365 Business Central que integre OpenAI desde la ficha de clientes, utilizando una Prompt Dialog Page con guías de preguntas (Prompt Guides).

Rellena los TODOs para que podamos mostrar la página.

## Requisitos Previos

- Visual Studio Code instalado
- Extensión AL Language para VS Code
- Business Central Development Environment (Sandbox)
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
│       └── CopilotCapability.Enum.al
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

## Paso 3: Crear la Prompt Dialog Page

### 3.1 Archivo `OpenAIPromptDialog.Page.al`
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
        //TODO
        }

        area(Content)
        {
           //TODO
        }
    }

    actions
    {
        //TODO
    }

    var
        
        //TODO

   
}
```

## Paso 4: Extender la Customer Card

### 4.1 Archivo `CustomerCardExt.PageExt.al`
```al
pageextension 50100 "Customer Card AI Ext" extends "Customer Card"
{
    actions
    {
    //TODO
    }
}
```

## Paso 5: Compilar y Desplegar


1. Presiona `F5` en Visual Studio Code
2. La extensión se compilará y publicará en tu entorno de desarrollo
3. Accede a Business Central y navega a la ficha de un cliente
4. Verás el nuevo botón "Asistente IA"



 **Uso de Azure Key Vault** (recomendado para producción)

## Mejores Prácticas Aplicadas

✅ **Naming Conventions:** Objetos con nombres descriptivos y prefijos consistentes  
✅ **Object IDs:** Uso del rango asignado (50100-50149)  
✅ **Caption y ToolTip:** Todos los campos tienen descripción  
✅ **Data Classification:** Campos clasificados correctamente  
✅ **Extensibility:** Uso de Enums extensibles  


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
