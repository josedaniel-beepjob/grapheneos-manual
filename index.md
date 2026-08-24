# Manual de Usuario y Configuración de GrapheneOS

## Pixel 10 Pro — Configuración de seguridad, privacidad y Credential Routing

**Sistema:** GrapheneOS personalizado
**Dispositivo:** Google Pixel 10 Pro
**Codename:** `blazer`
**Base GrapheneOS:** `2026081300`
**Android:** 17
**Build personalizada:** `2026082001 user`

> ℹ️ **INFORMACIÓN**
>
> Este manual corresponde a una instalación personalizada basada en GrapheneOS. Las funciones estándar de GrapheneOS se documentan según la versión actual, mientras que **Credential Routing** corresponde a una modificación específica de esta instalación.
>
> La release estable oficial disponible actualmente para Pixel 10 Pro es `2026081300`, que coincide con la base utilizada por esta build personalizada.

> ⚠️ **IMPORTANTE**
>
> Antes de cambiar PIN, contraseña, usuarios, Credential Routing, Duress o mecanismos de desbloqueo, asegúrese de conocer las credenciales actuales. Una configuración incorrecta puede impedir el acceso a un perfil o, en el caso de Duress, provocar un borrado irreversible.

---

# 1. Introducción a GrapheneOS

GrapheneOS es un sistema operativo móvil basado en Android Open Source Project con un enfoque reforzado en **seguridad, privacidad, aislamiento de aplicaciones y reducción de superficie de ataque**.

Mantiene la compatibilidad con el modelo de aplicaciones Android, pero añade numerosas protecciones adicionales, entre ellas permisos de red y sensores, Storage Scopes, Contact Scopes, protección USB-C, Auto Reboot, Duress PIN/Password y mejoras en perfiles de usuario.

## Owner y usuarios secundarios

### Owner

**Owner** es el usuario principal del dispositivo.

Tiene funciones administrativas que los usuarios secundarios no tienen, entre ellas la administración de perfiles y determinados ajustes globales.

Después de un reinicio completo, Owner tiene un papel especial y debe desbloquearse antes de que ciertas funciones de los usuarios secundarios puedan utilizarse normalmente.

### Usuarios secundarios

Cada usuario secundario constituye un espacio separado con:

* Aplicaciones propias.
* Datos de aplicaciones propios.
* Contactos propios.
* Archivos propios.
* Configuración propia.
* Credencial de bloqueo propia.
* Claves de cifrado propias.

GrapheneOS mejora el sistema de perfiles de Android y permite hasta 32 perfiles secundarios incluyendo Guest. Finalizar una sesión mediante **End session** detiene sus aplicaciones y elimina de memoria las claves de cifrado de ese perfil.

> ℹ️ **INFORMACIÓN**
>
> Ser Owner **no significa poder leer automáticamente los datos privados de los demás usuarios**.

## Ajustes globales y ajustes por usuario

Algunas configuraciones afectan a todo el teléfono, mientras que otras deben repetirse dentro de cada perfil.

Como regla práctica:

| Configuración           | Alcance                                                |
| ----------------------- | ------------------------------------------------------ |
| PIN/Password            | Por usuario                                            |
| Fingerprint             | Por usuario                                            |
| Scramble PIN            | Por usuario                                            |
| Aplicaciones y permisos | Por usuario/perfil                                     |
| VPN                     | Por perfil                                             |
| Storage Scopes          | Por aplicación y perfil                                |
| Contact Scopes          | Por aplicación y perfil                                |
| Credential Routing      | Administración desde Owner                             |
| Auto Reboot             | Dispositivo                                            |
| Duress PIN/Password     | Configurado desde Owner; borra el dispositivo completo |

---

# 2. Configuración inicial recomendada

Después de configurar un teléfono nuevo, revisar al menos lo siguiente:

* [ ] GrapheneOS correctamente instalado.
* [ ] Bootloader correctamente bloqueado.
* [ ] PIN o Password del Owner configurado.
* [ ] PIN independiente para cada usuario secundario.
* [ ] Scramble PIN revisado en cada usuario.
* [ ] Credential Routing configurado.
* [ ] Prefix independiente asignado a cada usuario.
* [ ] Duress PIN / Password configurado únicamente si el usuario comprende su funcionamiento.
* [ ] Auto Reboot configurado.
* [ ] USB-C Port revisado.
* [ ] Wi-Fi con **Use per-connection randomized MAC**.
* [ ] Network Permission revisado por aplicación.
* [ ] Sensors Permission revisado por aplicación.
* [ ] Storage Scopes utilizado cuando corresponda.
* [ ] Contact Scopes utilizado cuando corresponda.
* [ ] VPN revisada si se utiliza.
* [ ] Actualizaciones revisadas.
* [ ] USB debugging desactivado si no se necesita.
* [ ] OEM unlocking desactivado después de confirmar que el bootloader está bloqueado.

**[CAPTURA 01 — Settings]**

---

# 3. Wi-Fi Privacy — Use Per-Connection Randomized MAC

## ¿Qué es?

Una dirección **MAC** es un identificador utilizado por una interfaz de red para comunicarse dentro de una red local.

Utilizar siempre la misma MAC puede facilitar que una red reconozca que se trata del mismo dispositivo en diferentes conexiones.

GrapheneOS utiliza randomización de MAC y permite elegir cómo se genera esa dirección para cada red.

## ¿Para qué sirve?

Reduce la capacidad de una red Wi-Fi de reconocer y correlacionar conexiones sucesivas del teléfono.

## Ruta desde Settings

`Settings → Network & internet → Internet → [NOMBRE DE LA RED WI-FI] → Privacy`

Esta ruta está documentada oficialmente por GrapheneOS.

## Configuración paso a paso

1. Abra **Settings**.
2. Entre en **Network & internet**.

**[CAPTURA 02 — Network & internet]**

3. Pulse **Internet**.
4. Seleccione la red Wi-Fi que desea configurar.
5. Entre en **Privacy**.
6. Seleccione:

**Use per-connection randomized MAC**

**[CAPTURA 03 — Wi-Fi Privacy]**

## Opciones disponibles

### Use per-connection randomized MAC

Utiliza una MAC aleatoria que puede cambiar entre conexiones.

Es la opción predeterminada de GrapheneOS y la que ofrece mayor privacidad frente a seguimiento por la red.

### Use per-network randomized MAC

Utiliza una MAC aleatoria estable para esa red concreta.

La red podrá reconocer el teléfono en conexiones sucesivas a esa misma red, pero no verá la MAC física del dispositivo.

### Use device MAC

Utiliza la MAC propia del hardware.

Es la opción de menor privacidad y debería utilizarse únicamente cuando existe un motivo específico de compatibilidad.

## Configuración recomendada

**Use per-connection randomized MAC**

## Qué cambia al activarla

La red deja de recibir de forma estable la misma MAC en cada conexión.

## Advertencias

> ⚠️ **ADVERTENCIA**
>
> Algunos hoteles, portales cautivos, redes empresariales, sistemas de acceso y routers identifican dispositivos por su dirección MAC.
>
> Si una red concreta deja de funcionar correctamente, pruebe temporalmente **Use per-network randomized MAC** antes de utilizar **Use device MAC**.

GrapheneOS documenta problemas poco frecuentes con determinados routers y recomienda per-network randomization como alternativa de compatibilidad.

## Cómo comprobar que quedó correctamente configurada

1. Vuelva a:
   `Settings → Network & internet → Internet → [RED] → Privacy`
2. Compruebe que aparece seleccionado:
   **Use per-connection randomized MAC**.

---

# 4. Screen Lock — Configuración del bloqueo del dispositivo

## ¿Qué es?

El **Screen Lock** es la credencial principal que protege el acceso a los datos cifrados de cada usuario.

Puede utilizarse:

