# **Los 4 Pilares del diseño del proyecto**:

---

## 🔹 1. Origen de datos y sincronización con el software Python

* El sistema de Python ya emite facturas y genera el QR.
* **la base de datos municipal en Azure será el *único punto de verdad*** (single source of truth).
* Tanto el sistema Python como la aplicación web van a leer y escribir en esa misma BD (cada uno en su scope).
* La web debe tener permisos para **actualizar estados de facturas** (ej. de `pendiente` a `pagado`).

Independencia del software Python: él sigue mandando la factura y el QR, pero **el pago y la acreditación se controlan desde el servidor Backend en Azure**.

---

## 🔹 2. Flujo del contribuyente (usuario final)

1. Recibe la factura con un QR.
2. Escanea el QR → lo lleva a **Web de la factura en Azure**.
3. En la web se muestran los mismos datos de la factura (monto, vencimiento, descripción).
4. Usuario hace clic en **“Pagar”**.
5. Se procesa el pago vía **pasarela de pagos (ej. Mercado Pago, TodoPago, o integraciones de Azure Payment Connector)**.
6. Al recibir la confirmación de pago (webhook o callback de la fintech), el backend actualiza la factura en la BD municipal como **pagada**.
7. El servidor web envía un comprobante por mail (ej. usando **Azure Communication Services**).

---

## 🔹 3. Infraestructura en Azure

* **Frontend + Backend** → Azure App Service (Node.js/Express).
* **Base de datos municipal** → Azure SQL Database.
* **Archivos y comprobantes** → Azure Blob Storage (para guardar recibos o PDFs).
* **Autenticación segura** (para administración interna) → Azure AD B2C.
* **Monitoreo y logs** → Application Insights. (registros de actividad para datos contables)

⚡ Stack profesional, escalable y fácil de administrar con una sola cuenta de Azure.

---

## 🔹 4. Buenas prácticas de arquitectura

* **Separación de responsabilidades**:
  * App Node.js → solo lógica web y de pagos.
  * Python → sistema de administración y facturación contable.

* **Comunicación desacoplada**:
  * La BD compartida es la fuente común.
  * El servidor Web no depende del sistema Python para marcar pagos.

* **Seguridad primero**:
  * BD protegida, usando **Azure Managed Identity**, un **ORM** y **roles mínimos**.
  * Toda comunicación con la pasarela de pagos es HTTPS y con claves seguras en **Azure Key Vault**.

---
