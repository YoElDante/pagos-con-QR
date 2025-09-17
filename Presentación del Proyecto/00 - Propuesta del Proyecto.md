# 📑 Propuesta de Proyecto

## 1. Introducción: el problema actual

* Hoy, los contribuyentes reciben una factura de la municipalidad y deben pagar por medios poco integrados.
* El sistema Python actual resuelve parte del problema (facturación y QR), pero no centraliza el flujo completo ni actualiza de forma automática el estado de la base de datos.
* Esto genera **ineficiencias**, **posibles errores manuales** y **poca trazabilidad**.

---

## 2. Historia del usuario

📌 *Contribuyente*:

* Recibe su factura digital con un QR en su correo/WhatsApp.
* Escanea el QR → llega a una web oficial con el logo del Municipio.
* Ve sus datos (nombre, servicio, monto) y presiona **“Ir a pagar”**.
* Realiza el pago en una pasarela de pago confiable (ej. Mercado Pago).
* Recibe comprobante al instante.

📌 *Usuario interno (municipalidad)*:

* El sistema Python genera la factura y el QR.
* La web se encarga del flujo de pago.
* La BD municipal se actualiza automáticamente → el servicio pasa de **“pendiente”/"adeudado"** a **“pagado”**.
* Se puede auditar y reportar todo desde un único lugar.

---

## 3. Producto final esperado

* **Web multi-municipalidades** centralizada.
* **Arquitectura moderna en Azure** (segura, escalable, con backups y monitoreo).
* **Integración con pasarela de pagos**.
* **Actualización automática de las bases de datos municipales**.
* **QR con token encriptado (JsonWebToken / JWT)** para mayor seguridad.
* **Integración Continua y Entrega/Despliegue Continua (CI/CD)**: despliegue continuo con GitHub Actions o Azure DevOps.

---

## 4. Plan de desarrollo MVP (Producto Mínimo Viable)

✅ **Objetivo del MVP**:
Que un contribuyente pueda pagar online una factura de una municipalidad y que el pago actualice la base de datos.

📌 Etapas MVP:

1. **Infraestructura inicial en Azure**:

   * Web App + Azure SQL + CI/CD.
2. **Modelo básico en Sequelize**: conexión a una DB municipal.
3. **Validación de token en QR**.
4. **Pantalla simple de pago (nombre, monto, botón “Pagar”)**.
5. **Integración con pasarela de pagos**.
6. **Actualización del estado de factura en la DB**.
7. **Envío de comprobante al contribuyente**.

👉 Estimación (siendo un único dev Junior): 2 meses para MVP, trabajando full-time, 40 horas semanales.

---

## 5. Plan de desarrollo completo

📌 Extensiones sobre el MVP:

* Multi-tenant: soportar varias municipalidades con DBs independientes.
* Panel de administración interno para cada municipio.
* Reportes de pagos y auditoría.
* Alertas automáticas de vencimientos.
* Soporte para distintos métodos de pago (no solo Mercado Pago).
* Escalado con Azure Elastic Pools.

👉 Estimación: 6-9 meses para una versión robusta con estas características.

---

## 6. Adaptaciones al software de Python

* El software Python deberá:

  1. Generar el **token JWT** con `id_municipalidad` + `id_factura`.
  2. Incluir ese token en el QR y enviar el link al contribuyente.
* Todo lo demás (validación, actualización de BD, comprobantes) lo manejará la nueva web.

---

## 7. Beneficios del Proyecto

* **Beneficios para la municipalidad**:

  * Cobranza más ágil y segura.
  * Menos carga administrativa manual.
  * Transparencia y trazabilidad total.
* **Beneficios para el contribuyente**:

  * Pago online simple y confiable.
  * Comprobante inmediato.
  * Mayor confianza en el sistema.
* **Beneficios para el equipo**:

  * Independencia tecnológica.
  * Escalabilidad a más municipalidades sin rehacer la solución.

---