* PIN.
* Password.
* Según configuración, Pattern.
* Fingerprint como mecanismo secundario.

## ¿Para qué sirve?

La credencial principal participa en la protección de los datos cifrados del usuario.

Después de un reinicio, es necesario introducir una credencial principal antes de utilizar normalmente mecanismos secundarios como la huella.

## PIN vs Password

### PIN

Más rápido de introducir.

Un PIN aleatorio suficientemente largo ofrece un buen equilibrio entre seguridad y comodidad, especialmente en dispositivos Pixel con protección hardware contra intentos repetidos.

### Password

Permite utilizar una credencial más larga y compleja.

Es especialmente útil cuando se combina con **Two-Factor Fingerprint Unlock**, utilizando una contraseña fuerte como credencial principal y huella + Second-factor PIN para el uso cotidiano.

### Fingerprint

Es un mecanismo secundario de desbloqueo.

No sustituye permanentemente a la credencial principal.

## Ruta desde Settings

`Settings → Security & privacy → Device unlock → Screen lock`

## Configuración paso a paso — Owner

1. Cambie al perfil **Owner**.
2. Abra **Settings**.
3. Entre en **Security & privacy**.
4. Pulse **Device unlock**.
5. Entre en **Screen lock**.
6. Seleccione **PIN** o **Password**.
7. Configure:

`[PIN DEL OWNER]`

o la contraseña correspondiente.
8. Confirme la credencial.

**[CAPTURA 04 — Screen Lock]**

## Configuración de un usuario secundario

Para **cada usuario**:

1. Cambie al usuario.
2. Abra:
   `Settings → Security & privacy → Device unlock → Screen lock`
3. Configure una credencial propia:

`[PIN DEL USUARIO]`

4. Confírmela.
5. Repita el proceso con los demás usuarios.

## Configuración recomendada

Cada usuario debe tener su **propia credencial**.

No reutilice innecesariamente el mismo PIN entre perfiles.

## Qué cambia al configurarlo

Cada perfil queda protegido por su propia credencial y por sus propias claves de cifrado.

## Advertencias

> ⚠️ **ADVERTENCIA**
>
> No olvide el PIN o Password de un usuario. Credential Routing no sustituye la credencial Android real: solamente selecciona el usuario al que debe dirigirse esa credencial.

## Cómo comprobar que quedó correctamente configurado

1. Entre en el usuario.
2. Bloquee el teléfono.
3. Intente desbloquear utilizando únicamente la credencial que corresponde a ese perfil mediante el flujo configurado.
4. Compruebe que una credencial incorrecta no desbloquea el perfil.

---

# 5. Scramble PIN Input Layout

## ¿Qué es?

**Scramble PIN input layout** cambia la posición de los números del teclado cada vez que se presenta el teclado de PIN.

GrapheneOS incorpora esta función para dificultar que otra persona deduzca el PIN observando la posición de los toques.

## ¿Para qué sirve?

Reduce la utilidad de:

* Observación de movimientos.
* Marcas de dedos.
* Memorización de posiciones.
* Algunas formas de shoulder surfing.

## Ruta desde Settings

Para un PIN principal:

`Settings → Security & privacy → Device unlock → ⚙ junto a Screen lock → Scramble PIN input layout`

La ruta ha sido confirmada en la interfaz de GrapheneOS.

## Configuración paso a paso

1. Entre en el perfil que desea configurar.
2. Abra **Settings**.
3. Entre en **Security & privacy**.
4. Pulse **Device unlock**.
5. Pulse el icono **⚙** situado junto a **Screen lock**.
6. Active **Scramble PIN input layout**.

**[CAPTURA 05 — Scramble PIN]**

7. Bloquee el teléfono.
8. Abra el teclado de PIN.
9. Observe la posición de los números.
10. Vuelva a bloquear y abrir.
11. Confirme que el orden ha cambiado.

## Configuración recomendada

**Enabled**

Debe revisarse dentro de cada usuario.

## Qué cambia al activarla

Las posiciones de `0–9` dejan de permanecer fijas.

## Advertencias

El usuario debe leer los números en lugar de depender únicamente de memoria muscular.

## Cómo comprobar que quedó correctamente configurada

Bloquee y abra el teclado varias veces. Las posiciones numéricas deben cambiar.

---

# 6. Second-factor PIN

## ¿Qué es?

GrapheneOS permite utilizar:

`Fingerprint + Second-factor PIN`

para completar un desbloqueo secundario.

Esto permite mantener una contraseña principal fuerte y utilizar huella + un PIN más cómodo durante el uso cotidiano.

## ¿Para qué sirve?

Añade un segundo factor después de una huella válida.

## Ruta desde Settings

`Settings → Security & privacy → Device unlock → Fingerprint unlock → [AUTENTICARSE] → Second-factor PIN`

## Configuración paso a paso

1. Configure primero **Fingerprint unlock**.
2. Entre en su configuración.
3. Autentíquese.
4. Abra **Second-factor PIN**.
5. Configure el PIN.
6. Dentro de esa misma pantalla active, si lo desea:
   **Scramble PIN input layout**.

## Configuración recomendada

Utilizarlo cuando se quiera combinar una **Password fuerte** como credencial principal con la comodidad de huella + PIN.

## Qué cambia al activarla

Una huella correcta por sí sola ya no completa el desbloqueo: se necesita además el Second-factor PIN.

## Advertencias

No confundir:

| Credencial        | Función                                       |
| ----------------- | --------------------------------------------- |
| PIN principal     | Desbloqueo principal y protección del usuario |
| Second-factor PIN | Segundo factor después de fingerprint         |
| SIM PIN           | Protege la SIM/eSIM                           |
| Duress PIN        | Credencial destructiva de emergencia          |

## Cómo comprobarlo

1. Bloquee el teléfono.
2. Utilice una huella registrada.
3. Compruebe que se solicita el Second-factor PIN.
4. Confirme que el PIN correcto completa el desbloqueo.

---

# 7. Credential Routing

> ℹ️ **FUNCIÓN DISPONIBLE EN ESTA CONFIGURACIÓN DE GRAPHENEOS**

Credential Routing no es una función estándar de GrapheneOS. Forma parte de esta build personalizada.

La build `2026082001 user` contiene una modificación de Settings y SystemUI para configurar y utilizar esta función.

## ¿Qué es?

Credential Routing permite utilizar una pantalla de bloqueo neutral donde una entrada contiene:

`PREFIX + PIN ANDROID REAL`

El **Prefix** determina a qué usuario debe dirigirse la autenticación.

La parte restante continúa siendo el PIN real configurado para ese usuario.

## ¿Para qué sirve?

Permite seleccionar y desbloquear diferentes usuarios sin tener que mostrar un selector de usuarios tradicional en la pantalla bloqueada.

## Cómo funciona conceptualmente

`Entrada del usuario`

↓

`Credential Routing lee el Prefix`

↓

`El Prefix identifica al usuario destino`

↓

`El sistema cambia al usuario correspondiente`

↓

`El PIN restante se verifica como credencial Android normal de ese usuario`

La implementación del proyecto está diseñada para que el Prefix seleccione el usuario, mientras que el PIN real continúe siendo validado por los mecanismos normales de Android.

## Ruta desde Settings

Desde **Owner**:

`Settings → System → Multiple users → [Credential routing — CONFIRMAR EN LA INTERFAZ DE GRAPHENEOS]`

El nombre de la pantalla personalizada **Credential routing** está confirmado en la build actual, pero debe verificarse visualmente la posición exacta de la entrada antes de publicar una versión impresa definitiva del manual.

## Configuración paso a paso

1. Entre en **Owner**.
2. Abra **Settings**.
3. Entre en **System**.
4. Abra **Multiple users**.
5. Abra la pantalla personalizada **Credential routing**.

