# SilentSafe

SilentSafe es un software de protección de la seguridad para dispositivos personales, producido por **SilentStudio**.

- **Versión**: v1.0.0
- **Plataforma**: Windows

> Este repositorio es solo para la presentación del proyecto y **no contiene código fuente**.

## Características

- Escaneo de seguridad de archivos (paralelo multihilo + aceleración Rust)
- Monitoreo del sistema en tiempo real (registrado como servicio de Windows; reinicio automático ante fallos; la protección continúa incluso tras cerrar la aplicación)
- Gestión de cuarentena
- Protección de comportamiento (procesos / registro / red)
- Detección profunda de inyecciones (ETW-TI)
- Protección activada por defecto; la interfaz muestra solo los resultados y oculta los detalles técnicos

## Stack tecnológico

Python + PySide6 + QFluentWidgets + motor de escaneo en C++ + extensión de aceleración Rust

## Arquitectura

- **Capa UI**: Python + PySide6 + QFluentWidgets; navegación multipágina (Inicio / Consejos / Escaneo / Protección / Comportamiento / Cuarentena / Avisos / Ajustes); tema claro/oscuro y color de acento; cambio instantáneo de idioma (zh/en).
- **Motor de escaneo**: C++ (SilentSecurityEngine), escaneo paralelo multihilo, transmite progreso y resultados como JSONL; modos de archivo / directorio / disco completo.
- **Aceleración**: Rust (`ss_rust.pyd`, PyO3) analiza y agrega la salida JSONL del motor por lotes, aproximadamente 3x más rápido que el análisis línea a línea en Python; retrocede automáticamente a Python puro cuando no está disponible (semántica idéntica).
- **Monitoreo en tiempo real**: Windows `ReadDirectoryChangesW` basado en eventos, recursivo en todos los discos fijos; los aciertos de firma confirmados se eliminan automáticamente y los aciertos heurísticos se ponen en cuarentena.
- **Protección de comportamiento**: creación de procesos mediante ETW (0 latencia, detrás de `NtCreateProcess`; retroceso a sondeo si no está disponible); inicio automático del registro y conexiones salientes mediante diferencia de instantáneas; los eventos llevan PID / PID padre / cadena de comportamiento.
- **Servicio del sistema**: el motor se registra como servicio de Windows (SCM, inicio automático) con política de reinicio ante fallos (5 s / 10 s / 60 s); desacoplado del proceso UI — la protección continúa tras salir y el SCM lo reinicia si el proceso es terminado.
- **Sandbox**: los ejecutables de alto riesgo que fallan en cuarentena se analizan automáticamente en un proceso aislado, se reevalúan según el comportamiento muestreado y se reintenta la cuarentena si hay veredicto malicioso.
- **Verificación de firma**: validación offline de Authenticode con WinVerifyTrust + extracción del firmante (sin comprobar revocación, sin red); las firmas válidas de Microsoft / Google se confían por completo, otras firmas válidas se degradan mostrando el firmante.
- **Detección profunda de inyección**: ETW-TI (sesión de núcleo AutoLogger, Windows 11).
- **Modelo de comunicación**: UI y motor desacoplados mediante JSONL — tubería stdout para los escaneos; en modo servicio, los eventos de monitoreo/comportamiento se escriben en archivos y la UI los lee de forma incremental.
- **Cuarentena**: los archivos se mueven a un directorio de cuarentena y se renombran para impedir su re-ejecución; se admiten lista / restaurar / eliminar; la cuarentena y los registros se excluyen del escaneo.

---

## Derechos de autor

**Copyright © SilentStudio**

Algunos componentes públicos de este software (por ejemplo, ejemplos de SDK, partes del código frontend o módulos aportados por la comunidad) pueden estar sujetos a la GNU Affero General Public License (AGPL) v3.0 y sus términos complementarios cuando se cumplan condiciones específicas.

Los motores principales (por ejemplo, SilentSecurityEngine), los servicios en la nube (SSDBS) y cualquier parte no marcada explícitamente como Open Source están protegidos por las leyes de derechos de autor. La reproducción, modificación, ingeniería inversa o distribución comercial no autorizada de estas partes está estrictamente prohibida sin el consentimiento previo por escrito de SilentStudio.

---

## Equipo

SilentStudio, como organización matriz de SilentCodeTeams, supervisa el desarrollo y las operaciones de los siguientes subequipos:

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
