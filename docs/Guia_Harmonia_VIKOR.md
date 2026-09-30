# Harmonía VIKOR

Guía de instalación, uso y documentación técnica de la aplicación `index.html` para aplicar el método VIKOR de solución de compromiso multicriterio. Versión 1.0.

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Sugerencias o dudas: mgomezr1@gmail.com

## 1. Descripción general

`index.html` es una aplicación web de un solo archivo construida con HTML5, CSS3 y JavaScript. Todos los cálculos ocurren en el navegador y los datos nunca salen del equipo del usuario. La única dependencia externa es SheetJS (`https://cdn.sheetjs.com/xlsx-0.20.3/package/dist/xlsx.full.min.js`), que se usa solo para generar el libro Excel. El informe PDF se genera con código propio y no necesita librerías ni conexión.

El número de criterios (n) y de alternativas (m) lo define el usuario. Tablas, gráficos, hojas de Excel y páginas del PDF se construyen con ciclos a partir de n y m.

Configuración del método:

| Elemento | Opción implementada |
|---|---|
| Valores de referencia | Mejor valor f* y peor valor f⁻ observados en cada criterio, según su sentido |
| Sentido de cada criterio | Beneficio (más es mejor) o Costo (menos es mejor) |
| Pesos | Digitados por el usuario (deben sumar 1; hay botón para normalizar) o calculados por entropía de Shannon |
| Peso de la estrategia de la mayoría | v entre 0 y 1, con 0,5 como valor de consenso |
| Umbral de ventaja | DQ = 1/(m − 1) |
| Resultado | Solución de compromiso única o conjunto de compromiso, según las condiciones C1 y C2 |
| Robustez | Sensibilidad exacta a v, sensibilidad al peso de un criterio y dominancia |

La aplicación distingue dos orígenes de datos, visibles en la portada, en los resultados, en el Excel y en el PDF: «Datos digitados por el usuario» y «Datos de prueba generados por la aplicación». Los archivos exportados con datos de prueba llevan el prefijo `PRUEBA_`.

El nombre, la versión, el autor, el correo y la nota de uso están en una sola constante (`APLICATIVO`, al inicio del JavaScript). Si se cambian allí, se actualizan la interfaz, la cita, el Excel y el PDF.

**El nombre.** ἁρμονία (harmonía) significa en griego el ajuste entre partes que tiran en direcciones distintas, como las piezas de un carpintero o las cuerdas de una lira. Es lo que hace VIKOR: ajustar la utilidad de grupo y el arrepentimiento individual. Mantiene la línea de nombres griegos del portafolio (Kairós AHP, Áristos ELECTRE, Éngista TOPSIS, Axía MAUT, Prónoia PROMETHEE, Métron, Kíndynos VaR, Seismos).

## 2. Cómo guardar el archivo

1. Descargue `index.html`.
2. Guárdelo en una carpeta de su equipo, por ejemplo `Documentos/Harmonia_VIKOR/`.
3. Conserve la extensión `.html`. Si lo edita, use un editor de texto plano y guarde con codificación UTF 8.

## 3. Cómo ejecutarlo

1. Haga doble clic en `index.html` o arrástrelo a una ventana de Chrome, Edge, Firefox o Safari recientes. También funciona publicado en GitHub Pages.
2. Para exportar a Excel se necesita conexión a internet la primera vez, porque el navegador descarga SheetJS. Sin conexión funcionan la configuración, los cálculos, la sensibilidad, la verificación y el informe PDF.
3. No requiere instalar nada ni ejecutar un servidor.

Uso sin conexión (opcional): descargue una vez `xlsx.full.min.js` de la dirección anterior, guárdelo junto a `index.html` y cambie la etiqueta del encabezado por `<script src="xlsx.full.min.js"></script>`.

## 4. Estructura de la interfaz