**[CAPTURA 06 — Credential Routing]**

6. Compruebe que aparecen los usuarios que desea configurar.
7. Asigne un **Prefix único** a cada usuario.
8. Active Credential Routing mediante el control disponible en la pantalla.
9. Revise nuevamente todas las asignaciones antes de salir.
10. Bloquee el dispositivo.
11. Compruebe cada usuario de manera individual.

> ℹ️ **INFORMACIÓN**
>
> En la build actual **no existe una opción visible independiente que el usuario deba buscar llamada “Hide user switcher”**. La ocultación de las superficies de cambio de usuario forma parte de la lógica personalizada ya incorporada.

## Configuración recomendada

* Un Prefix diferente por usuario.
* No reutilizar Prefix.
* Todos los usuarios deben tener Screen Lock configurado.
* Configurar primero Owner.
* Probar cada ruta antes de entregar el teléfono.

## Qué cambia al activarla

La pantalla bloqueada puede dirigir la autenticación al usuario correspondiente según el Prefix introducido.

## Advertencias

> ⚠️ **ADVERTENCIA**
>
> Credential Routing **no sustituye el PIN real**.
>
> El Prefix no debe considerarse una contraseña adicional.
>
> La seguridad criptográfica continúa dependiendo principalmente de la credencial Android real del usuario.

No documente que un PIN sin Prefix funciona en la pantalla neutral a menos que ese comportamiento se haya comprobado específicamente en la build instalada.

## Cómo comprobar que quedó correctamente configurada

Para cada usuario:

1. Bloquee el teléfono.
2. Introduzca estructuralmente:

`[PREFIX CONFIGURADO][PIN DEL USUARIO]`

3. Compruebe que se abre el usuario correcto.
4. Bloquee nuevamente.
5. Pruebe otro usuario.
6. Introduzca deliberadamente un PIN incorrecto y confirme que no desbloquea.
7. Introduzca un Prefix no configurado y confirme que no desbloquea.

---

# 8. Credential Routing Prefix

## ¿Qué es?

El **Prefix** es la parte inicial de la entrada utilizada por Credential Routing para determinar qué usuario debe recibir la credencial.

## ¿Para qué sirve?

Permite que una única pantalla de bloqueo pueda diferenciar entre distintos usuarios.

## Dónde se configura

`Settings → System → Multiple users → [Credential routing — CONFIRMAR EN LA INTERFAZ DE GRAPHENEOS]`

## Configuración paso a paso

1. Abra **Credential routing** desde Owner.
2. Seleccione el usuario que desea configurar.
3. Introduzca:

`[PREFIX CONFIGURADO]`

4. Guarde o confirme utilizando el control presentado por la interfaz.

**[CAPTURA 07 — Prefix]**

5. Repita para cada usuario.
6. Compruebe que ningún usuario comparte el mismo Prefix.

## Formato

La implementación de este proyecto utiliza un **Prefix numérico de dos dígitos**.

No documentar valores reales en copias del manual entregadas a terceros.

## Configuración recomendada

Utilizar un Prefix diferente por usuario y mantener un registro administrativo seguro cuando sea necesario.

## Qué cambia al configurarlo

Credential Routing dispone de la asociación necesaria para dirigir una entrada al usuario seleccionado.

## Advertencias

El Prefix por sí solo:

* No desbloquea datos.
* No sustituye el PIN.
* No debe tratarse como la parte secreta principal de la credencial.

## Cómo comprobarlo

Introduzca:

`[PREFIX CONFIGURADO][PIN DEL USUARIO]`

y confirme que se abre exclusivamente el usuario asociado.

---

# 9. Comportamiento de Credential Routing después de un reinicio

En esta build personalizada existe una restricción deliberada después de un reinicio.

## Procedimiento

1. Reinicie el dispositivo.
2. Desbloquee primero **Owner** utilizando su ruta configurada.
3. Una vez dentro de Owner, vuelva a bloquear el dispositivo.
4. A partir de ese momento utilice las rutas de los usuarios secundarios.

Antes del primer desbloqueo de Owner, las rutas de usuarios secundarios no deben funcionar. Este comportamiento forma parte de la implementación validada del proyecto.

> ℹ️ **INFORMACIÓN**
>
> Esto coincide con el papel especial de Owner durante el arranque. No significa que Owner obtenga acceso a los datos privados de los perfiles secundarios.

---

# 10. Duress PIN / Password

> ⛔ **BORRADO IRREVERSIBLE**
>
> Introducir el Duress PIN o Duress Password configurado en un campo compatible provoca un **borrado irreversible del dispositivo**.
>
> El borrado incluye los datos del teléfono y las eSIM instaladas.
>
> El proceso no requiere reinicio y no puede interrumpirse una vez iniciado.

## ¿Qué es?

GrapheneOS incorpora una credencial especial de emergencia denominada:

* **Duress PIN**
* **Duress Password**

Su objetivo no es desbloquear el teléfono, sino iniciar un borrado irreversible cuando se introduce en un campo donde el sistema solicita una credencial del dispositivo.

## ¿Para qué sirve?

Está diseñada para situaciones en las que el usuario necesita disponer de una credencial que desencadene inmediatamente el borrado del dispositivo.

## Ruta desde Settings

Debe configurarse desde **Owner**:

`Settings → Security & privacy → Device unlock → Duress Password`

Ruta oficial confirmada por GrapheneOS.

## Configuración paso a paso

1. Entre en **Owner**.
2. Abra **Settings**.
3. Entre en **Security & privacy**.
4. Pulse **Device unlock**.
5. Abra **Duress Password**.

**[CAPTURA 08 — Duress PIN / Password]**

6. Lea completamente la advertencia presentada por el sistema.
7. Configure el **Duress PIN**.
8. Configure el **Duress Password**.
9. Guarde la configuración.

GrapheneOS exige configurar ambos para contemplar perfiles que pueden utilizar diferentes métodos de desbloqueo.

## Diferencias importantes

### PIN normal

Desbloquea el usuario correspondiente.

### Duress PIN

Inicia el borrado cuando se introduce en un campo de PIN de credencial compatible.

También funciona como Duress cuando se introduce en lugar del Second-factor PIN de fingerprint.

### SIM PIN

Protege la SIM.

Introducir el Duress PIN como SIM PIN **no activa actualmente el Duress wipe**.

### Duress Password

Equivalente destructivo utilizado en campos de Password.

## Configuración recomendada

Configurarla únicamente cuando:

* El usuario comprende perfectamente su efecto.
* Existe una política clara de uso.
* No se almacena la credencial junto al teléfono.
* La credencial no coincide con la credencial real.

## Qué cambia al activarla

El sistema comienza a reconocer la credencial Duress en los campos de autenticación compatibles.

## Advertencias

> ⛔ **BORRADO IRREVERSIBLE**
>
> No introduzca la credencial real de Duress “para ver si funciona”.
>
> No existe una prueba inocua del efecto final.

Si el Duress PIN/Password coincide exactamente con la credencial real de desbloqueo, GrapheneOS da prioridad a la credencial real y no realiza el borrado.

## Cómo comprobar que quedó configurada

En un teléfono de producción, la comprobación debe limitarse a:

1. Abrir nuevamente **Duress Password**.
2. Comprobar que la función aparece configurada.
3. **No introducir la credencial Duress en ningún campo de autenticación.**

---

# 11. Integración de Credential Routing con Duress

> ℹ️ **FUNCIÓN DISPONIBLE EN ESTA CONFIGURACIÓN DE GRAPHENEOS**

La arquitectura personalizada permite que Credential Routing dirija una entrada al usuario correspondiente antes de que la credencial restante sea procesada mediante la autenticación normal.

Conceptualmente:

`Credencial introducida`

↓

`Credential Routing`

↓

`Detección del Prefix`

