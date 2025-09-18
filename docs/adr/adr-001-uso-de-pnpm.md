# ADR-001 — Uso de pnpm en lugar de npm

## Estado
Aceptado

## Contexto
En agosto y septiembre de 2025, múltiples dependencias de **npm** fueron comprometidas con ataques de cadena de suministro.  
Esto genera un riesgo directo en proyectos que instalan dependencias de forma no controlada.

## Decisión
Adoptamos **pnpm** como gestor de dependencias para el proyecto.  
Se eligió pnpm por sus ventajas:
- Seguridad reforzada en la resolución de dependencias.
- Lockfile (`pnpm-lock.yaml`) más confiable.
- Instalaciones más rápidas y ahorro de espacio en disco.

## Consecuencias
- Todos los desarrolladores deben instalar y usar **pnpm**.  
- El `package-lock.json` no se usará; en su lugar se versiona `pnpm-lock.yaml`.  
- La documentación del setup debe reflejar este cambio.

## Configuración
- Todos los paquetes instalados para el proyecto deben tener al menos 10 días desde su última actualización.
- En caso de excepción dejar documentado el motivo y el date completo de la instalación del paquete.

[pnpm-workspace.yaml](../../pnpm-workspace.yaml)
```` 
minimumReleaseAge: 14400 # 10 días
minimumReleaseAgeExclude:
  - react # ejemplo
````