| Sección | Contenido |
|---|---|
| Riel lateral | Nombre, siete pasos y «Acerca de Harmonía», con un punto verde cuando el paso está listo o naranja cuando requiere atención. En tabletas y teléfonos se convierte en barra superior |
| Portada | Nombre, lema, origen de los datos, botón «Limpiar aplicación» y la balanza interactiva |
| Cómo funciona VIKOR | Cuatro pasos, diagrama del flujo desde la matriz hasta Q y los supuestos del método |
| 1. Configuración | Objetivo, número de criterios y de alternativas, y nombres de las alternativas |
| 2. Criterios, sentido y pesos | Selector del método de pesos (digitados o entropía) y tabla con nombre, unidad, sentido y peso; suma en vivo; botón para normalizar |
| 3. Matriz de decisión | Valores en unidad original; cada celda se tiñe de lavanda según su lejanía al mejor valor del criterio |
| 4. Estrategia v | Deslizador, campo para el valor exacto, botones 0,25, 0,50 y 0,75 y una lectura en palabras del valor elegido; botón «Calcular resultados» |
| 5. Resultados | Solución de compromiso y nueve bloques: configuración, criterios e ideales, matriz, lejanías, S R y Q, mapa de las dos fuerzas, clasificaciones, condiciones de aceptación y robustez |
| 6. Sensibilidad | Recorrido de v de 0 a 1 o del peso de un criterio, intervalos con la solución de cada tramo, cambio más cercano y gráfico interactivo |
| 7. Exportación | Excel y PDF |
| Acerca de Harmonía | El nombre, versión y autoría; validación con botón «Ejecutar verificación», estado y desplegables «Ver pruebas técnicas» y «Escenarios de prueba»; debajo, «Referencias» y «Cómo citar» |

### Balanza de la portada

Tres proyectos con utilidad de grupo y arrepentimiento ya reescalados: Equilibrio (S' = 0,35; R' = 0,30), Estrella (S' = 0; R' = 1), el mejor en el conjunto pero con una falla grave, y Prudente (S' = 1; R' = 0), sin fallas graves pero flojo en el conjunto. Al mover v la balanza se inclina hacia la mayoría o hacia el veto y las barras muestran Q = v·S' + (1 − v)·R'. Con v bajo gana Prudente, con v alto gana Estrella y entre 0,316 y 0,667 gana Equilibrio, que es la idea de compromiso. Se maneja con ratón, dedo o flechas del teclado y no afecta los datos del modelo.

### Identidad visual

Modo oscuro sobre un vino profundo, sin bordes visibles: las superficies se separan por contraste de tono y sombras suaves. El par de colores tiene significado: **menta** es la utilidad de grupo S (la mayoría) y **lavanda** el arrepentimiento individual R (el veto). El **oro** marca la solución de compromiso. La lavanda también tiñe la matriz de decisión y la de lejanías, porque ambas muestran qué tan lejos está cada valor del ideal. Toda la paleta y las medidas están en variables de `:root`. No se enlaza ninguna fuente externa; el bloque `@font-face` comentado permite cargar fuentes propias desde una carpeta `fuentes`.

### Validación restaurable

«Ejecutar verificación» corre las pruebas con escenarios internos. Antes de empezar guarda una instantánea de la pantalla (formulario, criterios, matriz, v, resultados y sensibilidad) y al terminar la restaura, de modo que el usuario encuentra su trabajo como lo dejó.

## 5. Exportación a Excel

| Hoja | Contenido |
|---|---|
| `Menu` | Datos del análisis, solución de compromiso, índice con enlace a cada hoja, software, autor, contacto, nota de uso y advertencia si los datos son de prueba |
| `Datos` | Criterios, unidades, sentido, pesos con su suma y matriz de decisión |
| `Entropia` | Solo si los pesos se calculan por entropía: sumas, proporciones, términos p × LN(p), k, entropía, diversidad y pesos |
| `Lejania` | Mejor y peor valor de cada criterio y lejanía normalizada de cada alternativa |
| `SyR` | Lejanías ponderadas, S y R |
| `Q` | v editable, extremos de S y R, valores reescalados, Q y puestos por S, R y Q |
| `Resultado` | Clasificación, condiciones C1 y C2, solución de compromiso, sensibilidad a v y estabilidad frente a los pesos |

