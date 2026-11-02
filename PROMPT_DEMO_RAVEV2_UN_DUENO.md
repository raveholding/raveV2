# SISTEMA VB · PROMPT DE VERSIÓN — DEMO «UN SOLO DUEÑO» (repositorio `raveV2`)

**Versión:** V26.43 · 2026-11-02 · **Producto:** SISTEMA VB de **VINCULAR BUSINESS** · **Publicación:** `https://raveholding.github.io/raveV2/`
**Para qué es:** demo para mostrar a clientes que son **un comercio de un solo dueño** (almacén, kiosco, autoservicio, comercio minorista). Se la prueban como propia: sin socios, sin rubros por persona, sin asistentes inteligentes y **sin nada de Almacén RAVE**.

> Este prompt define **esta versión**. Los requisitos funcionales completos de cada módulo están en el prompt maestro genérico `SISTEMA_VB_26F.md` (secciones 0–16). Acá se dice qué módulos lleva esta demo, cuáles no y qué datos usa. Si este prompt y el maestro difieren, **manda este prompt para esta demo**.

---

## 1. Mapa de versiones de SISTEMA VB (no mezclarlas)

| Versión | Repositorio y publicación | Para quién | Compilación (`fuente/build.py`) | Base local del navegador |
|---|---|---|---|---|
| **Cliente Almacén RAVE** (producción) | `AlmacenRAVE` | El negocio de los dueños: socios y rubros por persona | `cliente` (con la nube) | `rave-almacenrave-v1` |
| **Demo mayorista/minorista** | `KiniDistribuidoraDemo` | Distribuidoras y mayoristas | `kini` | `rave-kini-demo-v2` |
| **Demo un solo dueño** (ESTA) | `raveV2` | Comercio minorista de un dueño | `solo` | `rave-solo-demo-v1` |
| **Demo con asistentes inteligentes** | `raveV3` | Como Almacén RAVE + equipo SVB R2AVE | `v3` | `rave-v3-demo-v1` |

- **Una sola fuente de código** (`AlmacenRAVE/fuente`). Las versiones son **perfiles de compilación**, no copias. Nunca se edita a mano el `index.html` de una demo.
- Cada demo tiene **su propia base local** en el navegador. GitHub Pages comparte el origen `raveholding.github.io` entre repositorios: con el mismo nombre, una demo pisaría los datos de otra.
- Publicar una demo **no** publica las otras ni el cliente. Kini y el cliente no se tocan cuando se trabaja en esta demo.

## 2. Ficha de la demo (datos de ejemplo, rotulados «ejemplo»)

| Dato | Valor en la demo |
|---|---|
| Nombre comercial | **Mi Comercio** · «Almacén y kiosco · demo» (logo genérico «MI COMERCIO / DEMO») |
| Dirección, WhatsApp, redes, Wi-Fi | Vacíos o «(dirección de ejemplo)». **No** se usa ningún dato de Almacén RAVE |
| Colores | Grafito `#1f2a37` y verde azulado `#2e8b74` (no los dorados de RAVE) |
| Tipo de negocio | **Un solo dueño, fijo** (`cfg.biz='owner'`, `bizLocked`): todo el dinero es del dueño |
| Categorías | Almacén · Bebidas · Bebidas con alcohol (+18) · Lácteos y frescos · Golosinas y snacks · Limpieza y perfumería. **Sólo ordenan** inventario, Vender y menú: no son personas ni cajas |
| Catálogo | 27 artículos genéricos sin marcas (más un pesable por kilo y un combo), con código de barras de ejemplo, costo, precio y stock (algunos bajos para ver alertas) |
| Cajas | Perfil **simple**: una caja (se pueden agregar cajas y una caja principal desde «Cajas y sucursales») |
| Equipo | Usuario **ADMIN / 1234** y los roles de siempre; un empleado de mostrador de ejemplo con fichaje |
| Clientes y Club | Tres clientes de ejemplo con consentimiento, sellos y una membresía; cupón `BIENVENIDA10` |
| Venta | **Minorista** (el canal mayorista queda apagado: para mayoristas está la demo Kini) |
| Créditos | **VINCULAR BUSINESS** con banner y botones oficiales (regla 11 del maestro): **no se quitan** |

## 3. Qué lleva y qué NO lleva

