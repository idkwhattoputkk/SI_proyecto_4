# 🎛️ Proyecto 4 – Sistemas de Interacción: Control de Audio MIDI
## Control de audio mediante Mrmr y Pure Data

Este proyecto implementa un **sistema de interacción** que permite la manipulación de sonido en **tiempo real** utilizando el protocolo **OSC (Open Sound Control)**. La comunicación se establece entre un dispositivo móvil (**iPhone** con la app **Mrmr OSC Controller**) y el entorno de programación visual **Pure Data (PD)** ejecutándose en macOS.

---

### 🎯 Objetivos del Proyecto
* Establecer una comunicación fluida **OSC** entre un dispositivo móvil y **Pure Data**.
* Controlar dinámicamente **parámetros de sonido** (frecuencia, volumen) usando *sliders* desde la aplicación **Mrmr**.
* Reproducir un **archivo de audio** (`.wav`) a distancia mediante un evento remoto (botón).

---

### ⚙️ Componentes y Mapeo
La interacción se basa en el siguiente mapeo de control:

| Componente | Origen (Mrmr OSC Controller) | Destino (Pure Data Patch) | Parámetro Controlado |
| :--- | :--- | :--- | :--- |
| **Slider 0** | Mensaje OSC | Frecuencia del Oscilador | Generación de tono |
| **Slider 1** | Mensaje OSC | Volumen General | Amplitud de la salida |
| **Botón 2** | Mensaje OSC (Evento) | Activador de Sample | Reproducción de `sample.wav` |

**Detalles de Software:**
* **Mrmr OSC Controller (iOS):** Aplicación de envío de mensajes OSC.
* **Pure Data Patch:** `mrmr_dj_final_fixed.pd`
    * Puerto de recepción **UDP**: `8000`
    * Funcionalidad: Recepción de OSC, conversión a señal de control, generación de audio (oscilador, control de volumen y *sample player*).

---

### 🚀 Guía de Ejecución

Para poner en marcha el sistema, sigue los siguientes pasos:

1.  **Conexión de Red:** Asegúrate de que el **iPhone** (con Mrmr) y el **Mac** (con PD) estén conectados a la **misma red Wi-Fi**.
2.  **Preparación de Pure Data:**
    * Abre Pure Data (versión *vanilla* es compatible).
    * Carga el *patch* **`mrmr_dj_final_fixed.pd`**.
    * Activa el **DSP** (**Audio ON**) en Pure Data.
3.  **Configuración de Mrmr (iPhone):**
    * En la aplicación Mrmr, configura los siguientes parámetros de conexión:
        * **Host:** La **IP local** de tu Mac (ej. `192.168.1.99`).
        * **Port:** `8000`.
4.  **Interacción:** Comienza a mover los *sliders* o presiona el **Botón 2** para interactuar con el sonido generado en Pure Data.

---

### 🧱 Estructura del Repositorio

├── README.md                 <-- Documentación actual
├── mrmr_dj_final_fixed.pd    <-- Archivo principal de Pure Data
└── sample.wav                <-- Archivo de audio requerido por el patch

---

### 📝 Notas Adicionales
* El *patch* de PD utiliza objetos de **desempaquetado** (`[unpack s f s f]` y `[unpack f s f]`) adaptados al formato de mensaje OSC específico enviado por la aplicación Mrmr.
* El archivo **`sample.wav`** debe estar en la misma carpeta que el *patch* y se carga automáticamente al abrirlo.
* **Compatibilidad:** Diseñado y probado en macOS con **Pure Data *vanilla***.

---

### 🧑‍🎓 Autor
**Joan Emmanuel Umaña Grajales**

Estudiante de Ingeniería de Sistemas. Proyecto desarrollado para la asignatura **Sistemas de Interacción**.