# Lab 2: Desplegar un Modelo OpenAI

## Objetivo
Desplegar un modelo de Azure OpenAI Service para su uso con Business Central y el Copilot Toolkit.

---

## Introducción: ¿Por qué un modelo OpenAI para Business Central?

### Integración con Copilot Toolkit

Las codeunits oficiales del Copilot Toolkit están diseñadas específicamente para conectarse con Azure OpenAI Service endpoints. Estas incluyen:

- **"AOAI Chat Messages"**
- **"AOAI Operation Response"**
- **"AOAI Chat Completion Params"**
- Y otras codeunits relacionadas

### Requisitos de Conexión

Estas codeunits esperan los siguientes elementos:

1. ✅ **Un endpoint de Azure OpenAI Service**
   - URL del servicio de Azure OpenAI

2. ✅ **Una API Key de Azure OpenAI**
   - Clave de autenticación para acceder al servicio

3. ✅ **Un deployment name específico del modelo**
   - Ejemplos: `gpt-4`, `gpt-35-turbo`
   - Nombre del despliegue del modelo en tu recurso de Azure

---

## Paso 1: Crear el Recurso de Azure OpenAI

### 1.1. Acceder al Portal de Azure

1. Abre tu navegador
2. Ve a: **https://portal.azure.com**
3. Inicia sesión con tus credenciales de Azure

### 1.2. Crear un Nuevo Recurso

1. En el portal de Azure, haz clic en **"+ Create a resource"** (Crear un recurso)
2. En la barra de búsqueda, escribe: `Azure OpenAI`
3. Selecciona **"Azure OpenAI"** de los resultados
4. Haz clic en **"Create"** (Crear)

   <img width="1252" height="753" alt="image" src="https://github.com/user-attachments/assets/6c559643-698a-4d6e-9f75-d2371d7a0f82" />


### 1.3. Configurar el Recurso

Completa los siguientes campos:

#### **Basics** (Información Básica)

- **Subscription**: Selecciona tu suscripción de Azure
- **Resource group**: Selecciona o crea un grupo de recursos
- **Region**: Elige la región (ej: East US, Sweden Central)
- **Name**: Introduce un nombre único para tu recurso
- **Pricing tier**: Selecciona el nivel de precios adecuado

  <img width="708" height="751" alt="image" src="https://github.com/user-attachments/assets/51f40625-9391-4823-ac16-d78fe268c5d3" />


#### **Network** (Red)

- Configura las opciones de red según tus necesidades de seguridad

#### **Tags** (Etiquetas)

- (Opcional) Añade etiquetas para organizar tus recursos

### 1.4. Revisar y Crear

1. Haz clic en **"Review + create"**
2. Revisa la configuración
3. Haz clic en **"Create"**
4. Espera a que se complete el despliegue (puede tardar unos minutos)

<img width="1017" height="666" alt="image" src="https://github.com/user-attachments/assets/eaf8e145-fdf8-4888-a86e-291ca78290ed" />


---

## Paso 2: Ir a Azure AI Foundry

### 2.1. Desde el Portal de Azure

Una vez creado el recurso:

1. Ve a tu recurso de Azure OpenAI recién creado
2. En el menú superior o en la sección de **Overview**, busca el botón:
   - **"Go to Azure AI Foundry Studio"** o
   - **"Explore Azure AI Foundry"**
3. Haz clic en ese botón

<img width="2028" height="852" alt="image" src="https://github.com/user-attachments/assets/1cebac8b-738b-495a-a94e-efbf508d8f44" />


### 2.2. Acceso Directo

Alternativamente, puedes ir directamente a:
- **https://ai.azure.com/**
- Selecciona tu recurso de Azure OpenAI de la lista de recursos

---

## Paso 3: Desplegar un Modelo

### 3.1. Navegar a Deployments

1. En Azure AI Foundry, ve al menú lateral izquierdo
2. Haz clic en **"Deployments"** o **"Model deployments"** o **"Implementaciones"**