↓

`Identificación del usuario`

↓

`Verificación normal de la credencial`

↓

`Acción correspondiente`

En el caso de Duress, la credencial especial debe continuar llegando al mecanismo oficial de Duress de GrapheneOS. No debe implementarse un borrado independiente dentro de Credential Routing.

## Procedimiento general

1. Configure correctamente **Credential Routing**.
2. Configure una ruta válida para Owner.
3. Configure el **Prefix** correspondiente.
4. Configure oficialmente **Duress PIN / Password** desde Owner.
5. Revise visualmente que ambas funciones estén activas.
6. Documente para el administrador la sintaxis de producción únicamente después de haberla validado en un dispositivo de laboratorio.

**[DOCUMENTAR AQUÍ LA SINTAXIS EXACTA DEL PREFIX PARA DURESS]**

> ⛔ **BORRADO IRREVERSIBLE**
>
> No completar ese marcador utilizando valores reales en una copia pública del manual.

---

# 12. Cómo verificar Duress de forma segura

Una prueba funcional real debe realizarse **exclusivamente en un teléfono de laboratorio**.

El dispositivo debe:

* No contener información importante.
* No contener cuentas necesarias.
* No contener una eSIM que deba conservarse.
* Estar preparado para un factory reset.
* Tener respaldada cualquier información que deba conservarse.

En un teléfono de producción, la verificación termina en comprobar visualmente que Duress aparece configurado.

---

# 13. Auto Reboot

## ¿Qué es?

**Auto Reboot** reinicia automáticamente un dispositivo bloqueado cuando ningún perfil ha sido desbloqueado correctamente durante el período configurado.

Cada vez que el teléfono se bloquea comienza una cuenta regresiva. Si cualquier perfil se desbloquea correctamente, el temporizador se cancela y volverá a comenzar en el siguiente bloqueo.

## ¿Para qué sirve?

Permite devolver automáticamente los datos a un estado de mayor protección cuando el teléfono queda bloqueado y desatendido durante un período prolongado.

## Ruta desde Settings

Desde Owner:

`Settings → Security & privacy → Exploit protection → Auto reboot`

Esta pantalla se administra desde Owner, aunque el comportamiento afecta al dispositivo.

## Configuración paso a paso

1. Entre en **Owner**.
2. Abra **Settings**.
3. Entre en **Security & privacy**.
4. Pulse **Exploit protection**.
5. Entre en **Auto reboot**.

**[CAPTURA 09 — Auto Reboot]**

6. Seleccione el intervalo que corresponda a la política de seguridad.
7. Salga de Settings.

## Intervalos

GrapheneOS permite configurar Auto Reboot entre:

**10 minutos y 72 horas**

o desactivarlo.

El valor predeterminado de GrapheneOS es **18 horas**.

> ℹ️ **INFORMACIÓN**
>
> Consulte el selector de **Auto reboot** para ver los intervalos intermedios disponibles en esta versión. No deben documentarse intervalos que no aparezcan realmente en la interfaz.

## Configuración recomendada

Depende del equilibrio deseado.

**Intervalo corto:** mayor protección cuando el teléfono queda desatendido.

**Intervalo largo:** mayor comodidad y menor probabilidad de tener que introducir la credencial principal.

## Qué cambia al activarla

Si transcurre el período completo sin un desbloqueo correcto, el dispositivo se reinicia.

No realiza un factory reset.

## Advertencias

Auto Reboot y Duress son funciones completamente distintas:

* **Auto Reboot:** reinicia.
* **Duress:** borra.

## Cómo comprobarlo

1. Abra nuevamente **Auto reboot**.
2. Compruebe el valor seleccionado.
3. No es necesario esperar todo el intervalo como parte de una entrega rutinaria.

---

# 14. Before First Unlock — BFU

## ¿Qué es?

**BFU** significa **Before First Unlock**.

Describe el estado del teléfono después de encenderse o reiniciarse, antes de introducir por primera vez la credencial principal.

### Teléfono encendido y ya desbloqueado

El usuario ya introdujo su PIN o Password desde el último arranque.

### Teléfono recién reiniciado

Todavía no se introdujo la credencial principal.

En este segundo estado, una mayor parte del material necesario para acceder a los datos sensibles continúa protegida.

## Relación con Auto Reboot

Auto Reboot intenta devolver automáticamente un teléfono desatendido a este estado mediante un reinicio.

## Relación con Credential Routing

Después de un reboot de esta build personalizada:

1. Desbloquear Owner.
2. Volver a bloquear.
3. Después utilizar las rutas secundarias.

---

# 15. USB-C Port

## ¿Qué es?

GrapheneOS incorpora controles para reducir los ataques que podrían realizarse mediante el puerto USB-C cuando el teléfono está bloqueado.

## ¿Para qué sirve?

Permite decidir cuándo el puerto puede realizar transferencia de datos y cuándo queda limitado.

## Ruta desde Settings

En la interfaz actual:

`Settings → Security & privacy → Exploit protection → USB-C port`

La documentación de GrapheneOS utiliza también la ruta abreviada `Settings → Security → Exploit protection`; el nombre visual puede variar ligeramente con la versión de Settings.

## Configuración paso a paso

1. Abra **Settings**.
2. Entre en **Security & privacy**.
3. Pulse **Exploit protection**.
4. Abra **USB-C port**.

**[CAPTURA 10 — USB-C Port]**

5. Seleccione el modo deseado.

## Opciones

### Off

Deshabilita la funcionalidad del puerto mientras el sistema está iniciado, según las restricciones de esta función.

### Charging-only

Permite carga, pero no conexiones de datos.

### Charging-only when locked

Al bloquear el teléfono, restringe nuevas conexiones a carga.

Es la configuración predeterminada de GrapheneOS.

### Charging-only when locked, except before first unlock

Aplica una política distinta durante BFU.

Utilícela únicamente si comprende la diferencia y necesita esa compatibilidad.

### On

Mantiene la funcionalidad de datos disponible.

## Configuración recomendada

**Charging-only when locked**

para un buen equilibrio entre funcionalidad y seguridad.

## Qué cambia al activarla

Se reduce la superficie de ataque accesible a través de USB-C mientras el teléfono está bloqueado.

## Advertencias

Modos más restrictivos pueden afectar:

* Accesorios USB.
* Android Auto por cable.
* Transferencia de archivos.
* Dispositivos externos.
* Depuración.

## Cómo comprobarlo

1. Bloquee el teléfono.
2. Conecte un ordenador o accesorio de datos.
3. Confirme que se comporta según el modo seleccionado.

---

# 16. Storage Scopes

## ¿Qué es?

**Storage Scopes** es una función de GrapheneOS que puede sustituir permisos amplios de almacenamiento.

La aplicación puede creer que recibió el permiso solicitado, mientras que el sistema limita lo que realmente puede leer.

## ¿Para qué sirve?

Evita conceder a una aplicación acceso a todos los archivos o medios cuando solo necesita unos pocos.

## Ruta desde Settings

La entrada depende del permiso de almacenamiento que solicite la aplicación.

Ruta general:

`Settings → Apps → [APP] → Permissions → [Files / Photos and videos / Music and audio] → Storage Scopes`

Después de activarlo también puede aparecer una entrada directa:

`App info → Storage Scopes`

## Configuración paso a paso

1. Abra **Settings**.
2. Entre en **Apps**.
3. Abra la aplicación.
4. Pulse **Permissions**.
5. Abra el permiso de archivos o medios solicitado.
6. Seleccione **Storage Scopes**.
7. No conceda acceso adicional si la aplicación no lo necesita.
8. Si necesita un archivo o carpeta concreta, añádalo mediante el selector.
9. Guarde la selección.

## Configuración recomendada

Utilizar **Storage Scopes** siempre que una aplicación pueda funcionar sin acceso completo al almacenamiento.

