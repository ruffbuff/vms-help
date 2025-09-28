# Guía de Configuración de VMs para Gaming en VirtualBox

Esta guía te ayuda a configurar múltiples máquinas virtuales (VMs) para promociones de juegos y programas de referidos. Cada VM aparecerá como un dispositivo separado para sistemas externos, permitiéndote ejecutar múltiples instancias de juegos o campañas promocionales.

## Requisitos Previos

- **Requisitos Mínimos del Sistema:**
  - 16GB RAM (32GB recomendado para múltiples VMs)
  - 4+ núcleos de CPU
  - 80GB+ espacio libre en disco
  - Conexión a internet (WiFi o Ethernet)

## Paso 1: Descargar e Instalar VirtualBox

### 1.1 Descargar VirtualBox
1. Ve a [Descargas de VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Descarga **VirtualBox** para tu sistema operativo (Windows/Mac/Linux)
3. Descarga **VirtualBox Extension Pack** (misma página, "All supported platforms")

### 1.2 Instalar VirtualBox
1. Ejecuta el instalador de VirtualBox con configuración predeterminada
2. Completa la instalación y reinicia si es necesario

### 1.3 Instalar Extension Pack
1. Haz doble clic en el archivo `.vbox-extpack` descargado
2. O en VirtualBox: **Archivo → Preferencias → Extensiones → Agregar**
3. Acepta el acuerdo de licencia de Oracle
4. Reinicia VirtualBox

## Paso 2: Configurar Ajustes de VirtualBox

### 2.1 Configuración Inicial de VirtualBox
1. Abre VirtualBox
2. **Archivo → Preferencias → General:**
   - Establece "Carpeta de Máquina Predeterminada" en una unidad con mucho espacio
3. **Entrada:** Deja Tecla Host como Ctrl Derecho (o cambia según preferencia)

## Paso 3: Crear tu Primera Máquina Virtual

### 3.1 Crear Nueva VM
1. Haz clic en **"Nuevo"** en VirtualBox
2. **Nombre:** GameVM_1
3. **Tipo:** Microsoft Windows
4. **Versión:** Windows 10 o Windows 11 (64-bit)
5. Haz clic en **Siguiente**

### 3.2 Asignar Recursos
**Para sistemas con 32GB RAM:**
- **Memoria Base:** 8192 MB (8GB)
- **Procesadores:** 4 núcleos

**Para sistemas con 16GB RAM:**
- **Memoria Base:** 4096 MB (4GB)
- **Procesadores:** 2-4 núcleos

### 3.3 Crear Disco Duro Virtual
1. **Crear un disco duro virtual ahora**
2. **Tipo de archivo de disco duro:** VDI
3. **Almacenamiento:** Asignado dinámicamente
4. **Tamaño:** 80-100 GB
5. Haz clic en **Crear**

## Paso 4: Configurar VM para Gaming y Aislamiento de Red

### 4.1 Configuración de Pantalla
1. Selecciona tu VM → **Configuración → Pantalla:**
   - **Memoria de Video:** 128 MB (máximo)
   - **Controlador Gráfico:** VMSVGA o VBoxSVGA
   - **Habilitar Aceleración 3D:** ✓ (si está disponible)

### 4.2 Configuración de Red (CRÍTICO para el aislamiento)
1. **Configuración → Red → Adaptador 1:**
   - **Conectado a:** Adaptador Puente
   - **Nombre:**
     - **Para WiFi (portátiles):** Selecciona tu adaptador WiFi
     - **Para Ethernet (PCs de escritorio):** Selecciona tu adaptador Ethernet
   - **Avanzado → Dirección MAC:** Haz clic en el botón actualizar 🔄
   - **Cable conectado:** ✓

### 4.3 Optimización del Sistema
1. **Configuración → Sistema → Placa Base:**
   - **Habilitar I/O APIC:** ✓
2. **Configuración → Sistema → Procesador:**
   - **Habilitar PAE/NX:** ✓

### 4.4 Configuración de Almacenamiento
1. **Configuración → Almacenamiento:**
   - **Controlador IDE → Vacío**
   - Haz clic en el icono del disco → **Elegir archivo de disco**
   - Selecciona tu archivo ISO de Windows

## Paso 5: Instalar Windows

### 5.1 Iniciar Instalación
1. Haz clic en **Iniciar** (flecha verde)
2. Instala Windows normalmente
3. Completa la configuración de Windows con un nombre único de computadora (ej., "GamePC-1")

### 5.2 Instalar Guest Additions
1. En la VM en ejecución: **Dispositivos → Insertar imagen de CD de Guest Additions**
2. Abre **Este PC** → doble clic en **Unidad de CD (Guest Additions)**
3. Ejecuta **VBoxWindowsAdditions.exe** como administrador
4. Instala con configuración predeterminada
5. **Reinicia la VM**

### 5.3 Configurar Pantalla
Después del reinicio:
- **Ver → Redimensionar Automáticamente Pantalla del Invitado** ✓
- La pantalla ahora se redimensionará correctamente con la ventana

## Paso 6: Verificar Aislamiento de Red

### 6.1 Verificar Configuración de Red de la VM
En la VM, abre Símbolo del Sistema y ejecuta:
```cmd
ipconfig /all
```
Anota:
- **Dirección IPv4** (ej., 192.168.1.100)
- **Dirección Física (MAC)** (ej., 08-00-27-XX-XX-XX)

### 6.2 Comparar con el Sistema Anfitrión
En tu computadora principal, ejecuta el mismo comando:
```cmd
ipconfig /all
```

**Indicadores de éxito:**
- ✓ Direcciones IP diferentes (ej., Anfitrión: 192.168.1.50, VM: 192.168.1.100)
- ✓ Direcciones MAC diferentes
- ✓ Misma puerta de enlace predeterminada (IP del router)

### 6.3 Probar IP Externa
En el navegador de la VM, visita: https://whatismyipaddress.com/
- La IP externa puede ser la misma (normal para redes domésticas)
- Lo importante son las diferentes IPs internas y direcciones MAC

## Paso 7: Optimizar Rendimiento de VM para Gaming

### 7.1 Configuración de Rendimiento de Windows
En la VM:
1. **Sistema → Configuración avanzada del sistema → Rendimiento → Configuración**
2. Selecciona **"Ajustar para mejor rendimiento"**
3. **Opciones de Energía:** Configura en **"Alto rendimiento"**

### 7.2 Deshabilitar Servicios Innecesarios
- Deshabilitar temporalmente Windows Defender (para mejor rendimiento)
- Apagar actualizaciones automáticas durante el gaming
- Cerrar aplicaciones en segundo plano

## Paso 8: Crear VMs Adicionales

### 8.1 Clonar VM Existente
1. **Apaga** completamente la primera VM
2. **Clic derecho en VM → Clonar**
3. **Nombre:** GameVM_2
4. **Política de Dirección MAC:** ⚠️ **Generar nuevas direcciones MAC para todos los adaptadores de red**
5. **Tipo de Clonación:** Clonación completa
6. Haz clic en **Clonar**

### 8.2 Verificar Aislamiento de Nueva VM
1. Inicia la VM clonada
2. Ejecuta `ipconfig /all` - debería mostrar IP y MAC diferentes
3. Cambia nombre de computadora: **Configuración → Sistema → Acerca de → Renombrar este PC**

### 8.3 Aislamiento de Navegador (Importante)
Para cada VM, usa diferentes navegadores o borra todos los datos:
- **VM 1:** Chrome
- **VM 2:** Firefox
- **VM 3:** Edge
- O borrar todos los datos del navegador entre usos

## Paso 9: Mejores Prácticas para Promociones de Gaming

### 9.1 Gestión de VMs
- **Ejecutar VMs de una en una** para mejor rendimiento
- **Diferentes resoluciones de pantalla** por VM
- **Nombres únicos de computadora** para cada VM
- **Diferentes navegadores** o datos de navegador borrados

### 9.2 Consideraciones de Red
- Cada VM obtiene una IP única de tu router
- Las direcciones MAC deben ser diferentes (automático al clonar correctamente)
- Usar modos de navegación privado/incógnito
- Evitar software DNS/AdBlock ya que algunas promociones lo detectan

### 9.3 Gestión de Recursos
**Para sistemas de 32GB RAM:**
- Ejecutar 2-3 VMs simultáneamente (8GB cada una)
- O 4-5 VMs (4-6GB cada una)

**Para sistemas de 16GB RAM:**
- Ejecutar 1 VM a la vez (6-8GB)
- O 2 VMs (4GB cada una)

## Solución de Problemas

### FPS Bajo en Juegos
- Aumentar asignación de RAM de VM
- Asignar más núcleos de CPU
- Habilitar aceleración 3D si está disponible
- Cerrar programas innecesarios en sistema anfitrión

### Problemas de Red
- Verificar que Adaptador Puente esté seleccionado
- Verificar que se generen diferentes direcciones MAC
- Reiniciar router si las VMs obtienen la misma IP

### Aceleración 3D Deshabilitada
- Instalar Extension Pack
- Probar diferentes Controladores Gráficos (VBoxSVGA, VBoxVGA)
- Algunos hardware no soportan aceleración 3D de VM

## Notas Importantes

⚠️ **Descargo Legal:** Solo usa esta configuración para campañas promocionales legítimas que permitan múltiples cuentas. Siempre lee los términos de servicio.

⚠️ **Rendimiento:** Las VMs funcionan 30-50% más lento que sistemas nativos. Elige juegos en consecuencia.

⚠️ **Seguridad:** Cada VM está aislada pero comparte tu conexión a internet y dirección IP externa.

## Lista de Verificación de Configuración Rápida

- [ ] VirtualBox instalado
- [ ] Extension Pack instalado
- [ ] VM creada con 8GB RAM, 4 núcleos, 80GB disco
- [ ] Adaptador de red puente configurado
- [ ] Dirección MAC única generada
- [ ] Windows instalado y actualizado
- [ ] Guest Additions instalado
- [ ] Aislamiento de red verificado (IPs/MACs diferentes)
- [ ] Rendimiento optimizado
- [ ] VMs adicionales clonadas con nuevas direcciones MAC

---

**Éxito:** Cada VM aparecerá como una computadora separada para sistemas externos, perfecto para promociones de gaming y programas de referidos.