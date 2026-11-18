# mg-lora-rag

Experimento de **ajuste fino eficiente (LoRA)** sobre un modelo de lenguaje pequeño, con una tarea de preguntas y respuestas (QA) y un análisis de cómo cambia el comportamiento tras el ajuste.

> Proyecto de la asignatura Práctica 2 (LoRA y RAG). El enunciado completo está en [`Practica_2_LoRAyRAG.pdf`](Practica_2_LoRAyRAG.pdf).

## Objetivo
Aprender y aplicar PEFT con LoRA: entrenar un pequeño conjunto de matrices adaptadoras en lugar de todos los pesos del modelo, y evaluar el resultado.

## Contenido
- `notebooks/4.2a_fine_tuning_lora.ipynb`: notebook principal con preparación del dataset, tokenización, configuración de LoRA (`r`, `lora_alpha`, `target_modules`), entrenamiento y evaluación.

## Configuración actual del notebook
| Elemento | Valor |
|---|---|
| Modelo base | `deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B` |
| Dataset de entrenamiento | `yunfan-y/trump-qa` (Hugging Face) |
| Método | LoRA mediante la librería `peft` |
| Épocas | 10 |

## Requisitos
- Python 3.8 o superior.
- Paquetes: `transformers`, `datasets`, `peft`, `evaluate`, `torch`.
- GPU recomendada. El notebook fuerza el uso de una sola GPU para evitar errores de NCCL con varias GPU.

## Estado y puntos pendientes
Este repositorio está en fase de experimentación. Antes de considerar los resultados fiables hay que resolver lo siguiente:

- **Descripción inconsistente:** el texto del notebook menciona el dataset IMDB de sentimiento, pero el código carga `yunfan-y/trump-qa`. La tarea real es QA, no clasificación.
- **Modelos mencionados:** en el código aparece una alternativa comentada (`google/gemma-3-1b-it`). El README original mencionaba Gemma 3 4B y Llama 3.2 3B, que no coinciden con la configuración actual.
- **Métricas:** para modelos generativos, `accuracy` no aplica directamente. Conviene usar perplejidad y una métrica de QA (por ejemplo, exact match o F1 sobre respuestas de referencia).
- **Resultados:** no hay resultados publicados todavía. Pendiente: comparar el modelo base y el modelo ajustado sobre el mismo conjunto de prueba.

## Cómo reproducir
1. Instalar las dependencias.
2. Abrir el notebook y ejecutar las celdas en orden.
3. Ajustar `MODEL_NAME` y el dataset si se quiere repetir el experimento con otro modelo.

## Licencia
MIT
