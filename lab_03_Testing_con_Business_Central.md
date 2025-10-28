# Lab03 - Probando AI en Business Central

## Objetivo
En este laboratorio aprenderás a integrar y probar capacidades de IA en Business Central utilizando Azure OpenAI. Configurarás una extensión personalizada y verificarás su funcionamiento con datos reales de clientes.

## Requisitos Previos

Antes de comenzar este laboratorio, es **imprescindible** haber completado el Lab02 y tener:

- ✅ El [Lab02](https://github.com/RCORELLA/AprendeBusinessCentralWorkshopsPublic/blob/main/lab_02_deploy_openAI.md) completamente funcional
- ✅ Azure OpenAI desplegado con los datos de conexión necesarios
- ✅ Acceso a un entorno de Business Central donde puedas instalar extensiones

## Paso 1: Descargar la Extensión

Descarga el archivo de extensión desde el repositorio:

📦 [Roberto Corella - Aprende Business Central_LAB00 - Testing AI Foundry_1.0.0.0.app](https://github.com/RCORELLA/AprendeBusinessCentralWorkshopsPublic/blob/main/Roberto%20Corella%20-%20Aprende%20Business%20Central_LAB00%20-%20Testing%20AI%20Foundry_1.0.0.0.app)

> **Nota:** Asegúrate de guardar el archivo .app en una ubicación accesible de tu equipo.

## Paso 2: Instalar la Extensión en Business Central

1. Accede a tu entorno de **Business Central**
2. Busca la página **Administración de extensiones** (Extension Management)
3. Haz clic en **Cargar extensión** (Upload Extension)
4. Selecciona el archivo `.app` descargado en el paso anterior
5. Espera a que el proceso de instalación finalice
6. Verifica que la extensión aparece como **Instalada** en la lista

## Paso 3: Configurar ABC AI Setup

Una vez instalada la extensión, necesitas configurar los parámetros de conexión con Azure OpenAI:

1. Busca y abre la página **ABC AI Setup**
2. Completa los siguientes campos con la información del Lab02:
   - **Endpoint**: URL de tu servicio Azure OpenAI
   - **API Key**: Clave de acceso al servicio
   - **Deployment Name**: Nombre del modelo desplegado (ej: gpt-4, gpt-35-turbo)
   - Cualquier otro parámetro específico de configuración

<img width="1870" height="495" alt="image" src="https://github.com/user-attachments/assets/31b28915-75f1-45c3-a9a2-dc51dc947ba9" />



> ⚠️ **Importante:** Asegúrate de que todos los datos coinciden exactamente con los de tu despliegue de Azure OpenAI del Lab02.

## Paso 4: Probar la Funcionalidad

Ahora es el momento de verificar que todo funciona correctamente:

1. Ve a la **lista de clientes** (Customers)
2. Abre la **ficha de cualquier cliente** (Customer Card)
3. Localiza el botón de **Copilot** llamado **ABC Ask me Anything**
   <img width="782" height="403" alt="image" src="https://github.com/user-attachments/assets/50b0e0a5-e860-4ca2-b9ab-7ae02c4ee2fb" />

5. Haz clic en el botón
6. Realiza una consulta de prueba, por ejemplo:
   - "¿Cómo puedo hacer una factura en Business Central?"
   - "Me explicas las dimensiones de Business Central"


## Verificación de Éxito

✅ Si todo está configurado correctamente, deberías:
- Ver el panel de Copilot abrirse al hacer clic en el botón
- Recibir respuestas coherentes basadas en Business Central
- No ver mensajes de error de conexión

## Troubleshooting

Si encuentras problemas:

| Problema | Solución |
|----------|----------|
| Error de conexión | Verifica que el Endpoint y API Key en ABC AI Setup sean correctos |
| El botón no aparece | Confirma que la extensión está instalada y activada |
| Respuestas incoherentes | Verifica el Deployment Name del modelo en la configuración |
| Error de permisos | Asegúrate de tener permisos para usar la extensión |

## Recursos Adicionales

- [Repositorio completo del workshop](https://github.com/RCORELLA/AprendeBusinessCentralWorkshopsPublic)
- [Lab02 - Deploy OpenAI](https://github.com/RCORELLA/AprendeBusinessCentralWorkshopsPublic/blob/main/lab_02_deploy_openAI.md)

## Conclusión

¡Felicidades! Has integrado exitosamente capacidades de IA en Business Central. Esta configuración te permite explorar cómo la inteligencia artificial puede mejorar la experiencia del usuario y proporcionar insights basados en datos empresariales.

---

**Siguiente paso:** Experimenta con diferentes tipos de consultas y explora las posibilidades de la IA en otros módulos de Business Central.