### 3.2. Crear un Nuevo Deployment

1. Haz clic en **"+ Create new deployment"**
2. Selecciona el modelo que deseas desplegar:
   - **gpt-4** - Modelo más avanzado
   - **gpt-4-turbo** - Versión optimizada de GPT-4
   - **gpt-35-turbo** - Versión más rápida y económica
   - **gpt-4o** - Último modelo optimizado

<img width="1255" height="663" alt="image" src="https://github.com/user-attachments/assets/ba1750e8-026b-4073-a270-1096258184a5" />



### 3.3. Configurar el Deployment

- **Deployment name**: Introduce un nombre descriptivo
  - Ejemplo: `gpt-4-deployment` o `gpt-35-turbo-prod`
  - ⚠️ **Importante**: Este nombre será necesario en Business Central
- **Model version**: Selecciona la versión del modelo
- **Deployment type**: Selecciona el tipo (Standard o Provisioned)
- **Tokens per minute rate limit**: Configura el límite de tokens

### 3.4. Confirmar Deployment

1. Revisa la configuración
2. Haz clic en **"Create"**
3. Espera a que se complete el despliegue

<img width="697" height="713" alt="image" src="https://github.com/user-attachments/assets/10f6ff48-51cb-4619-aeb2-6981e1c1b5df" />


---

## Paso 4: Obtener las Credenciales para Business Central

### 4.1. Endpoint URL

1. Ve a tu recurso en Azure AI Foundry
2. En el menú, selecciona **"Keys and Endpoint"** o equivalente
3. Copia la **Endpoint URL**
   - Formato: `https://YOUR-RESOURCE.openai.azure.com/`

### 4.2. API Key

1. En la misma sección **"Keys and Endpoint"**
2. Copia la **Key 1** o **Key 2**
3. ⚠️ **Importante**: Guarda esta clave de forma segura

### 4.3. Deployment Name

- Es el nombre que le diste al deployment en el Paso 3.3
- Ejemplo: `gpt-4-deployment` o `gpt-35-turbo-prod`

---

## Paso 5: Probar el Modelo (Opcional)

### 5.1. Usar el Chat Playground

1. En Azure AI Foundry, ve a **"Playgrounds" → "Chat"**
2. Selecciona tu deployment
3. Escribe un mensaje de prueba
4. Verifica que el modelo responde correctamente

---

## Resumen: Información para Business Central

Al finalizar este lab, deberás tener:

| Elemento | Descripción | Ejemplo |
|----------|-------------|---------|
| **Endpoint** | URL del servicio | `https://mi-recurso.openai.azure.com/` |
| **API Key** | Clave de autenticación | `abc123...xyz789` |
| **Deployment Name** | Nombre del modelo desplegado | `gpt-4-deployment` |

Esta información será necesaria para configurar las codeunits del Copilot Toolkit en Business Central.

---

## Notas Importantes

- 🔒 **Seguridad**: Nunca compartas tu API Key públicamente
- 💰 **Costos**: Los modelos OpenAI tienen costos asociados por uso
- 📊 **Límites**: Respeta los rate limits configurados
- 🔄 **Versiones**: Mantén actualizadas las versiones de los modelos

---

## Próximos Pasos

En el siguiente lab, aprenderás a:
- Configurar Business Central con estas credenciales
- Utilizar las codeunits del Copilot Toolkit
- Crear tu primera integración con OpenAI

---

## Troubleshooting

### Error: "Deployment failed"
- Verifica que tienes cuota disponible en tu suscripción
- Comprueba que la región seleccionada soporta el modelo

### No veo el botón "Go to Azure AI Foundry"
- Asegúrate de que el recurso se ha desplegado completamente
- Refresca la página del portal de Azure

### El modelo no responde en el Playground
- Verifica que el deployment está en estado "Succeeded"
- Comprueba que has seleccionado el deployment correcto

---

*Instructor: Roberto Corella*  
*LinkedIn: https://www.linkedin.com/in/robertocorella/*
*Fecha: Octubre 2025*
