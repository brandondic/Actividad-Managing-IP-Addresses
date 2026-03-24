# 🌐 Guía Técnica: Redes e IPs para Developers

---

## 1. Conceptos Fundamentales

| Concepto | Definición simple | Nivel técnico breve | Ejemplo |
|----------|------------------|--------------------|---------|
| IP | La "matrícula" o dirección de tu dispositivo en internet. | Protocolo de capa 3 (Red) del modelo OSI para direccionamiento. | 192.168.1.1 |
| IPv4 | El estándar antiguo, usa números cortos. | Formato de 32 bits dividido en 4 octetos decimales. | 172.217.13.174 |
| IPv6 | El estándar nuevo, casi infinito y con letras. | Formato de 128 bits en ocho grupos hexadecimales. | 2001:db8::ff00:42 |

---

## 2. Tipos de IP (Clave para Desarrollo)

### 🔍 Comparativa Rápida

- **Pública vs. Privada**  
  - La Pública es la cara visible hacia internet (tu router).  
  - La Privada es interna y solo existe en tu red local (tu laptop, impresora, etc.).

- **Estática vs. Dinámica**  
  - La Estática es fija (servidores).  
  - La Dinámica cambia al reiniciar la conexión (usuarios finales).

### 📊 Tipos

| Tipo | ¿Qué es? | ¿Cuándo se usa? | Ejemplo real |
|------|---------|----------------|--------------|
| Pública | Identificador visible en la WAN (internet). | Para que el mundo encuentre tu servidor o router. | IP asignada por tu ISP |
| Privada | Identificador en la LAN (red local). | Conectar dispositivos dentro de una misma red. | 192.168.0.15 |
| Estática | Dirección fija que no cambia. | Servidores, bases de datos, VPN. | 8.8.8.8 |
| Dinámica | IP temporal que cambia automáticamente. | Dispositivos domésticos. | IP de tu móvil en Wi-Fi |

---

## 3. Conexión y Desarrollo (CRÍTICO)

- **IP en Backend Local**  
  Se usa `localhost` o `127.0.0.1`, que apunta a tu propia máquina.

- **IP en Producción**  
  Se usa una IP pública estática o un dominio que apunte a ella.

- **El dilema del Localhost**  
  No puedes acceder al `localhost` de otro computador.  
  👉 Para conectar dos PCs necesitas usar sus **IPs privadas**.

- **Base de Datos en la Nube**  
  - Usan IPs públicas protegidas por **whitelists**.  
  - Solo ciertas IPs pueden conectarse (ej: tu backend).

---

## 4. Caso Práctico: Debugging de Conexión

**Escenario:** El frontend funciona pero no se conecta al backend.

### 🔧 ¿Qué revisar?

- **Variables de entorno (.env)**  
  Verifica que no estés apuntando a `localhost` si el backend está en la nube.

- **Firewall / Puertos**  
  Asegúrate de que el puerto (ej: `8080`) esté abierto en AWS, Azure, etc.

- **CORS**  
  El navegador puede bloquear la petición por seguridad.

- **Errores 404 / 500**  
  Usa DevTools (`F12`) → pestaña **Network**:
  - `404` → problema de ruta
  - `500` → error interno del servidor

---

## 5. DHCP y DNS: La Infraestructura Invisible

- **DHCP (Dynamic Host Configuration Protocol)**  
  👉 Asigna automáticamente IPs dentro de la red.

- **DNS (Domain Name System)**  
  👉 Traduce dominios a IPs.

### 🌍 Flujo de navegación

1. Escribes una URL en el navegador.
2. Tu PC consulta al DNS.
3. El DNS devuelve la IP.
4. El navegador se conecta a esa IP y pide la web.

---

## 6. Analogía Obligatoria

- **IP** = Dirección de tu casa  
- **DNS** = Agenda de contactos  
- **DHCP** = Recepcionista que te asigna una habitación  

---

## 🧠 Bonus: Nivel Bootcamp Pro

- **NAT (Network Address Translation)**  
  Permite que múltiples dispositivos usen una sola IP pública.

- **Docker Networking**  
  Cada contenedor tiene su propia IP interna.  
  👉 Se expone con puertos:  
  ```bash
  docker run -p 8080:3000