Fórmulas reales en cada paso:

| Cálculo | Fórmula en Excel |
|---|---|
| Mejor y peor valor | `MAX` y `MIN` de la columna en `Datos`, invertidos si el criterio es de costo |
| Lejanía | `=IF(rango=0,0,(f*−f)/rango)` |
| Proporción de entropía | `=x/SUM(columna)` |
| Término de entropía | `=IF(p>0,p*LN(p),0)` |
| Entropía y peso | `=−k*SUM(términos)`, `=1−E` y `=diversidad/SUM(diversidades)` |
| Lejanía ponderada | `=w*d` |
| S y R | `=SUM(fila)` y `=MAX(fila)` |
| S' y R' | `=IF(S⁻−S*<=1E−9,0,(S−S*)/(S⁻−S*))` y la análoga para R |
| Q | `=v*S'+(1−v)*R'` |
| Puestos | `=RANK(valor,rango,1)` |
| Primera y segunda por Q | `=SMALL(rango de Q,1)`, `=SMALL(rango de Q,2)` y `=INDEX(nombres,MATCH(...))` |
| C1 | `=IF(ventaja>=DQ,"Se cumple","No se cumple")` con `DQ = 1/(m−1)` |
| C2 | `=IF(OR(S de a1<=S*,R de a1<=R*),"Se cumple","No se cumple")` |

Si el estudiante cambia v en la celda `B4` de la hoja `Q`, se recalculan Q, los puestos, la primera y la segunda por Q y las condiciones C1 y C2. La tabla de clasificación y el texto del conjunto de compromiso de la hoja `Resultado` quedan con el orden del v original, y así lo indican sus títulos. Las fórmulas guardan también su valor.

## 6. Informe ejecutivo en PDF

Documento tamaño carta con:

1. **Objetivo y recomendación:** solución o conjunto de compromiso, Q de la primera, primera y segunda por Q, mejor por S y por R, intervalo de v que conserva el resultado, menor cambio de peso que lo altera y dominancia.
2. **Clasificación:** S, R, Q y puestos, con barras.
3. **Criterios, pesos y valores de referencia.**
4. **Condiciones de aceptación** C1 y C2 con sus valores.
5. **Robustez:** gráfico de Q frente a v, tabla de intervalos de v y estabilidad frente al peso de cada criterio.
6. **Nota metodológica, referencias y recuadro de autoría.**

Cada página lleva pie con «Harmonía VIKOR versión 1.0 | Desarrollado por Mario Sergio Gómez Rueda | Uso académico | mgomezr1@gmail.com», la frase de propiedad intelectual y «Página x de n», y una marca de agua diagonal translúcida «USO ACADÉMICO».

## 7. Fundamento de cálculo

**Valores de referencia.** Para cada criterio j, f*ⱼ es el mejor valor observado y f⁻ⱼ el peor. En un criterio de beneficio f*ⱼ = máximo y f⁻ⱼ = mínimo; en uno de costo, al revés.

**Lejanía normalizada.** dᵢⱼ = (f*ⱼ − fᵢⱼ) / (f*ⱼ − f⁻ⱼ). Vale 0 en el mejor valor y 1 en el peor. Si f*ⱼ = f⁻ⱼ el criterio no discrimina: dᵢⱼ = 0 para todas las alternativas y se advierte.

**Utilidad de grupo y arrepentimiento individual.** Sᵢ = Σⱼ wⱼ dᵢⱼ y Rᵢ = máxⱼ wⱼ dᵢⱼ. Corresponden a las métricas L₁ y L∞ de la familia de soluciones de compromiso de Yu (1973). En ambas, menos es mejor, y siempre Rᵢ ≤ Sᵢ.

**Índice de compromiso.** Qᵢ = v (Sᵢ − S*) / (S⁻ − S*) + (1 − v) (Rᵢ − R*) / (R⁻ − R*), con S* = mín S, S⁻ = máx S, R* = mín R y R⁻ = máx R. Si S⁻ = S* (o R⁻ = R*) ese término vale 0 para todas y se advierte.

