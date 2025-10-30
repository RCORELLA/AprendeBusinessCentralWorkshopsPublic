flowchart TD
    A[1. Registrar la capacidad en Copilot] --> B[2. Poner los parámetros]
    B --> C[3. Rellenar la autorización]
    C --> C1[Endpoint]
    C --> C2[Deployment]
    C --> C3[API Key]
    C1 --> D
    C2 --> D
    C3 --> D
    D[4. Indicar a OpenAI que capacidad vamos a usar] --> E[5. Añadir el System Prompt]
    E --> F[6. Añadir el User Prompt]
    F --> G[7. Hacer la llamada a GPT]
    G --> H[8. Recoger el prompt de respuesta]
    
    style A fill:#e1f5ff
    style B fill:#e1f5ff
    style C fill:#fff4e1
    style D fill:#e1f5ff
    style E fill:#f0e1ff
    style F fill:#f0e1ff
    style G fill:#e1ffe1
    style H fill:#ffe1e1
