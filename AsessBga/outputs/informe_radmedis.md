---
title: "Informe General — Assessment Radmedis"
subtitle: "Analisis de Cartera de Clientes"
author: "Farid Sayago"
organization: "Radmedis"
date: "2026-03-10"
version: "1.0"
abstract: "Analisis de una cartera de 10 clientes con registros de pago para el periodo febrero--octubre 2024. Total recaudado: 1,100,000 COP. Tasa de recuperacion estimada: 44% (proxy de deuda: 250,000 COP por cliente). Dos clientes en mora. Tres clientes con pagos sin fecha confirmada. Cinco clientes con pago formalizado."
toc: false
---

# Alcance y Metodologia

El dataset contiene 10 registros con cuatro variables: ID Cliente, Nombre, Fecha de Pago y Monto Pagado. El analisis cubre el periodo febrero--octubre 2024. Las definiciones analiticas adoptadas son:

- **Mora:** cliente sin fecha de pago (NaT) y monto igual a cero.
- **Pago sin fecha:** monto registrado mayor a cero pero sin fecha de cobro confirmada.
- **Recuperacion:** calculada sobre un proxy de 250,000 COP por cliente (deuda original no disponible).
- **Desglose mensual:** solo meses con pagos efectivamente registrados; no se imputan ceros.

# KPIs de Cartera

| KPI | Valor |
|---|---|
| Total clientes | 10 |
| Total recaudado | 1,100,000 COP |
| Deuda proxy total | 2,500,000 COP |
| Tasa de recuperacion* | 44.0% |
| Clientes en mora | 2 |
| Clientes con pago sin fecha | 3 |
| Clientes pagados con fecha | 5 |

*Aproximacion. Requiere deuda original real para calculo preciso.

# Clasificacion de Clientes

| ID | Nombre | Fecha de Pago | Monto (COP) | Estado |
|---|---|---|---|---|
| C001 | Juan Perez | Sin registro | 0 | En mora |
| C002 | Maria Gomez | 2024-02-20 | 100,000 | Pagado con fecha |
| C003 | Carlos Lopez | 2024-03-09 | 50,000 | Pagado con fecha |
| C004 | Ana Diaz | Sin registro | 250,000 | Pago sin fecha |
| C005 | Luis Torres | 2024-05-26 | 50,000 | Pagado con fecha |
| C006 | Lucia Ramirez | Sin registro | 0 | En mora |
| C007 | Andres Martinez | Sin registro | 100,000 | Pago sin fecha |
| C008 | Paola Mejia | 2024-08-28 | 250,000 | Pagado con fecha |
| C009 | Pedro Rios | Sin registro | 250,000 | Pago sin fecha |
| C010 | Laura Sanchez | 2024-10-04 | 50,000 | Pagado con fecha |

# Desglose Mensual

Solo se incluyen los cinco meses con pagos registrados. Meses sin actividad se omiten.

| Mes | N Clientes | Monto Total (COP) |
|---|---|---|
| 2024-02 | 1 | 100,000 |
| 2024-03 | 1 | 50,000 |
| 2024-05 | 1 | 50,000 |
| 2024-08 | 1 | 250,000 |
| 2024-10 | 1 | 50,000 |

El mes de mayor recaudacion fue agosto 2024 (250,000 COP, Paola Mejia). La recaudacion no presenta un patron de regularidad mensual.

# Hallazgos

1. El 50% de los clientes no tiene fecha de pago registrada, lo que impide un analisis de flujo de caja confiable.
2. El 20% (C001, C006) se encuentra en mora efectiva, con riesgo de incobrabilidad directa.
3. El 30% (C004, C007, C009) tiene pagos acreditados pero sin trazabilidad temporal.
4. La recaudacion se concentra en pagos puntuales y dispersos, sin esquema de cobro periodico.
5. No se detectaron duplicados ni errores tipograficos en el dataset.

# Conclusiones y Recomendaciones

**Calidad de datos:** Implementar registro obligatorio de fecha en todos los pagos para habilitar analisis de flujo de caja real.

**Gestion de mora:** Definir un proceso formal de seguimiento para C001 y C006 con plazos y responsables asignados.

**Recuperacion:** Obtener la deuda original por cliente para calcular la tasa real y priorizar gestiones de cobro segun exposicion.

**Estructura de pagos:** Establecer esquemas de pago periodicos para normalizar la recaudacion y reducir la dependencia de pagos esporadicos.