**Clasificaciones.** Se ordena de menor a mayor por S, por R y por Q. Diferencias menores que 10⁻⁹ se consideran empate y comparten puesto; a igualdad se respeta el orden de registro.

**Condiciones de aceptación** (Opricovic y Tzeng, 2004). Sean a1 y a2 la primera y la segunda por Q.

- C1, ventaja aceptable: Q(a2) − Q(a1) ≥ DQ, con DQ = 1/(m − 1).
- C2, estabilidad aceptable: a1 también es la mejor por S o por R.

**Solución de compromiso.** Si se cumplen C1 y C2, a1. Si solo falla C2, a1 y a2. Si falla C1, a1, a2, …, a(M), donde M es el mayor puesto tal que Q(a(M)) − Q(a1) < DQ.

**Pesos digitados.** No negativos, al menos uno positivo y |Σw − 1| ≤ 0,0001; se usan divididos por su suma. Un peso cero se advierte.

**Pesos por entropía** (Hwang y Yoon, 1981). pᵢⱼ = xᵢⱼ / Σᵢ xᵢⱼ; Eⱼ = −(1 / ln m) Σᵢ pᵢⱼ ln pᵢⱼ, con 0 · ln 0 = 0; diversidad dvⱼ = 1 − Eⱼ; wⱼ = dvⱼ / Σ dv. Exige valores no negativos y columnas con suma positiva. El sentido del criterio no interviene. Si ningún criterio discrimina, la aplicación pide digitar los pesos.

**Dominancia.** a domina a b si su lejanía es menor o igual en todos los criterios con peso positivo y menor en al menos uno.

**Sensibilidad a v (exacta).** Qᵢ(v) = v S'ᵢ + (1 − v) R'ᵢ es una recta en v. El orden y las condiciones solo cambian donde dos rectas se cruzan (Qᵢ = Qⱼ) o donde su distancia iguala DQ (Qᵢ − Qⱼ = ± DQ). La aplicación calcula todos esos puntos, evalúa el resultado en el centro de cada tramo y une los tramos contiguos con la misma solución.

**Sensibilidad al peso de un criterio.** Al fijar en x el peso del criterio c, los demás se ajustan como wⱼ (1 − x) / Σᵢ≠c wᵢ (reparto igual si todos eran 0). Las lejanías no cambian. Como R es un máximo y S y R se reescalan dentro del grupo, Q no es lineal en x: la aplicación recorre una malla de 401 puntos y ubica cada cambio por bisección hasta una precisión de 10⁻⁷. El resumen de estabilidad de los resultados usa una malla de 201 puntos con la misma bisección. Dos conjuntos con las mismas alternativas en distinto orden se consideran el mismo resultado.

## 8. Explicación de las funciones

| Función | Qué hace |
|---|---|
| `interpretarNumero`, `interpretarV`, `interpretarEntero` | Convierten texto en número (punto o coma decimal); rechazan separadores mezclados; v entre 0 y 1 |
| `validarPesos` | Suma, signos, ceros y vacíos de los pesos digitados |
| `calcularPesosEntropia` | Proporciones, entropía, diversidad y pesos, con sus validaciones |
| `calcularIdeales`, `calcularLejanias` | f*, f⁻ y lejanías normalizadas |
| `calcularSyR`, `calcularQ` | S, R, extremos, S', R' y Q |
| `ordenarAscendente` | Clasificación con empates que comparten puesto |
| `evaluarCondiciones` | DQ, C1, C2 y conjunto de compromiso |
| `calcularVikor` | Ejecuta el método completo y reúne advertencias y dominancia |
| `calcularDominancia`, `describirCompromiso`, `nombresConjunto` | Apoyo al análisis y a los textos |
| `sensibilidadV`, `ajustarPesos`, `evaluarConPesos`, `sensibilidadPeso`, `resumirEstabilidad` | Sensibilidad y robustez |
| `solicitarConfiguracion`, `renderizarTablaCriterios`, `actualizarSumaPesos`, `normalizarPesosInterfaz`, `cambiarMetodoPesos`, `confirmarConfiguracion` | Pasos 1 y 2 |
| `renderizarMatriz`, `actualizarTintesColumna`, `tinteLejania`, `leerMatrizNumerica` | Paso 3 |
| `establecerV`, `lecturaDeV`, `construirModeloDesdeEstado`, `calcularResultados` | Paso 4 y cálculo |
| `renderizarResultados`, `renderizarGraficoSR` | Resultados |
| `ejecutarSensibilidadDesdeInterfaz`, `renderizarSensibilidad`, `renderizarGraficoSensibilidad` | Paso 6 |
| `crearLibroResultados` y `crearHoja…` | Libro Excel |
| `DocumentoPDF`, `generarInformePDF`, `dibujarSensibilidadVPDF` | Informe PDF nativo |
| `ejecutarPruebas`, `tomarInstantanea`, `restaurarInstantanea`, `cargarEscenarioPrueba` | Verificación y escenarios |
| `inicializarExplorador`, `inicializarRiel`, `aplicarDatosAplicativo` | Portada, navegación y datos del aplicativo |

