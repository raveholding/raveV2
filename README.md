# Sistema RAVE · demo para el cliente

Demo de evaluación de **Sistema RAVE** (VINCULAR BUSINESS) con los datos de Almacén y Licorería RAVE (Urquiza 1052, Salta).
Un solo archivo (`index.html`): menú público adelante y panel de gestión en `#acceso`.

- Menú público: `/`  · Acceso del equipo: `/#acceso`
- Usuarios de prueba: ADMIN 1234 · Supervisor 1111 · Mostrador 0000

**Es una demo.** Costos, stock, códigos de barras, cupones, membresía, Wi-Fi, clientes y ventas históricas son de ejemplo.
Los datos se guardan sólo en el navegador de quien la prueba. No hay nube ni claves en el archivo (Sistema → Nube figura como *Pendiente de configuración*).
**Facturación electrónica (ARCA):** al cobrar con *Con ARCA (F8)* la demo genera un comprobante **SIMULADO** (CAE inventado, rotulado «SIN VALIDEZ FISCAL») para mostrar el recorrido: elegir receptor, factura, ticket con CAE y nota de crédito. En el sistema del cliente el CAE lo pide el servidor a ARCA (WSAA + WSFE) con el certificado del propio comercio; ese recorrido todavía debe probarse en homologación.
Los textos legales son plantillas [VERIFICAR] con asesor; periféricos sin probar con equipos reales.

**V26.13:** Tiendanube como integración (en la demo es una **conexión simulada** con datos de ejemplo: conectar, vincular productos, recibir una orden y registrarla como venta), **pasos para conectar cada integración**, cobro mayorista por tramos, traspasos de fondos sin rubros (un solo dueño con varias cajas y caja principal) y pago a proveedores repartido entre cajas.

**V26.1:** cobro mixto con vuelto y cuenta corriente parcial, y marca oficial VINCULAR BUSINESS.

Desarrollado por **VINCULAR BUSINESS** · Único celular (387) 4484132 · vincularbusiness@gmail.com · *“Tu idea, en buenas manos.”*
