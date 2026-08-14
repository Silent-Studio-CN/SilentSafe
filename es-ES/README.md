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
- Experiencia estilo Kaspersky: protección activada por defecto, solo resultados, detalles técnicos ocultos

## Stack tecnológico

Python + PySide6 + QFluentWidgets + motor de escaneo en C++ + extensión de aceleración Rust

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