## Qué cambia al activarla

La app puede seguir creando sus propios archivos, pero no obtiene acceso general a archivos creados por otras aplicaciones. Se pueden autorizar excepciones concretas.

## Advertencias

Si una aplicación con Storage Scopes se desinstala y vuelve a instalar, puede perder el acceso a archivos creados por su instalación anterior y necesitar que el usuario los vuelva a seleccionar.

## Cómo comprobarlo

Abra:

`App info → Storage Scopes`

y revise la lista de archivos o carpetas permitidos.

### Ejemplo

Una aplicación para editar una imagen no necesita ver todas las fotografías.

Autorice únicamente:

`[IMAGEN NECESARIA]`

en lugar de toda la biblioteca.

---

# 17. Contact Scopes

## ¿Qué es?

**Contact Scopes** permite presentar a una aplicación únicamente determinados contactos o datos de contacto, en lugar de conceder acceso a toda la agenda.

## ¿Para qué sirve?

Reduce la cantidad de información personal que una aplicación puede leer.

## Ruta desde Settings

`Settings → Apps → [APP] → Permissions → Contacts → Contact Scopes`

También puede aparecer una entrada directa **Contact Scopes** en App info después de configurarlo.

## Configuración paso a paso

1. Abra la aplicación en **Settings → Apps**.
2. Pulse **Permissions**.
3. Abra **Contacts**.
4. Configure **Contact Scopes**.
5. Seleccione:

   * Contactos concretos.
   * Datos concretos de contacto.
   * Grupos/labels cuando corresponda.
6. Confirme.

## Configuración recomendada

Permitir únicamente los contactos estrictamente necesarios.

## Qué cambia al activarla

La aplicación cree disponer del permiso de contactos, pero GrapheneOS filtra qué información puede leer.

La escritura de contactos queda bloqueada con Contact Scopes.

## Advertencias

Una aplicación puede conservar información que obtuvo **antes** de activar Contact Scopes.

## Cómo comprobarlo

Regrese a **Contact Scopes** y revise la lista autorizada.

### Ejemplo — Aplicación de mensajería

Si solo necesita comunicarse con tres personas, autorice esos tres contactos en lugar de toda la agenda.

---

# 18. Network Permission

## ¿Qué es?

GrapheneOS añade un permiso **Network** para bloquear el acceso directo e indirecto de una aplicación a las redes disponibles, incluyendo localhost.

## ¿Para qué sirve?

Permite utilizar aplicaciones que no necesitan Internet sin permitirles comunicarse con servidores externos.

## Ruta desde Settings

`Settings → Apps → [APP] → Permissions → Network`

## Configuración paso a paso

1. Abra **Settings**.
2. Entre en **Apps**.
3. Seleccione la aplicación.
4. Pulse **Permissions**.
5. Abra **Network**.
6. Permita o deniegue el acceso.

También puede revisarse durante la instalación de aplicaciones, ya que GrapheneOS muestra este control en el proceso de instalación.

## Configuración recomendada

**Desactivado** para aplicaciones que no necesitan Internet.

Ejemplos posibles:

* Calculadora offline.
* Visor de documentos offline.
* Herramientas locales.
* Determinadas aplicaciones de notas.

## Qué cambia al desactivarlo

GrapheneOS presenta a la aplicación la red como no disponible en lugar de simplemente dejar que las conexiones fallen.

## Advertencias

Puede dejar de funcionar:

* Sincronización.
* Notificaciones push.
* Inicio de sesión.
* Descarga de contenido.
* Licencias en línea.

## Cómo comprobarlo

Abra la aplicación y confirme que sus funciones locales continúan funcionando y que las funciones en línea no tienen conectividad.

---

# 19. Sensors Permission

## ¿Qué es?

El permiso **Sensors** de GrapheneOS controla sensores que Android normalmente no protege con permisos individuales, entre ellos:

* Accelerometer.
* Gyroscope.
* Compass.
* Barometer.
* Thermometer.
* Otros sensores similares.

No sustituye los permisos separados de **Camera**, **Microphone**, **Body Sensors** o **Activity Recognition**.

## ¿Para qué sirve?

Reduce el acceso innecesario de aplicaciones a sensores físicos del teléfono.

## Ruta desde Settings

Por aplicación:

`Settings → Apps → [APP] → Permissions → Sensors`

Para cambiar el comportamiento predeterminado de nuevas aplicaciones:

`Settings → Security & privacy → More security & privacy → Allow Sensors permission to apps by default`

## Configuración paso a paso

1. Abra la aplicación en **Settings → Apps**.
2. Pulse **Permissions**.
3. Abra **Sensors**.
4. Desactive el permiso si la aplicación no lo necesita.
5. Pruebe la aplicación.

## Configuración recomendada

Para aplicaciones instaladas por el usuario, negar Sensors cuando no sea necesario.

No modificar indiscriminadamente permisos de aplicaciones del sistema.

## Qué cambia al bloquearlo

La aplicación recibe datos neutralizados o deja de recibir eventos de esos sensores.

## Advertencias

Algunas aplicaciones pueden necesitar sensores para:

* Orientación.
* Navegación.
* Detección de movimiento.
* Funciones específicas del hardware.

## Cómo comprobarlo

Utilice normalmente la aplicación. GrapheneOS también puede mostrar una notificación cuando una app intenta utilizar sensores que tiene bloqueados.

---

# 20. User Profiles

## ¿Qué son?

Los perfiles de usuario son espacios aislados dentro del mismo teléfono.

Cada uno dispone de sus propias aplicaciones, datos, configuración y claves de cifrado.

## ¿Para qué sirven?

Permiten separar contextos como:

* Personal.
* Trabajo.
* Aplicaciones con Google Play.
* Aplicaciones de mayor riesgo.
* Uso temporal.

## Ruta desde Settings

`Settings → System → Multiple users`

## Crear un usuario

1. Entre en Owner.
2. Abra:
   `Settings → System → Multiple users`
3. Active **Multiple users** si fuera necesario.
4. Seleccione la opción para añadir un usuario.
5. Siga el Setup Wizard.
6. Cambie al nuevo usuario.
7. Configure su Screen Lock.
8. Configure sus aplicaciones y permisos.

## Credenciales independientes

Cada usuario debe configurarse dentro de:

`Settings → Security & privacy → Device unlock`

## Cambiar de usuario

En GrapheneOS estándar puede hacerse desde **Multiple users** y desde diferentes superficies del selector.

> ℹ️ **INFORMACIÓN**
>
> En esta build personalizada, las superficies visibles de cambio de usuario pueden estar ocultas deliberadamente cuando Credential Routing está habilitado.

## End Session

### ¿Qué es?

**End session** no es simplemente bloquear la pantalla.

Al finalizar la sesión de un usuario secundario:

* Sus aplicaciones se detienen.
* El perfil queda inactivo.
* Sus claves de cifrado son purgadas de memoria y registros de hardware.

### Configuración recomendada

Utilizar **End session** cuando un perfil sensible ya no necesita permanecer funcionando.

## Cómo comprobarlo

Después de finalizar la sesión, vuelva a ese perfil. Deberá iniciar nuevamente su sesión mediante la credencial correspondiente.

---

# 21. Two-Factor Fingerprint Unlock

## ¿Qué es?

Combina:

`Fingerprint + Second-factor PIN`

para el desbloqueo secundario.

## Ruta

`Settings → Security & privacy → Device unlock → Fingerprint unlock`

## Configuración paso a paso

1. Configure una credencial principal.
2. Registre la huella.
3. Entre en **Fingerprint unlock**.
4. Configure **Second-factor PIN**.
5. Active su Scramble PIN si lo desea.
6. Bloquee el teléfono.
7. Realice la prueba.

## Configuración recomendada

