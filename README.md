# Ley 81 + Snowflake: Guia Completa de Cumplimiento

Entrenamiento paso a paso para implementar cumplimiento con la **Ley 81 de 26 de marzo de 2019** (Proteccion de Datos Personales de Panama) usando recursos nativos de Snowflake. Cubre desde fundamentos legales hasta operacion completa con 9 modulos ejecutables.

---

## Que esta incluido

| Archivo | Descripcion |
|---------|-------------|
| `LEY81_SNOW.html` | Guia interactiva con teoria, SQL ejecutable y sidebar navegable (dark mode) |
| `LEY81_SNOW.sql` | SQL consolidado (1100+ lineas) para ejecucion directa en Snowsight |

## Modulos

| # | Modulo | Articulos Ley 81 | Recursos Snowflake |
|---|--------|-------------------|-------------------|
| 1 | Fundamentos de la Ley 81 | Arts. 1-5, 20 | Vision general de la arquitectura |
| 2 | Gobernanza y RBAC | Arts. 17, 20 | Roles, grants, segregacion de funciones |
| 3 | Clasificacion de Datos | Arts. 1-5, 10 | `SYSTEM$CLASSIFY`, tags de sistema |
| 4 | Tags Personalizados | Arts. 6, 8-9, 17 | Object tagging, herencia, bases legales |
| 5 | Enmascaramiento Dinamico | Arts. 20, 6 | Masking policies, tag-based masking |
| 6 | Row Access Policies | Art. 6 num. 1, Art. 20 | RAP, limitacion de finalidad |
| 7 | Projection Policies | Art. 6 num. 3, Art. 10, Art. 20 | Projection policies (FAIL/NULLIFY), proporcionalidad |
| 8 | Derechos del Titular (ARCO) | Arts. 13-16 | Stored procedures, portabilidad, anonimizacion |
| 9 | Auditoria y Cumplimiento | Arts. 17, 21-24, 31-35 | ACCESS_HISTORY, alertas, reportes |

## Defensa en Profundidad

El entrenamiento implementa tres capas independientes de proteccion en la misma tabla:

```
Capa 1: Row Access Policy    -> filtra FILAS (quien ve cuales registros)
Capa 2: Projection Policy    -> bloquea COLUMNAS en el output (quien ve cuales campos)
Capa 3: Masking Policy        -> transforma VALORES visibles (como aparecen los datos)
```

## Pre-requisitos

- Snowflake Enterprise Edition (o superior)
- Role `ACCOUNTADMIN` o `SYSADMIN` para configuracion inicial
- Snowsight (interfaz web) para ejecucion interactiva

## Como usar

1. **Configure las variables** al inicio del archivo SQL:
   ```sql
   SET LEY81_USER      = '<SU_USUARIO>';
   SET LEY81_DPO_EMAIL = '<SU_EMAIL>';
   ```

2. **Ejecute secuencialmente** cada modulo en Snowsight (Modulo 2 antes de 3, etc.)

3. **O abra el HTML** (`LEY81_SNOW.html`) en el navegador para la guia interactiva con teoria y SQL lado a lado

## Limpieza

Para eliminar todos los objetos creados por el entrenamiento:

```sql
USE ROLE ACCOUNTADMIN;
DROP DATABASE IF EXISTS LEY81_GOVERNANCE;
DROP DATABASE IF EXISTS EMPRESA_DEMO_PA;
DROP WAREHOUSE IF EXISTS LEY81_TRAINING_WH;
DROP ROLE IF EXISTS LEY81_OFICIAL_DATOS;
DROP ROLE IF EXISTS LEY81_PRIVACY_ADMIN;
DROP ROLE IF EXISTS LEY81_DATA_STEWARD;
DROP ROLE IF EXISTS LEY81_ANALYST;
DROP ROLE IF EXISTS RRHH_ANALYST;
DROP ROLE IF EXISTS MARKETING_ANALYST;
DROP ROLE IF EXISTS FINANZAS_ANALYST;
DROP NOTIFICATION INTEGRATION IF EXISTS LEY81_NOTIFICATIONS;
```

## Licencia

[MIT](LICENSE)
