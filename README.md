# Horizonte Senior · Antioquia_26

**¿Quién necesita acompañamiento Senior para adoptar IA de forma segura? Radiografía de Antioquia con ENTIC Hogares 2024**

Proyecto final individual del programa **Horizonte Senior** (Ruta N), profesor Daniel Román Ramírez.
Autor: José I. Agudelo Vélez.

## Contexto

Un grupo de personas de 45 a 75 años aprende analítica de datos para convertir datos crudos y experiencia de vida en conocimiento estratégico. La pregunta de partida es: *si yo soy parte de este grupo, ¿por dónde empiezo?* El proyecto usa datos de personas (no de empresas) para decidir a quién debería asesorar primero una célula Senior en el uso seguro de la inteligencia artificial.

## Las tres preguntas

1. ¿Una persona con poca madurez digital usa IA? ¿Influye su contexto regional (municipio y zona) para que use IA?
2. ¿Qué proporción de las personas que usan IA en Antioquia tiene pocas prácticas de ciberseguridad (riesgo crítico) y qué incidentes digitales reportan?
3. ¿Se puede identificar quién necesita asesoría en IA: quienes la usan con riesgo crítico y quienes no la usan por falta de capacidades?

## Datos

- **Fuente:** Encuesta de Tecnologías de la Información y las Comunicaciones en Hogares (ENTIC Hogares) 2024, DANE.
- **Alcance:** 148.700 personas en 53.343 hogares; 78.259 adultos con internet en el país; **5.219 adultos con internet en Antioquia**. Se usan solo adultos (18 años o más).
- **Datos limpios del proyecto:** `salida/dataset_modelo_antioquia.csv` (5.219 filas, 407 columnas; el factor de expansión es `fex`).
- **Base original:** no se incluye por su tamaño (110 MB). Se descarga del catálogo de microdatos del DANE y se guarda como `BD_in/BASE DEFINITIVA ENTIC HOGARES 2024.csv`.

## Hallazgos principales

Las cifras son ponderadas con el factor de expansión, salvo que se indique otra cosa.

| Tema | Resultado |
|---|---|
| Uso de IA en Antioquia | 16,2 % de los adultos con internet (nacional 17,8 %) |
| Brecha de edad | 7,3 % entre 45 y 64 años frente a 22,3 % entre 18 y 44 años |
| Zona | Cabecera 17,6 %, centro poblado 7,8 %, rural disperso 8,3 % |
| Riesgo crítico | 29,2 % de quienes usan IA tiene 5 o menos de 11 prácticas de protección (una regla, no un modelo) |
| Incidentes digitales | 25,4 % de quienes usan IA los reporta, frente a 10,6 % de quienes no la usan |
| Barrera de capacidades | 54,7 % de quienes no usan IA dice que no sabe qué es o no sabe usarla |

Conclusión para una célula Senior: el acompañamiento debe ser **individual y no solo territorial**. La madurez digital de la persona pesa más que su municipio.

## Modelos y métricas

Se comparan regresión logística, árbol de decisión (profundidad 4) y Random Forest contra un modelo de referencia (*Dummy*). Como medida de calidad se usa el **Índice C (AUC)**: 0,5 equivale a lanzar una moneda y 1 es separar perfectamente.

- **Pregunta 1 (¿quién usa IA?):** solo con perfil y hogar, Índice C 0,84; al sumar la madurez digital propia, 0,91. La brecha frente al municipio no agrega capacidad de predicción.
- **Pregunta 3 (barrera de capacidades):** Índice C cercano a 0,80 con perfil, habilidades y usos.
- **Pregunta 3 (riesgo crítico):** resultado moderado (Índice C 0,73 en una prueba 80/20 con 129 personas; 0,78 en validación cruzada). Sirve para priorizar, no para afirmar que una persona concreta está en riesgo.

## Limitaciones

- Es una **asociación, no una causa**: usar IA es en sí una señal de madurez digital.
- ENTIC está diseñada para resultados nacionales y departamentales; las cifras por municipio tienen muestras pequeñas y solo sirven para priorizar dónde mirar.
- El «riesgo crítico» es una regla de exposición. En los datos, el índice de protección no predice incidentes (quienes protegen más reportan más; una explicación posible es la causalidad inversa).
- El interés en capacitación (63,4 % entre quienes tienen la barrera de capacidades, n = 247) solo se pregunta a quienes conocen programas públicos de formación digital.
- Las cifras para empresas citadas en la presentación (ILIA 2026, CEPAL) son estimaciones de modelo, no datos de una encuesta.

## Contenido del repositorio

```
Proyecto_Final_Senior_JoseAgudelo.ipynb   Cuaderno documentado de principio a fin (carga, EDA, limpieza, modelos)
Tablero_JoseAgudelo_v5.pbix               Tablero de Power BI de 4 páginas (requiere Power BI Desktop)
Presentacion_Proyecto_Final_Senior_JIAV_V64.pptx     Presentación académica
Presentacion_Proyecto_Final_Senior_JIAV_V7_QRv.pptx   Presentación narrativa (data storytelling)
salida/dataset_modelo_antioquia.csv       Datos limpios que alimentan el cuaderno y el tablero
salida/*.csv                              Tablas de resultados (segmentos, municipios, métricas)
salida/..._ejecutado.ipynb                Copia del cuaderno que el propio cuaderno guarda al terminar la corrida
salida/graficos/                          Gráficos G1 a G9 y EDA en PNG
BD_in/                                    Cuestionario y metodología ENTIC, DIVIPOLA (la base original se descarga aparte)
```

## Cómo reproducirlo

1. Abre el cuaderno en Google Colab, o en Jupyter con Python 3 y las librerías `pandas`, `numpy`, `matplotlib` y `scikit-learn`.
2. Coloca la base original del DANE en `BD_in/` (junto con `divipola.csv`).
3. Ejecuta las celdas en orden. Las salidas se guardan en `salida/`, incluida una copia ejecutada del cuaderno.
4. Abre `Tablero_JoseAgudelo_v5.pbix` con Power BI Desktop; los datos están incluidos en el archivo.

## Licencia y uso

Trabajo académico. Los datos de ENTIC Hogares 2024 pertenecen al DANE y se usan con fines educativos; cita la fuente al reutilizarlos.