Especialmente útil con:

**Password fuerte + Fingerprint + Second-factor PIN**

## Qué cambia

Una huella válida requiere también el PIN secundario.

## Advertencias

Una huella sigue siendo un mecanismo secundario. El sistema exigirá periódicamente la credencial principal y la necesita después del arranque.

GrapheneOS limita a cinco los intentos fallidos totales de fingerprint.

## Verificación

Huella correcta → aparece Second-factor PIN → PIN correcto → desbloqueo.

---

# 22. LTE-only Mode

## ¿Qué es?

Permite limitar la conexión móvil a LTE, deshabilitando 2G, 3G y 5G.

## ¿Para qué sirve?

Su objetivo principal es reducir superficie de ataque al evitar grandes cantidades de código de protocolos más antiguos y más recientes. No está diseñado como una solución para hacer confidenciales las llamadas telefónicas tradicionales.

## Ruta desde Settings

`Settings → Network & internet → SIMs → [SIM] → Preferred network type`

## Configuración paso a paso

1. Abra **Settings**.
2. Entre en **Network & internet**.
3. Pulse **SIMs**.
4. Seleccione la SIM.
5. Abra **Preferred network type**.
6. Seleccione la opción LTE correspondiente.

## Configuración recomendada

Utilizar solamente cuando el operador proporciona LTE fiable y VoLTE funciona correctamente.

## Qué cambia

El teléfono deja de utilizar 2G, 3G y 5G.

## Advertencias

> ⚠️ **ADVERTENCIA**
>
> Las llamadas tradicionales en LTE-only requieren **VoLTE**, o **VoWiFi** mediante Wi-Fi.
>
> Si las llamadas dejan de funcionar, desactive LTE-only.

## Cómo comprobarlo

1. Realice una llamada saliente.
2. Reciba una llamada.
3. Pruebe SMS.
4. Compruebe datos móviles.
5. Si alguno falla, revise compatibilidad con el operador.

---

# 23. System Updates

## ¿Qué es?

Las actualizaciones corrigen vulnerabilidades del sistema operativo, firmware, controladores y componentes incluidos.

En GrapheneOS oficial, el updater comprueba automáticamente actualizaciones aproximadamente cada seis horas cuando existe conectividad y las instala en segundo plano en el slot inactivo. Después solicita reiniciar.

## Ruta estándar

`Settings → System → System update`

## Configuración paso a paso — GrapheneOS oficial

1. Abra **Settings**.
2. Entre en **System**.
3. Abra **System update**.
4. Revise:

   * Estado de actualización.
   * Release channel.
   * Redes permitidas.
   * Requisitos de batería/carga.
   * Automatic reboot del updater, si corresponde.
5. Reinicie cuando la actualización instalada lo solicite.

## Configuración recomendada

Mantener el dispositivo actualizado tan pronto como sea razonablemente posible.

## Diferencia importante

### Auto Reboot de seguridad

`Settings → Security & privacy → Exploit protection → Auto reboot`

Reinicia un teléfono que permanece bloqueado durante demasiado tiempo.

### Automatic reboot del updater

Pertenece al proceso de actualización y permite que una actualización ya instalada complete el cambio de versión mediante un reinicio.

Son funciones diferentes.

## Advertencia para esta build personalizada

> ⚠️ **IMPORTANTE — BUILD PERSONALIZADA**
>
> La build `2026082001` utiliza modificaciones y firma propias.
>
> **No debe asumirse que puede instalar directamente los paquetes OTA oficiales de GrapheneOS.**
>
> El proyecto necesita mantener su propio proceso compatible de actualización, portar las modificaciones a nuevas bases y firmar las actualizaciones de forma compatible.
>
> **[CONFIRMAR MECANISMO DE ACTUALIZACIÓN DE ESTA BUILD]**

La documentación técnica del proyecto ya advierte que una build personalizada no debe tratarse como una release oficial para futuras actualizaciones.

## Cómo comprobar la versión

`Settings → About phone → Build number`

Para esta instalación debe corresponder a la build de producción entregada.

---

# 24. Sandboxed Google Play

## ¿Qué es?

GrapheneOS permite instalar las versiones oficiales de Google Play como **aplicaciones normales dentro del sandbox**, sin concederles los privilegios especiales que poseen en un sistema Android integrado con Google.

## ¿Para qué sirve?

Proporciona compatibilidad con aplicaciones que dependen de:

* Google Play services.
* Push notifications.
* Play Store.
* In-app purchases.
* APIs específicas de Google.

## Instalación

Dentro del perfil donde sea necesario:

1. Abra **App Store** de GrapheneOS.
2. Seleccione **Google Play services**.
3. Instálelo.
4. GrapheneOS instalará también **Google Play Store**.

## Ruta de configuración

`Settings → Apps → Sandboxed Google Play`

## Configuración recomendada

Instalarlo únicamente en los perfiles que realmente tengan aplicaciones dependientes de Google Play.

## Qué cambia

Las aplicaciones del **mismo perfil** pueden utilizar Google Play cuando lo necesiten.

Google Play instalado en un perfil no se vuelve automáticamente disponible en los demás.

## Advertencias

Los permisos continúan siendo permisos normales de aplicaciones. No conceda acceso que no sea necesario.

## Cómo comprobarlo

1. Abra **App Store**.
2. Confirme que Play services y Play Store están actualizados.
3. Abra:
   `Settings → Apps → Sandboxed Google Play`
4. Revise su configuración.

---

# 25. Vanadium

## ¿Qué es?

**Vanadium** es el navegador incluido por GrapheneOS y también proporciona la implementación WebView del sistema.

Está basado en Chromium con endurecimiento adicional de seguridad y privacidad.

## ¿Para qué sirve?

* Navegación web.
* WebView utilizado por aplicaciones.
* Reducción de superficie de ataque respecto a configuraciones menos endurecidas.

## Ruta

Abra **Vanadium** desde el launcher.

Para sus datos y permisos:

`Settings → Apps → Vanadium`

## Configuración paso a paso

1. Mantenga Vanadium actualizado.
2. Revise permisos.
3. No conceda **Location**, **Camera**, **Microphone** o **Sensors** salvo que los necesite.
4. Revise permisos de sitios dentro del navegador.

## Configuración recomendada

Utilizar Vanadium como navegador predeterminado salvo que exista un requisito específico para otro navegador.

## Qué cambia

Las páginas web y WebView utilizan el motor endurecido incluido por GrapheneOS.

## Advertencias

Desactivar funciones de sitios puede romper determinadas páginas.

## Cómo comprobarlo

Abra **App Store** y confirme que Vanadium no tiene actualizaciones pendientes.

---

# 26. Funciones adicionales recomendadas

## 26.1 VPN

### ¿Qué es?

Una VPN crea un túnel de red entre el perfil y el proveedor VPN.

### Ruta

`Settings → Network & internet → VPN → ⚙ junto a la VPN`

### Configuración

1. Instale/configure la VPN.
2. Entre en su engranaje.
3. Active **Always-on VPN** si desea conexión automática.
4. Active **Block connections without VPN** si desea impedir tráfico cuando el túnel no esté disponible.

### Recomendación

Para una política VPN estricta:

**Always-on VPN → ON**

**Block connections without VPN → ON**

### Advertencias

VPN se configura por perfil. Los perfiles secundarios y Private Space tienen configuraciones VPN separadas.

### Verificación

Desconecte temporalmente el servidor VPN y compruebe que no existe conectividad si **Block connections without VPN** está activo.

---

## 26.2 Private Space

### ¿Qué es?

Private Space es un espacio aislado para aplicaciones y datos, integrado en Android y soportado por GrapheneOS. GrapheneOS lo describe como un perfil anidado dentro de Owner.

### Ruta

`Settings → Security & privacy → Private space`