## 9. Ejemplo verificado

Escenario «Prueba 2: selección de laboratorio clínico» (datos ficticios), con v = 0,5:

| Laboratorio | Costo por prueba (miles COP, costo) | Entrega (horas, costo) | Calidad (puntaje, beneficio) | Cobertura (pruebas, beneficio) |
|---|---|---|---|---|
| A | 42 | 24 | 88 | 180 |
| B | 38 | 36 | 80 | 150 |
| C | 50 | 12 | 92 | 210 |
| D | 45 | 20 | 85 | 160 |
| E | 36 | 48 | 75 | 140 |
| Peso | 0,35 | 0,25 | 0,25 | 0,15 |

Resultados de la aplicación, iguales a los de una implementación independiente en Python con NumPy (diferencias menores que 10⁻¹¹):

| Laboratorio | S | R | Q |
|---|---|---|---|
| A | 0,356443 | 0,150000 | 0,010738 |
| B | 0,521709 | 0,176471 | 0,352358 |
| C | 0,350000 | 0,350000 | 0,500000 |
| D | 0,490640 | 0,225000 | 0,421899 |
| E | 0,650000 | 0,250000 | 0,750000 |

DQ = 1/(5 − 1) = 0,25. La ventaja de A sobre B es 0,341620 ≥ 0,25 (C1 se cumple) y A es la mejor por R (C2 se cumple): **A es la solución de compromiso**. La solución se mantiene para v entre 0,2811 y 0,7342; con v menor el resultado es el conjunto {A, B} y con v mayor el conjunto {A, C}. El menor cambio de un peso que altera el resultado es 0,0541, en el costo por prueba (la solución se mantiene si ese peso está entre 0,237 y 0,404).

## 10. Pruebas automáticas

| # | Prueba | Qué verifica |
|---|---|---|
| 1 | Interpretación de números y de v | Punto, coma, signo, notación científica, vacíos, errores y rango de v |
| 2 | Pesos digitados | Suma, negativos, ceros, todos en cero |
| 3 | Entropía de Shannon | E(0,25; 0,75) = 0,811278; columna constante con peso 0; rechazo de negativos; pesos del escenario 3 contra Python |
| 4 | Lejanía normalizada | f* y f⁻ según el sentido; d en beneficio y costo; criterio constante |
| 5 | Solución analítica | Q = (1/6; 1; 5/12), S, R, DQ y conjunto {A, C} calculables a mano |
| 6 | Implementación independiente | S, R y Q del escenario 2 contra Python; solución única |
| 7 | Conjuntos de compromiso | Falla de C1 (escenario 3) y falla solo de C2 (escenario 4) |
| 8 | Extremos y casos degenerados | v = 0 y v = 1, S constante, alternativas idénticas, empates |
| 9 | Tamaños dinámicos | 66 modelos con n de 2 a 12 y m de 2 a 12, pesos de ambos tipos y v variable |
| 10 | Sensibilidad a v | Tramos contiguos de 0 a 1 y cada punto de cambio confirmado a ambos lados |
| 11 | Sensibilidad al peso | Pesos ajustados suman 1 y cada cambio se confirma a ± 0,000001 |
| 12 | Excel | Hojas, enlaces del menú, SUM, MAX, RANK, LN, referencias a Entropia y clasificación releída |
| 13 | PDF | xref, longitudes de flujo, pie, numeración y marca de agua en cada página |
| 14 | Formatos | Coma decimal, tintes de lejanía y conversión a WinAnsi |
| 15 | Interfaz | El escenario cargado en pantalla da el mismo resultado que el cálculo directo |