**Lleva** (con los requisitos del maestro): Resumen/Analytics, Vender (POS con F1–F12, lector, balanza, pagos mixtos, cuenta corriente, cupones, sellos), Caja, Arqueo y cierre de **un solo dueño** (ventas por medio, esperado y contado), Cajas cerradas, Inventario por categorías, Proveedores y compras, Clientes, Fidelización (Club, tarjeta, sellos), Cupones y membresías, Personal y fichaje, Tareas, Menú público (pedido por WhatsApp, modo «tienda con envíos» opcional), Legal, Periféricos y ticket, Importar/Exportar, Integraciones (en estado real), Roles, Auditoría, Configuración (incluye «Borrar todo y empezar vacío» y «Volver a los datos de ejemplo»), el Asistente de texto de comandos (`ActionRegistry`, 4.13) y la facturación con **simulador rotulado** (sin validez fiscal).

**NO lleva:**
- **Centro Inteligente, Gerente IA ni el equipo SVB R2AVE.** Están en raveV3. La compilación `solo` no incluye `p10-centro.js`, `p10b-r2ave.js` ni `p10c-vivo.js`.
- **Socios ni rubros por persona.** No hay reparto, sueldo a medias, impuesto por socio, ganancia propia ni caja por rubro (la 4.27 del maestro no aplica).
- **Canal mayorista** (4.22): para eso está Kini.
- **Ningún dato de Almacén RAVE.** Ni nombre, dirección, teléfono, WhatsApp, Instagram, Wi-Fi, rubros, catálogo, reseñas ni textos para buscadores.

## 4. Dónde vive en el código

- `fuente/p3o-solo.js`, perfil «solo»:
  - `soloCats` y `soloProds` (catálogo).
  - `soloBase` (datos y configuración de la demo).
  - `soloExtras` (quita clientes y ventas mayoristas de los ejemplos generales).
- Enganches mínimos:
  - `p2-core.js`: `DEF()` aplica `soloBase`; `bizMigrate` fija un solo dueño.
  - `p6-loyalty.js`: `demoExtras` llama `soloExtras`.
  - `p3k-owner.js`: el texto dice «Comercio de un solo dueño».
- `fuente/build.py`, perfil `solo`:
  - Marca genérica (`solo_brand`: logo, colores, título y textos del menú público).
  - Base local propia.
  - Sin el Centro Inteligente.

## 5. Compilar, probar y publicar (sin tocar otras versiones)

```bash
cd AlmacenRAVE/fuente
python3 build.py solo /tmp/rave/solo.html && rm -f all.js
cd pruebas && python3 sv1.py          # prueba propia de esta demo
# regresión general (usa las otras compilaciones): v1 v2 v4–v7 d1 p1 h1 h3 g1–g3 k1–k4 kc1 resp4 pq1
cp /tmp/rave/solo.html ../../../ravev2/index.html   # luego commit y push en raveV2
```

**Prueba `sv1` (18 verificaciones; todas deben pasar):**
- **Marca y contenido:** el ingreso no muestra nada de Almacén RAVE; los créditos de Vincular Business están; ninguna pantalla muestra datos de Almacén RAVE; el menú público es de «Mi Comercio»; el archivo publicado no contiene el Centro ni los asistentes.
- **Modelo de negocio:** es un solo dueño fijo; las categorías no tienen responsable ni reparto; no hay Centro ni asistentes; no hay canal mayorista; el arqueo no tiene sueldo, reparto ni ganancia por socio.
- **Operación:** se vende yerba + gaseosa = $ 7.100, se descuenta el stock, el dinero va a la caja del negocio y el arqueo lo muestra.
- **Forma:** 360 px sin desborde y consola sin errores.

## 6. Reglas que no se negocian en esta demo

1. Datos inventados rotulados «ejemplo» (regla 14 del maestro). La demo no es el sistema del cliente: no se conecta a la nube.
2. Si se agrega un módulo al código común, se decide **explícitamente** si entra en `solo`: por defecto, nada nuevo del Centro Inteligente entra acá.
3. Antes de publicar, `sv1` en verde y regresión sin fallas nuevas. Nunca se publica esta demo en otro repositorio.
4. Entrega honesta: qué cambió, qué se probó y qué no.

## 7. Límites conocidos

- La jurisdicción legal por defecto sigue siendo «Argentina / Salta» (horario de alcohol y textos legales `[VERIFICAR]`). Se cambia en «Legal y cumplimiento» según el cliente.
- El asistente de texto (comandos como «cuánto vendimos hoy») sigue incluido: es parte del núcleo, no es el equipo de asistentes inteligentes. Si se lo quiere quitar de esta demo, hay que pedirlo.
- Una visita anterior a raveV2 con datos de Almacén RAVE queda en la base vieja del navegador (`rave-cliente-v3`). La demo nueva arranca limpia en `rave-solo-demo-v1`.
