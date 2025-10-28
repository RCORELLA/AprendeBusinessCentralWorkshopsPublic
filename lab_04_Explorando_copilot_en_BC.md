# Lab 04 - Usos de Copilot en Business Central

## Objetivo
En este laboratorio explorarás las diferentes funcionalidades de Copilot integradas nativamente en Business Central. Aprenderás a utilizar análisis de datos, chat conversacional, generación de configuraciones y automatización de tareas mediante prompts en lenguaje natural.

## Requisitos Previos

- ✅ Tener acceso a Business Central con Copilot habilitado
- ✅ Datos de demostración o datos reales en el sistema
- ✅ Familiaridad básica con la navegación en Business Central

## Caso de Uso 1: Análisis de Vistas con Copilot

Copilot puede ayudarte a crear análisis personalizados de datos directamente desde las listas de Business Central.

### Ejercicio 1.1: Análisis de Salidas de Productos

**Objetivo:** Visualizar las salidas de productos agrupadas por mes y producto.

**Pasos:**
1. Ve a la página **Item Ledger Entries** (Movimientos de productos)
2. Haz clic en el botón **Analyze** (Analizar) en la cinta de opciones
3. Activa **Copilot** en el panel de análisis
4. Introduce el siguiente prompt:
```
Mostrar las salidas de productos por mes y agrupadas por producto
```

**Resultado esperado:**
- Una tabla mostrando los productos en filas
- Meses en columnas
- Cantidades de salida como valores

### Ejercicio 1.2: Análisis de Clientes por País

**Objetivo:** Obtener una vista agrupada de clientes según su ubicación geográfica.

**Pasos:**
1. Ve a la página **Customers** (Clientes)
2. Haz clic en **Analyze** (Analizar)
3. Activa **Copilot**
4. Introduce el siguiente prompt:
```
Mostrar los clientes agrupados por país, usando la información maestra de clientes
```

**Resultado esperado:**
- Agrupación de clientes por país
- Conteo de clientes por región
- Posibilidad de ver información adicional como saldo total por país

## Caso de Uso 2: Chat Conversacional con Copilot

El chat de Copilot permite realizar consultas en lenguaje natural sobre los datos de tu empresa.

### Ejercicio 2.1: Consultar Facturas de un Cliente Específico

**Pasos:**
1. Abre el **Chat de Copilot** desde cualquier página (icono de Copilot en la esquina superior)
2. Introduce el siguiente prompt en inglés:
```
Could you give me last 3 invoices from Adatum Corporation?
```

**Resultado esperado:**
- Lista de las 3 últimas facturas del cliente Adatum Corporation
- Información relevante: número de factura, fecha, importe
- Enlaces directos a las facturas para acceder rápidamente

### Ejercicio 2.2: Filtrar Clientes por Saldo

**Pasos:**
1. En el **Chat de Copilot**, introduce el siguiente prompt en español:
```
me puedes mostrar los clientes con un saldo mayor que 500
```

**Resultado esperado:**
- Lista de clientes filtrados con saldo > 500
- Información del saldo actual de cada cliente
- Opción para abrir la ficha de cliente directamente

> 💡 **Tip:** Copilot entiende tanto inglés como español. Puedes alternar entre idiomas según tu preferencia.

## Caso de Uso 3: Generación de Configuraciones

Copilot puede ayudarte a crear configuraciones complejas mediante instrucciones simples.

### Ejercicio 3.1: Crear Series Numéricas para Pedidos de Venta

**Objetivo:** Generar automáticamente una configuración de numeración para documentos de venta.

**Pasos:**
1. Ve a la página **No. Series** (Series numéricas)
2. Activa **Copilot** (si está disponible en la página) o usa el chat
3. Introduce el siguiente prompt:
```
Create number series for sales orders
```

**Resultado esperado:**
- Copilot sugiere una nueva serie numérica
- Propone un código (ej: SO-ORD)
- Define rangos de numeración lógicos
- Configura incrementos automáticos

**Acciones:**
- Revisa la propuesta de Copilot
- Ajusta si es necesario
- Acepta y guarda la configuración

## Caso de Uso 4: Automatización de Documentos

Una de las funcionalidades más potentes: replicar documentos anteriores automáticamente.

### Ejercicio 4.1: Repetir un Pedido Anterior

**Objetivo:** Crear un nuevo pedido de venta basado en uno del mes pasado.

**Pasos:**
1. Abre un **Sales Order** (Pedido de venta) nuevo
2. En el campo del cliente, selecciona el cliente deseado
3. Activa **Copilot** en el documento (botón en la cinta de opciones)
4. Introduce el siguiente prompt:
```
Repíteme el mismo pedido que el mes pasado
```

**Resultado esperado:**
- Copilot busca pedidos anteriores del cliente
- Identifica el pedido del mes pasado
- Copia las líneas del pedido automáticamente
- Ajusta fechas al contexto actual

**Acciones siguientes:**
- Revisa las líneas copiadas
- Modifica cantidades o productos si es necesario
- Confirma y procesa el pedido

> ⚠️ **Importante:** Siempre verifica que los datos copiados sean correctos antes de procesar documentos.

## Mejores Prácticas

### Para Análisis de Datos
- ✅ Sé específico con las agrupaciones que deseas
- ✅ Menciona el período de tiempo si es relevante


### Para Chat Conversacional
- ✅ Utiliza frases completas y claras
- ✅ Especifica nombres exactos de clientes o productos
- ✅ Incluye criterios numéricos concretos (ej: "mayor que 500")

### Para Automatización
- ✅ Verifica siempre los datos generados automáticamente
- ✅ Ajusta configuraciones según tus necesidades específicas


## Casos de Uso Adicionales para Explorar

Una vez domines los ejercicios anteriores, prueba estos prompts:

**Análisis:**
- "Muestra las ventas por vendedor del último trimestre"
- "Agrupa los productos por categoría y muestra el stock actual"

**Chat:**
- "¿Cuáles son los 5 productos más vendidos este mes?"
- "Muéstrame los pedidos pendientes de servir"

**Automatización:**
- "Crea una oferta basada en la última oferta de este cliente"
- "Genera series numéricas para albaranes de compra"

## Troubleshooting

| Problema | Solución |
|----------|----------|
| Copilot no aparece | Verifica que tu licencia incluye Copilot y está habilitado en la configuración |
| Respuestas no precisas | Reformula el prompt siendo más específico |
| No encuentra datos históricos | Asegúrate de que existen datos del período mencionado |
| Error al crear configuraciones | Verifica que tienes permisos de administrador |

## Recursos Adicionales

- [Documentación oficial de Copilot en Business Central](https://learn.microsoft.com/dynamics365/business-central/copilot-overview)
- [Repositorio del workshop](https://github.com/RCORELLA/AprendeBusinessCentralWorkshopsPublic)

## Conclusión

¡Felicidades! Has explorado las principales funcionalidades de Copilot en Business Central. Esta herramienta puede aumentar significativamente tu productividad al:
- Simplificar análisis complejos de datos
- Responder preguntas en lenguaje natural
- Automatizar tareas repetitivas
- Acelerar configuraciones del sistema

---

**Siguiente paso:** Experimenta con tus propios prompts y descubre nuevas formas de aprovechar Copilot en tu trabajo diario con Business Central.


*Instructor: Roberto Corella*  
*LinkedIn: https://www.linkedin.com/in/robertocorella/*

*Fecha: Octubre 2025*