### Configuración

1. Entre en **Private space**.
2. Autentíquese.
3. Pulse **Set up**.
4. Elija si utilizar la credencial del dispositivo o una distinta.
5. Configure las aplicaciones necesarias.
6. Configure **Lock private space automatically**.

La ruta y el procedimiento están documentados para Android actual.

### Recomendación

Útil para aplicaciones sensibles que necesitan estar más integradas con Owner que un usuario secundario completo.

### Advertencias

> ⛔ **PÉRDIDA DE DATOS**
>
> Eliminar Private Space elimina las aplicaciones y sus datos locales. Android no incluye esos datos locales en la restauración normal de Private Space.

### Verificación

Bloquee Private Space y confirme que sus aplicaciones desaparecen de las superficies normales donde corresponde.

---

## 26.3 Secure App Spawning

### ¿Qué es?

Es una protección de GrapheneOS para endurecer la creación de procesos de aplicaciones.

Desde la release `2026071100`, GrapheneOS sustituyó el antiguo modelo por una implementación con **control por aplicación**. La base `2026081300` utilizada en este teléfono ya incluye ese cambio.

### Ruta

`Settings → Apps → [APP] → [Secure app spawning — CONFIRMAR UBICACIÓN EXACTA EN LA INTERFAZ]`

### Configuración

Mantenerlo activado salvo que una aplicación concreta tenga un problema de compatibilidad comprobado.

Después de modificarlo, la versión actual de GrapheneOS requiere reiniciar para aplicar el cambio.

### Recomendación

**Enabled**

### Advertencias

No desactivar protecciones de exploit como primera solución ante un problema de aplicación.

### Verificación

Reinicie después del cambio y compruebe que la aplicación funciona.

---

## 26.4 Exploit Protection

### ¿Qué es?

Agrupa controles de GrapheneOS diseñados para reducir superficie de ataque y dificultar la explotación de vulnerabilidades.

### Ruta

`Settings → Security & privacy → Exploit protection`

### Configuración

Mantenga los valores predeterminados salvo que exista una necesidad de compatibilidad concreta.

### Recomendación

No desactivar protecciones sin una causa documentada.

### Advertencias

Reducir endurecimientos puede mejorar compatibilidad con una aplicación defectuosa, pero reduce protección.

### Verificación

Revise que no se hayan cambiado opciones accidentalmente.

---

## 26.5 Fingerprint Security

### ¿Qué es?

GrapheneOS endurece el desbloqueo por huella limitándolo a cinco intentos totales fallidos.

### Ruta

`Settings → Security & privacy → Device unlock → Fingerprint unlock`

### Configuración

Registre únicamente dedos necesarios y combine con Second-factor PIN cuando la política lo requiera.

### Recomendación

Para máxima seguridad, use una credencial principal fuerte.

### Advertencias

Fingerprint es un mecanismo secundario.

### Verificación

Compruebe que los dedos no registrados no desbloquean.

---

## 26.6 App Permissions

### ¿Qué es?

Controla el acceso de cada app a información y hardware.

### Ruta

`Settings → Apps → [APP] → Permissions`

### Configuración

Revise individualmente:

* Camera.
* Microphone.
* Location.
* Contacts.
* Network.
* Sensors.
* Photos and videos.
* Nearby devices.

### Recomendación

Conceder únicamente lo necesario.

### Advertencias

Revocar permisos puede afectar funciones legítimas.

### Verificación

Utilice la app y conceda posteriormente únicamente lo que demuestre necesitar.

---

## 26.7 Auditor / Device Verification

### ¿Qué es?

GrapheneOS incluye herramientas para verificar el estado y autenticidad de una instalación compatible mediante su sistema de attestation.

### Ruta

Abra **Auditor** desde el launcher.

### Configuración

Siga el asistente de Auditor para la modalidad de verificación que vaya a utilizar.

### Recomendación

Útil para dispositivos administrados o cuando se necesite una comprobación independiente del estado del sistema.

### Advertencias

No confundir una verificación de integridad con un análisis antivirus.

### Verificación

Auditor debe completar satisfactoriamente la verificación configurada.

---

## 26.8 Camera Privacy

### ¿Qué es?

Los permisos Camera y Microphone controlan qué aplicaciones pueden utilizar estos sensores sensibles.

### Ruta por aplicación

`Settings → Apps → [APP] → Permissions → Camera`

y:

`Settings → Apps → [APP] → Permissions → Microphone`

### Configuración

Conceda **Allow only while using the app** cuando resulte apropiado.

### Recomendación

No conceder cámara o micrófono permanentemente a aplicaciones que no lo necesitan.

### Advertencias

Aplicaciones de llamadas, videollamadas y captura multimedia necesitan estos permisos para sus funciones.

### Verificación

Abra el permiso de la aplicación y confirme el estado seleccionado.

---

## 26.9 Location

### ¿Qué es?

Controla el acceso de aplicaciones a la ubicación.

### Ruta

`Settings → Location`

Por aplicación:

`Settings → Apps → [APP] → Permissions → Location`

### Configuración

Utilice el nivel mínimo necesario para cada app.

### Recomendación

Preferir acceso únicamente durante el uso cuando sea suficiente.

### Advertencias

Navegación y seguimiento en segundo plano pueden necesitar una política distinta.

### Verificación

Revise el Privacy Dashboard y los permisos de la aplicación.

---

## 26.10 Wi-Fi y Bluetooth Scanning

### ¿Qué es?

Permite realizar escaneos para servicios de ubicación incluso cuando los interruptores principales de Wi-Fi o Bluetooth están apagados.

GrapheneOS los desactiva de forma predeterminada.

### Ruta

`Settings → Location → Location services → Wi-Fi and Bluetooth scanning`

### Configuración recomendada

**Off** salvo que una función específica requiera estos escaneos.

### Qué cambia

Con ellos apagados, desactivar Wi-Fi o Bluetooth impide también este tipo de escaneo de ubicación.

### Advertencias

Algunos servicios de ubicación pueden perder precisión.

### Verificación

Confirme que ambos interruptores están en el estado deseado.

---

## 26.11 eSIM

### ¿Qué es?

GrapheneOS admite eSIM. Para añadir y administrar nuevas eSIM necesita activar temporal o permanentemente la función propietaria de gestión incluida de forma opcional.

### Ruta

`Settings → Network & internet → eSIM support`

### Configuración

1. Active **eSIM support**.
2. Realice la instalación o administración de la eSIM.
3. Manténgalo habilitado cuando sea necesario para gestionar una eSIM protegida por PIN.

### Recomendación

Mantenerlo según necesidades del operador y de administración.

### Advertencias

El Duress wipe elimina también las eSIM instaladas.

### Verificación

Compruebe que la línea eSIM aparece correctamente dentro de la configuración de red.

---

## 26.12 Notification Forwarding entre perfiles

### ¿Qué es?

GrapheneOS puede reenviar notificaciones de un usuario que continúa ejecutándose en segundo plano hacia el usuario actualmente activo.

### Ruta

Dentro del usuario que debe enviar sus notificaciones:

`Settings → System → Multiple users → Send notifications to current user`

La denominación puede variar ligeramente con la versión.

### Configuración

1. Entre en el perfil origen.
2. Abra **Multiple users**.
3. Active **Send notifications to current user**.
4. Cambie al usuario habitual.
5. Genere una notificación de prueba.

### Recomendación

Activarlo únicamente si se necesitan alertas de un perfil que permanece en segundo plano.

### Advertencias

Requiere que ese usuario continúe funcionando; **End session** detendrá sus aplicaciones.

### Verificación

Confirme que la notificación llega al usuario activo.

---

## 26.13 Install Available Apps

### ¿Qué es?

Permite a Owner hacer disponible en un usuario secundario una aplicación que ya está instalada en Owner, sin tener que volver a descargar el paquete. Los datos siguen siendo independientes.

