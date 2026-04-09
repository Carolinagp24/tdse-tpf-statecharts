<p align="center">
  <img src="./img/logo-fiuba.png" alt="Logo FIUBA" width="200">
</p>

<p align="center">
  <strong>UNIVERSIDAD DE BUENOS AIRES</strong><br>
  <strong>Facultad de Ingeniería</strong><br>
  <strong>86.65/TA134 Taller de Sistemas Embebidos</strong>
</p>

# Memoria del Trabajo Final: **Alarma Vecinal IoT**

<table align="center">
  <tr>
    <th>Autor</th>
    <th>Padrón</th>
  </tr>
  <tr>
    <td>Valentín Alexis Guirin</td>
    <td>107416</td>
  </tr>
  <tr>
    <td>Yerson Monzón Alayo</td>
    <td>104262</td>
  </tr>
  <tr>
    <td>Carolina Gonzales Peralta</td>
    <td>110804</td>
  </tr>
</table>

<p align="center">
  <em>Este trabajo fue realizado en la Ciudad Autónoma de Buenos Aires, entre diciembre de 2025 y marzo de 2026.</em>
</p>

---

## 📑 Índice General
1. [Resumen / Abstract](#resumen--abstract)
2. [Estado de Implementación](#estado-de-implementación)
3. [Arquitectura del Sistema](#arquitectura-del-sistema)
4. [Lógica de Control (FSM)](#lógica-de-control-fsm)
5. [Hardware y Módulos](#hardware-y-módulos)
6. [Diseño del Firmware](#diseño-del-firmware)
7. [Ensayos y Resultados](#ensayos-y-resultados)
8. [Conclusiones y Futuro](#conclusiones-y-futuro)

---

## 📝 Resumen / Abstract
**Resumen:** En el presente trabajo se diseñó e implementó una alarma vecinal para solucionar la problemática de inseguridad en barrios de la Ciudad de Buenos Aires. Mediante un módulo GSM y un botón de pánico, los usuarios pueden activar alertas sonoras y lumínicas. El sistema permite el mantenimiento vía BLE con doble factor de autenticación y gestión de whitelist en una memoria EEPROM externa.

**Abstract:** This paper describes the design and implementation of a neighborhood alarm system aimed at addressing security concerns in Buenos Aires. By utilizing a GSM module and a panic button, users can trigger audible and visual alerts. The system supports maintenance via BLE with dual-factor authentication and whitelist management using an external EEPROM.

---

##  Estado de Implementación


| Funcionalidad / Módulo | Estado | Nota Técnica |
| :--- | :---: | :--- |
| **Núcleo Base (STM32F103)** | 🟢 | Periféricos y SysTick configurados. |
| **Módulo GSM (SIM800L)** | 🟢 | Llamadas y envío de SMS operativos. |
| **Gestión BLE (HM-10)** | 🟡 | En fase de diseño del diagrama de estados . |
| **Memoria EEPROM (I2C)** | 🟢 | Lectura/Escritura de Whitelist estable. |
| **Sensor LDR** | 🟢 | Calibración de umbral nocturno lista. |
| **Botón de Pánico** | 🟢 | Interrupción externa configurada. |
| **Modo Bajo Consumo** | 🟢 |hecho |

> **Leyenda:** 🟢 Completo | 🟡 En Desarrollo | 🔴 Pendiente

---

##  Lógica de Control (FSM)
Aquí se detallan las máquinas de estados finitos que gobiernan el comportamiento del sistema.

### 4.1 FSM Principal (Sistema Global)
Gestiona el paso entre los modos de reposo, alerta activa y administración.

<p align="center">
  <img src="./img/fsm_main.png" alt="FSM Principal">
</p>

### 4.2 FSM Módulo GSM
Controla la inicialización del módulo, el registro en la red y la gestión de llamadas entrantes.

<p align="center">
  <img src="./img/fsm_gsm.png" alt="FSM GSM">
</p>

### 4.3 FSM Modo Administrador (BLE)
Lógica de autenticación y gestión de la base de datos de usuarios (Whitelist).

<p align="center">
  <img src="./img/fsm_admin.png" alt="FSM BLE">
</p>




## 📂 Diseño del Firmware
### 6.1 Diagramas de Secuencia
Los diagramas de secuencia ilustran la interacción temporal entre los módulos:

* **Activación GSM:** `(Imagen pendiente: ./img/seq_gsm.png)`
* **Activación Botón:** `(Imagen pendiente: ./img/seq_panic.png)`
* **Acceso Técnico:** `(Imagen pendiente: ./img/seq_ble.png)`

---

