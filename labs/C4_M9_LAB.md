**C4_M9_LAB**

**TÍTULO DEL LABORATORIO:** Construyendo un Agente Multi-Paso con Mastra

**MÓDULO:** 9. Mastra y Desarrollo con LLM

**CURSO:** 4. Ingeniería de Software con IA

**OBJETIVO:**
Implementar un Agente en Mastra que sea capaz de realizar una tarea de múltiples pasos: recibir una consulta de usuario, buscar información relevante (simulada) y generar una respuesta final basada en esa información, utilizando la estructura de `Agent` y `Tool` de Mastra.

**REQUISITOS PREVIOS:**
*   Node.js 18+ instalado.
*   Conocimientos básicos de TypeScript.
*   API Key de OpenAI.

**DURACIÓN ESTIMADA:** 60 minutos

---

### PASO 1: Inicialización del Proyecto

1.  Crea un nuevo directorio para tu proyecto: `mkdir mastra-lab && cd mastra-lab`.
2.  Inicializa un proyecto TypeScript básico (o usa `npx create-mastra@latest` si prefieres la estructura completa, pero para este lab haremos algo minimalista).
    ```bash
    npm init -y
    npm install @mastra/core zod openai dotenv typescript tsx
    npx tsc --init
    ```

### PASO 2: Definición de la Herramienta (`tools.ts`)

Crea un archivo `tools.ts`. Vamos a simular una herramienta de búsqueda de productos.

```typescript
import { createTool } from "@mastra/core";
import { z } from "zod";

// Base de datos simulada
const PRODUCTS = [
  { id: "1", name: "Laptop Pro", price: 1200, stock: 5 },
  { id: "2", name: "Smartphone X", price: 800, stock: 0 },
  { id: "3", name: "Headphones", price: 150, stock: 20 },
];

export const productSearchTool = createTool({
  id: "search-products",
  description: "Busca productos en el inventario por nombre",
  schema: z.object({
    query: z.string().describe("El nombre del producto a buscar"),
  }),
  execute: async ({ context }) => {
    const query = context.query.toLowerCase();
    const results = PRODUCTS.filter((p) => 
      p.name.toLowerCase().includes(query)
    );
    return results;
  },
});
```

### PASO 3: Creación del Agente (`agent.ts`)

Crea un archivo `agent.ts`. Importa tu herramienta y configura el agente.

```typescript
import { Agent } from "@mastra/core";
import { productSearchTool } from "./tools";
import * as dotenv from "dotenv";

dotenv.config();

export const salesAgent = new Agent({
  name: "Sales Assistant",
  instructions: `
    Eres un asistente de ventas útil. 
    Tu objetivo es ayudar a los clientes a encontrar productos y verificar su precio y stock.
    Si un producto no tiene stock, sugiere buscar otro o informa amablemente.
    Usa la herramienta 'search-products' para obtener información real.
  `,
  model: {
    provider: "openai",
    name: "gpt-4o-mini", // O gpt-3.5-turbo
  },
  tools: {
    productSearchTool,
  },
});
```

### PASO 4: Ejecución (`index.ts`)

Crea el archivo principal para interactuar con el agente.

```typescript
import { salesAgent } from "./agent";

async function main() {
  const query = "Hola, ¿tienen el Smartphone X y cuánto cuesta?";
  console.log(`Usuario: ${query}`);

  const response = await salesAgent.generate(query);

  console.log("\nAgente:");
  console.log(response.text);
}

main().catch(console.error);
```

### PASO 5: Prueba y Refinamiento

1.  Ejecuta el código: `npx tsx index.ts`.
2.  Observa cómo el agente decide llamar a la herramienta (internamente) y usa el resultado (precio 800, stock 0) para responderte.
3.  Prueba con otra consulta: "¿Qué laptops tienen?".

### ENTREGABLE

Un archivo `.zip` con tu código fuente (`tools.ts`, `agent.ts`, `index.ts`, `package.json`) y una captura de pantalla de la terminal mostrando la interacción donde el agente informa correctamente sobre el stock del producto.
