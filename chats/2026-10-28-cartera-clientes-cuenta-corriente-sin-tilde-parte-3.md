# Cartera CC: carga del tilde Cuenta Corriente en iTraffic Cuenca

- **Fecha:** 2026-10-28
- **Proyecto / cliente:** Cuenca del Plata (iTraffic Cuenca) — cartera de clientes con cuenta corriente autorizada
- **Actualiza a:** [2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde-parte-2.md](2026-10-28-cartera-clientes-cuenta-corriente-sin-tilde-parte-2.md)

## Objetivo
Marcar el tilde de cuenta corriente en los 15 clientes de la cartera que no lo tenían.

## Estado final
Terminado. Los 15 clientes quedaron con el tilde guardado, y cada uno se verificó reabriendo la ficha después de guardar. [datos]

## Decisiones y por qué
- La usuaria pidió hacerlo directamente en el sistema. Inició sesión ella en el navegador de la app y confirmó el primer cliente antes de seguir con el resto. [decisión]
- En cada ficha se cambió sólo ese tilde. No se tocó ningún otro campo. [decisión]

## Archivos, tablas y objetos relevantes
- Pantalla: iTraffic Cuenca → Maestros → Cliente (`/iTraffic_Cuenca/A_Maestros/Agencia`), pestaña Generales, sección Estadísticas, tilde "Cuenta Corriente". [datos]
- En el formulario, el campo es `Ctacte` (`AgenciaDialog`, Softur.Serenity, módulo A_Maestros). En el export del listado aparece como la columna "Concuentacorriente". [datos]
- Para buscar se escribe el nombre y se hace clic en la lupa; Enter no dispara la búsqueda. Para guardar se usa el botón "Actualizar", que guarda y cierra la ficha. [datos]
- IDs actualizados: 13188, 12233, 3478, 31270, 1276, 12155, 12905, 12990, 31278, 517, 12283, 2992, 1341, 12052, 31305.

## Cambios hechos
Tilde Cuenta Corriente activado y guardado en los 15 clientes listados arriba.

## Errores y cómo se resolvieron
- La sesión no se veía en el navegador de la app — la usuaria había iniciado sesión en otra ventana — volvió a iniciar sesión en el navegador de la app.
- La búsqueda a veces no se aplicaba porque se escribía antes de que cargara la página — se agregó una espera de unos 4 segundos después de cargar.

## Riesgos
- En 4 HATS TRAVEL el tilde "Activo" (Estadísticas) está sin marcar. No se tocó; está pendiente confirmar si corresponde. [datos]

## Pendientes
- [ ] Revisar el tilde "Activo" de 4 HATS TRAVEL (y del resto, si aplica) — usuaria.

## Cómo validar
Exportar de nuevo el listado de Clientes y filtrar esos 15 IDs: la columna Concuentacorriente tiene que estar en VERDADERO.

## Datos que pueden quedar viejos
- Clientes con tilde en el sistema — 124 (109 + 15) — (foto al 2026-10-28)
