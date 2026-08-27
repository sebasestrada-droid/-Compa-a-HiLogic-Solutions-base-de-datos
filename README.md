# 📊 Modelo de Base de Datos — Gestión de Sucursales

## 📝 Descripción

Proyecto académico de modelamiento de una base de datos orientada a la gestión de **sucursales, trabajadores, contratos, clientes, productos y boletas de venta**.

El proyecto contempla el diseño de un **Modelo Entidad-Relación Extendido (MER-E)** y su posterior representación mediante un **modelo relacional**, utilizando Oracle SQL Developer Data Modeler.

El objetivo es representar correctamente las entidades, atributos, relaciones, cardinalidades y jerarquías de especialización definidas según las reglas de negocio del caso.

---

## 🎯 Objetivos

- Identificar las entidades principales del sistema.
- Definir los atributos correspondientes a cada entidad.
- Establecer claves primarias y claves foráneas.
- Definir las relaciones entre las entidades.
- Establecer cardinalidades y obligatoriedad.
- Representar jerarquías mediante supertipos y subtipos.
- Aplicar buenas prácticas de nomenclatura.
- Utilizar Oracle SQL Developer Data Modeler para desarrollar el modelo.

---

## 🧩 Entidades del modelo

### Entidades principales

**SUCURSAL**
- `numero_sucursal` — Clave primaria
- `nombre`
- `direccion`
- `comuna`

**CONTRATO**
- `numero_contrato` — Clave primaria
- `fecha_contrato`
- `numero_sucursal` — Clave foránea
- `rut_trabajador` — Clave foránea

**TRABAJADOR**
- `rut_trabajador` — Clave primaria
- `nombre`
- `fecha_nacimiento`

**CARGO**
- `codigo_cargo` — Clave primaria
- `descripcion`
- `rut_trabajador` — Clave foránea

**CLIENTE**
- `rut_cliente` — Clave primaria
- `puntos`

**BOLETA**
- `numero_boleta` — Clave primaria
- `fecha_boleta`
- `monto_venta`
- `cantidad_productos`
- `rut_cliente` — Clave foránea

**PRODUCTO**
- `codigo_producto` — Clave primaria
- `descripcion`
- `valor`
- `marca`
- `stock`

---

## 👥 Subtipos de CLIENTE

### CLIENTE_VIP

- `porcentaje_descuento`

### CLIENTE_NORMAL

- `descuento_pesos`

La entidad `CLIENTE` funciona como supertipo y se especializa en `CLIENTE_VIP` y `CLIENTE_NORMAL`.

---

## 📄 Subtipos de CONTRATO

### CONTRATO_PRACTICANTE

- `compensacion`

### CONTRATO_INDEFINIDO

- `afp`
- `sistema_salud`
- `sueldo_base`

La entidad `CONTRATO` funciona como supertipo y se especializa en `CONTRATO_PRACTICANTE` y `CONTRATO_INDEFINIDO`.

---

## 🔗 Relaciones

| Entidades | Relación | Cardinalidad |
|---|---|---|
| SUCURSAL — CONTRATO | **ASIGNA** | 1 : N |
| SUCURSAL — BOLETA | **EMITE** | 1 : N |
| CLIENTE — BOLETA | **REALIZA** | 1 : N |
| TRABAJADOR — BOLETA | **EMITE** | 1 : N |
| TRABAJADOR — CONTRATO | **TIENE** | 1 : N |
| PRODUCTO — BOLETA | **INCLUYE** | N : N |
| TRABAJADOR — CARGO | **OCUPA** | Según cardinalidad definida en el modelo |

### Especializaciones

- `CONTRATO` → `CONTRATO_PRACTICANTE`
- `CONTRATO` → `CONTRATO_INDEFINIDO`
- `CLIENTE` → `CLIENTE_VIP`
- `CLIENTE` → `CLIENTE_NORMAL`

---

## 🏗️ Jerarquías del MER-E

### CLIENTE

```text
                 CLIENTE
                /       \
               /         \
      CLIENTE_VIP    CLIENTE_NORMAL