### Ruta

Desde Owner:

`Settings → System → Multiple users → [USUARIO] → Install available apps`

### Configuración

1. Seleccione el usuario.
2. Pulse **Install available apps**.
3. Active las aplicaciones necesarias.

### Recomendación

Útil para preparar teléfonos de forma controlada.

### Advertencias

La aplicación se instala como una instancia independiente para ese usuario. Sus datos no se copian.

### Verificación

Cambie al usuario y compruebe que la aplicación aparece sin datos del Owner.

---

## 26.14 Restricción de instalación de aplicaciones

### ¿Qué es?

GrapheneOS permite a Owner impedir que un usuario secundario instale aplicaciones adicionales.

### Ruta

`Settings → System → Multiple users → [USUARIO] → [CONTROL DE INSTALACIÓN DE APPS — CONFIRMAR NOMBRE EXACTO]`

### Configuración

Instale primero las apps necesarias y después active la restricción.

### Recomendación

Útil para teléfonos entregados con una configuración cerrada.

### Advertencias

Puede impedir que el usuario instale aplicaciones legítimas posteriormente.

### Verificación

Desde el usuario secundario, compruebe que no puede instalar nuevas aplicaciones.

---

## 26.15 End Session

### ¿Qué es?

Finaliza completamente la sesión de un usuario secundario y devuelve sus claves de cifrado al estado de reposo.

### Ruta

Puede estar disponible mediante el menú de usuario o acciones del sistema.

En esta build personalizada determinadas superficies del selector se encuentran ocultas, por lo que la ubicación efectiva debe comprobarse:

**[CONFIRMAR EN LA INTERFAZ DE GRAPHENEOS]**

### Configuración recomendada

Utilizar después de terminar actividades sensibles en un usuario secundario cuando no necesite permanecer ejecutándose.

### Advertencias

No recibirá notificaciones ni ejecutará procesos en segundo plano después de End Session.

### Verificación

Al volver al perfil deberá iniciarse nuevamente su sesión.

---

# 27. Configuración recomendada rápida

| Función                  | Configuración recomendada               | Observaciones                               |
| ------------------------ | --------------------------------------- | ------------------------------------------- |
| Wi-Fi MAC                | **Use per-connection randomized MAC**   | Mayor privacidad                            |
| Screen Lock              | PIN aleatorio largo o Password          | Configurar por usuario                      |
| Scramble PIN             | **Enabled**                             | Por usuario                                 |
| Second-factor PIN        | Según política                          | Útil con Password fuerte                    |
| Auto Reboot              | Según política de seguridad             | 10 min–72 h / Off                           |
| USB-C Port               | **Charging-only when locked**           | Valor predeterminado de GrapheneOS          |
| Credential Routing       | **Enabled**, si se utilizará            | Función personalizada                       |
| Prefix                   | Único por usuario                       | No es la credencial secreta principal       |
| Duress PIN / Password    | Configurar con máxima precaución        | Borrado irreversible                        |
| Storage Scopes           | Utilizar cuando sea posible             | Limita archivos                             |
| Contact Scopes           | Utilizar cuando sea posible             | Limita agenda                               |
| Network Permission       | Revisar por aplicación                  | Bloquear si no necesita Internet            |
| Sensors Permission       | Bloquear si no es necesario             | Revisar por app                             |
| LTE-only                 | Solo con VoLTE compatible               | Puede afectar llamadas                      |
| VPN                      | Always-on + Block without VPN si aplica | Configurar por perfil                       |
| Wi-Fi/Bluetooth scanning | Off salvo necesidad                     | Privacidad                                  |
| Sandboxed Google Play    | Solo donde sea necesario                | Instalar por perfil                         |
| System updates           | Mantener al día                         | Build personalizada requiere proceso propio |

---

# 28. Checklist de entrega del teléfono

## Sistema

* [ ] Build correcta instalada.
* [ ] Bootloader bloqueado.
* [ ] Build number verificado.
* [ ] OEM unlocking desactivado.
* [ ] USB debugging desactivado.
* [ ] Autorizaciones ADB revocadas.

## Owner

* [ ] Screen Lock configurado.
* [ ] Scramble PIN revisado.
* [ ] Fingerprint revisado.
* [ ] Second-factor PIN revisado si corresponde.
* [ ] Duress PIN / Password configurado si corresponde.

## Usuarios secundarios

* [ ] Todos los usuarios necesarios creados.
* [ ] Cada usuario tiene credencial propia.
* [ ] Scramble PIN configurado en cada usuario.
* [ ] Aplicaciones necesarias instaladas.
* [ ] Permisos revisados.
* [ ] End Session explicado al usuario.

## Credential Routing

* [ ] Credential Routing configurado.
* [ ] Ruta Owner configurada.
* [ ] Prefix único para cada usuario.
* [ ] Ruta de cada usuario probada.
* [ ] PIN incorrecto probado.
* [ ] Prefix inexistente probado.
* [ ] Comportamiento Owner-first después de reboot probado.
* [ ] No existe un selector de usuarios visible no deseado.
* [ ] Usuario comprende que la entrada es `Prefix + PIN Android real`.

## Privacidad

* [ ] Wi-Fi en **Use per-connection randomized MAC**.
* [ ] Storage Scopes revisado.
* [ ] Contact Scopes revisado.
* [ ] Network Permission revisado.
* [ ] Sensors Permission revisado.
* [ ] Location revisada.
* [ ] Wi-Fi scanning revisado.
* [ ] Bluetooth scanning revisado.
* [ ] VPN revisada si corresponde.

## Seguridad

* [ ] Auto Reboot configurado.
* [ ] USB-C Port configurado.
* [ ] Exploit Protection revisado.
* [ ] Secure App Spawning mantenido activo salvo excepción documentada.
* [ ] Usuario informado sobre BFU.
* [ ] Usuario informado de que Duress produce un borrado irreversible.

## Actualizaciones

* [ ] Mecanismo de actualización de esta build personalizada documentado.
* [ ] Responsable de mantener nuevas builds definido.
* [ ] No se ha asumido compatibilidad directa con OTA oficiales de GrapheneOS.

---

# 29. Resumen de uso diario

Para un uso normal:

1. Despierte el teléfono.
2. En la pantalla de bloqueo introduzca:

`[PREFIX CONFIGURADO][PIN DEL USUARIO]`

3. El sistema dirigirá la autenticación al perfil correspondiente.
4. Utilice el teléfono normalmente.
5. Cuando termine de utilizar un perfil sensible, considere **End session**.
6. Después de un reinicio completo, desbloquee **Owner primero**.
7. Mantenga Wi-Fi, permisos y aplicaciones bajo las configuraciones recomendadas.

> ⛔ **RECORDATORIO FINAL SOBRE DURESS**
>
> **Duress PIN / Password no es un PIN alternativo de desbloqueo.**
>
> Es una credencial de borrado irreversible.
>
> Nunca debe probarse en un teléfono de producción.

---

# 30. Nota de control de versión

Este manual ha sido preparado específicamente para:

`Pixel 10 Pro (blazer)`

`Android 17`

`GrapheneOS base 2026081300`

`Custom build 2026082001 user`

GrapheneOS cambia con el tiempo. Antes de reutilizar este manual con una futura base, deben volver a verificarse las rutas de Settings y el funcionamiento de las funciones estándar.

Las instrucciones y restricciones de **Credential Routing** deben revisarse nuevamente si se modifica cualquiera de los parches de SystemUI o Settings utilizados por el proyecto. La documentación actual del proyecto confirma el modelo `PREFIX + PIN REAL`, el requisito de desbloquear Owner primero después de reboot y la ausencia de un ajuste visible separado para ocultar el selector.

**Fin del manual.**