## 11. Verificación realizada antes de entregar

1. La aplicación se abrió en Chromium sin errores en la consola y las 15 pruebas quedaron aprobadas. En el entorno de verificación el dominio cdn.sheetjs.com no estaba disponible, por lo que SheetJS se sirvió desde una copia local de la versión 0.18.5 publicada en npm; las funciones que usa la aplicación son las mismas en la versión 0.20.3 del CDN.
2. Los libros Excel de los escenarios 2 y 3 se abrieron en LibreOffice con los valores guardados borrados, para forzar el recálculo de las 133 y 224 fórmulas. Todas coincidieron con los valores de la aplicación (diferencia máxima 3 × 10⁻¹⁵). Al cambiar v a 0,25 y a 1 en la hoja `Q`, Q y las condiciones recalculadas coincidieron con Python.
3. Los informes PDF pasaron la revisión estructural de qpdf y se rasterizaron para revisarlos: tres páginas con pie y marca de agua en todas.
4. Sin desplazamiento horizontal a 400, 360 y 320 píxeles de ancho; se revisaron capturas de escritorio y de teléfono de las secciones principales.
5. El texto visible de la aplicación, con los cinco escenarios cargados y la verificación ejecutada, no contiene guiones fuera de las referencias bibliográficas.

## 12. Limitaciones

1. El ideal y el peor valor salen de los datos observados. Agregar o quitar una alternativa puede cambiar el orden de las demás, una propiedad conocida de VIKOR.
2. Los pesos por entropía miden cuánto discrimina cada criterio en la muestra, no su importancia para quien decide, y cambian si cambian los datos. Exigen valores no negativos.
3. DQ = 1/(m − 1) es muy exigente con tres alternativas o menos; en esos casos es frecuente obtener un conjunto de compromiso.
4. La sensibilidad a los pesos es numérica (malla y bisección) y cambia un criterio a la vez; no explora cambios simultáneos de varios pesos.
5. Los datos se consideran ciertos. No se implementan variantes difusas, por intervalos ni con normalizaciones alternativas de VIKOR.
6. La aplicación no guarda los datos: al recargar la página se pierden, por lo que conviene exportar el Excel o el PDF.
7. Por rendimiento del navegador se admiten hasta 60 criterios y 60 alternativas; no es un límite del método.

## 13. Referencias

Hwang, C.-L., & Yoon, K. (1981). *Multiple attribute decision making: Methods and applications*. Springer. https://doi.org/10.1007/978-3-642-48318-9

Opricovic, S. (1998). *Multicriteria optimization of civil engineering systems*. Faculty of Civil Engineering, Belgrade.

Opricovic, S., & Tzeng, G.-H. (2004). Compromise solution by MCDM methods: A comparative analysis of VIKOR and TOPSIS. *European Journal of Operational Research, 156*(2), 445–455. https://doi.org/10.1016/S0377-2217(03)00020-1

Opricovic, S., & Tzeng, G.-H. (2007). Extended VIKOR method in comparison with outranking methods. *European Journal of Operational Research, 178*(2), 514–529. https://doi.org/10.1016/j.ejor.2006.01.020

Yu, P. L. (1973). A class of solutions for group decision problems. *Management Science, 19*(8), 936–946. https://doi.org/10.1287/mnsc.19.8.936

## 14. Cómo citar

Gómez Rueda, M. S. (2026). *Harmonía VIKOR* (Versión 1.0) [Aplicación web]. Uso académico.
