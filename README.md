# Harmonía VIKOR

Aplicación web académica para decidir con el método **VIKOR** de Opricovic y Tzeng: encuentre la alternativa que más se acerca al ideal sin dejar a ningún criterio demasiado atrás, equilibrando lo que conviene a la mayoría de criterios con el peor rezago individual.

**Abrir la aplicación:** https://mgomezr1.github.io/harmonia-vikor/

No requiere instalación ni registro. Funciona en cualquier navegador moderno, en computador, tableta o teléfono.

## Qué permite hacer

- Definir un objetivo, los criterios y las alternativas, en la cantidad que necesite.
- Indicar si cada criterio es de beneficio o de costo.
- Digitar los pesos o calcularlos por entropía de Shannon a partir de los datos.
- Elegir el peso v de la estrategia de la mayoría, con 0,5 como valor de consenso.
- Obtener las lejanías normalizadas, la utilidad de grupo S, el arrepentimiento individual R y el índice Q.
- Revisar las condiciones de ventaja aceptable (C1) y estabilidad aceptable (C2) y obtener la solución o el conjunto de compromiso.
- Hacer análisis de sensibilidad exacto frente a v y frente al peso de cada criterio.
- Descargar los resultados en Excel, con fórmulas reales en cada paso, y un informe ejecutivo en PDF.

## Cómo usarla

1. Mueva la balanza de la portada para ver cómo v cambia la alternativa preferida y lea «Cómo funciona VIKOR».
2. En **Configuración**, escriba el objetivo, el número de criterios y de alternativas y registre los nombres.
3. En **Criterios y pesos**, indique el sentido de cada criterio, elija el método de pesos y confirme.
4. En **Matriz de decisión**, digite los valores. El color de cada celda muestra su lejanía al mejor valor del criterio.
5. En **Estrategia v**, elija v y pulse **Calcular resultados**.
6. Si quiere, explore la **Sensibilidad** y descargue el **Excel** o el **informe PDF**.

El **modo de prueba** carga ejemplos con datos ficticios para practicar; esos datos no representan decisiones reales.

## Privacidad

Todos los cálculos se hacen en su navegador. Los datos no se envían a ningún servidor ni se guardan: al cerrar o recargar la página se pierden, así que descargue el Excel o el PDF antes de salir.

## Requisitos

- Navegador actualizado (Chrome, Edge, Firefox o Safari) con JavaScript activo.
- Conexión a internet para exportar a Excel, porque la aplicación descarga la biblioteca SheetJS. El informe PDF funciona sin conexión.

## Documentación

La guía completa (método, fórmulas, funciones, exportaciones, verificación y limitaciones) está en [docs/Guia_Harmonia_VIKOR.md](docs/Guia_Harmonia_VIKOR.md).

## Cómo citar

Gómez Rueda, M. S. (2026). *Harmonía VIKOR* (Versión 1.0) [Software]. https://mgomezr1.github.io/harmonia-vikor/

## Autoría y uso

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Consulte los términos en [LICENSE.md](LICENSE.md). Sugerencias o dudas: mgomezr1@gmail.com

## Fundamento metodológico

- Opricovic, S. (1998). *Multicriteria optimization of civil engineering systems*. Faculty of Civil Engineering, Belgrade.
- Opricovic, S., & Tzeng, G.-H. (2004). Compromise solution by MCDM methods: A comparative analysis of VIKOR and TOPSIS. *European Journal of Operational Research, 156*(2), 445–455. https://doi.org/10.1016/S0377-2217(03)00020-1
- Opricovic, S., & Tzeng, G.-H. (2007). Extended VIKOR method in comparison with outranking methods. *European Journal of Operational Research, 178*(2), 514–529. https://doi.org/10.1016/j.ejor.2006.01.020
- Hwang, C.-L., & Yoon, K. (1981). *Multiple attribute decision making: Methods and applications*. Springer. https://doi.org/10.1007/978-3-642-48318-9
- Yu, P. L. (1973). A class of solutions for group decision problems. *Management Science, 19*(8), 936–946. https://doi.org/10.1287/mnsc.19.8.936

## Componentes de terceros

La exportación a Excel usa [SheetJS Community Edition](https://sheetjs.com), distribuida bajo la licencia Apache 2.0 y cargada desde cdn.sheetjs.com.
