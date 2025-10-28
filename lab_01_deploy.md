# Lab: Configuración Inicial de Azure OpenAI

## Objetivo
Acceder al portal de Azure OpenAI y familiarizarse con los recursos disponibles.

---

## Paso 1: Acceder al Portal

1. Abre tu navegador web
2. Dirígete a la URL: **https://ai.azure.com/**
3. Inicia sesión con tus credenciales de Azure

---

## Paso 2: Explorar el Portal de Azure AI Foundry

Una vez dentro del portal, verás la interfaz principal con las siguientes secciones:

### Menú Lateral Izquierdo

#### **Home**
- Página principal del portal

#### **Get started**
- Recursos y tutoriales para comenzar

#### **Model catalog**
- Catálogo de modelos de IA disponibles

#### **Playgrounds** (Áreas de prueba)
- **Chat**: Interfaz para probar modelos conversacionales
- **Assistants** (PREVIEW): Crear asistentes personalizados
- **Video** (PREVIEW): Herramientas de procesamiento de video
- **Audio** (PREVIEW): Herramientas de procesamiento de audio
- **Images**: Generación y procesamiento de imágenes

#### **Tools** (Herramientas)
- **Fine-tuning**: Ajuste fino de modelos
- **Azure OpenAI**: Gestión de recursos OpenAI

---

## Paso 3: Revisar Recursos Recientes

En el panel central verás la sección **"Recent resources"** que muestra:

### Recursos Disponibles

1. **customer360** (Azure OpenAI - eastus)
   - Recurso principal de OpenAI

2. **usOpenAiwithDalle** (Azure OpenAI - eastus)
   - Recurso con capacidades DALL-E

3. **customer360** (Project Default - eastus)
   - Proyecto por defecto con recurso AI Foundry

---

## Paso 4: Crear un Nuevo Proyecto

### 4.1. Iniciar la Creación

1. En el panel principal, haz clic en el botón **"+ Create new"**
2. Selecciona **"Project"** (Proyecto)

### 4.2. Configuración Básica del Proyecto

En la pantalla "Create a project", completa los siguientes campos:

<img width="739" height="759" alt="image" src="https://github.com/user-attachments/assets/28425ec1-bcce-4c7d-a353-9b99f2fecfd7" />


#### **Project Name** (Nombre del Proyecto) *
- Introduce un nombre descriptivo para tu proyecto
- Ejemplo: `Demo-Companial`

### 4.3. Opciones Avanzadas

Expande la sección **"Advanced options"** para configurar:

#### **Azure AI Foundry resource** *
- Nombre del recurso de Azure AI Foundry
- Ejemplo: `demo-companial-resource`

#### **Subscription** *
- Selecciona tu suscripción de Azure
- Ejemplo: `rcorella`
- Si necesitas crear una nueva: haz clic en **"Create a new subscription"** 🔗

#### **Resource group** *
- Selecciona un grupo de recursos existente o crea uno nuevo
- Ejemplo: `(new) rg-rcorella-3874`
- Para crear un nuevo grupo:
  1. Escribe el nombre del nuevo grupo
  2. Haz clic en **"Create new resource group"**
  3. Introduce el nombre (ej: `Demo-Companial`)
  4. Haz clic en **"OK"**

#### **Public network access**
- Estado: **Enabled** (Habilitado por defecto)
- Permite el acceso desde internet público

#### **Region** *
- Selecciona la región donde se alojará el proyecto
- Ejemplo: `Sweden Central`
- Otras opciones comunes: East US, West Europe, etc.

### 4.4. Políticas y Seguridad

En la parte inferior verás:
- Enlace a políticas de datos, privacidad y seguridad
- **"Configure in Azure Portal"** 🔗 - Para configuración avanzada

### 4.5. Crear el Proyecto

1. Revisa que todos los campos obligatorios (*) estén completos
2. Haz clic en el botón azul **"Create"**
3. Alternativamente, haz clic en **"Cancel"** para cancelar

### 4.6. Proceso de Configuración

Una vez iniciada la creación, verás una pantalla con:

- **"Welcome to Azure AI Foundry"**
- **"Jumpstart your AI journey"** - Descripción de las capacidades
  - Buscar modelos ideales de OpenAI, Mistral, Meta y otros proveedores
  - Vincular, testear y personalizar dentro de un proyecto
  - Botón **"Explore models"** para comenzar



## Paso 5: Confirmar los EndPoints

<img width="991" height="886" alt="image" src="https://github.com/user-attachments/assets/1799a091-2ea3-47e9-b7cf-d7c87d4b0f3c" />

## Paso 6: Elegir el modelo

<img width="1591" height="753" alt="image" src="https://github.com/user-attachments/assets/34aa5e94-d0d9-4ab2-8c91-ac75addd3415" />

## Paso 7: Desplegar en una webApp

<img width="1154" height="917" alt="image" src="https://github.com/user-attachments/assets/63300be2-abe7-442b-ab14-9da94675749b" />

Una vez desplegada, podrás acceder a la webApp

<img width="670" height="909" alt="image" src="https://github.com/user-attachments/assets/6ae73a2d-5e78-498a-85ad-a9ad98f34319" />


<img width="1182" height="711" alt="image" src="https://github.com/user-attachments/assets/d5efc74d-87df-4f25-99ec-1be2fd1e5ebd" />

---

## Notas Importantes

- La región predeterminada para estos recursos es **East US**
- Algunos servicios están en **PREVIEW** (Vista previa)
- Puedes buscar recursos específicos usando la barra de búsqueda en la parte superior

---

## Próximos Pasos

Una vez familiarizado con el portal:
1. Explora el **Model catalog** para ver los modelos disponibles
2. Prueba el **Chat Playground** para interactuar con los modelos
3. Revisa la documentación en **Get started**

---

## Recursos Adicionales

- Portal: https://ai.azure.com/
- Documentación oficial de Azure OpenAI
- Ejemplos y tutoriales en el portal

---

*Instructor: Roberto Corella*  
*LinkedIn: https://www.linkedin.com/in/robertocorella/*
