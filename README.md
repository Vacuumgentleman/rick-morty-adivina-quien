# 🌀 Portal Guess – Rick & Morty

Aplicación web interactiva desarrollada con **Vue.js** que implementa el clásico juego **“Adivina Quién”**, utilizando personajes del universo Rick & Morty y consumiendo datos desde una API pública REST.

El objetivo del juego es adivinar el personaje secreto seleccionado aleatoriamente por la aplicación en el menor número de preguntas y turnos posibles, descartando personajes mediante preguntas lógicas.

---

## 🎯 Objetivo del Proyecto

Desarrollar una aplicación web frontend que:

- Consuma datos desde una API pública  
- Utilice Vue.js y componentes reutilizables  
- Presente una interfaz gráfica clara, moderna y responsive  
- Funcione correctamente en PC, tablet y dispositivos móviles  
- Sea desplegada y accesible desde la web mediante Vercel  

---

## 🧪 API Utilizada

**Rick and Morty API (REST)**  
🔗 https://rickandmortyapi.com/

Se utiliza el endpoint de personajes para obtener información como:

- Nombre  
- Imagen  
- Estado (Alive, Dead, Unknown)  
- Especie  
- Género  
- Origen  
- Ubicación  
- Episodios en los que aparece  

Los personajes se cargan dinámicamente y se selecciona uno de forma aleatoria como personaje secreto.

---

## 🕹️ Descripción del Juego

- Al iniciar una partida, la aplicación selecciona **20 personajes aleatorios**.  
- La aplicación escoge un **personaje secreto**.  
- El jugador puede:
  - Hacer una pregunta por turno.
  - O intentar adivinar directamente el personaje.
- Las preguntas permiten descartar personajes automáticamente.
- Los personajes descartados se marcan visualmente con una **X**.
- Al acertar, se muestra un **popup final** con:
  - Número de preguntas
  - Número de turnos
  - Puntaje final
- El jugador puede volver a jugar sin recargar la página.

---

## ✨ Funcionalidades Principales

- ✅ Consumo de API pública usando \`fetch\`
- ✅ Juego interactivo tipo Adivina Quién
- ✅ Selección aleatoria del personaje secreto
- ✅ Sistema de preguntas por categorías
- ✅ Descarte automático de personajes
- ✅ Contador de turnos y preguntas
- ✅ Sistema de puntaje
- ✅ Modal de victoria con resumen de resultados
- ✅ Navegación entre vistas usando Vue Router
- ✅ Diseño responsive (PC / Tablet / Móvil)
- ✅ Interfaz gráfica con identidad visual Rick & Morty

---

## 🎨 Interfaz y Experiencia de Usuario (UI/UX)

- Grid uniforme de personajes (5x4 en desktop)
- Navbar sticky siempre visible
- Panel de preguntas:
  - Lateral derecho en desktop
  - Fijo en la parte inferior en móvil
- Botón final con animación tipo portal
- Colores, tipografía y estilo inspirados en Rick & Morty
- Diseño claro, usable e intuitivo

---

## 📱 Diseño Responsive

La aplicación se adapta correctamente a distintos tamaños de pantalla:

- 💻 **Desktop:** tablero completo + panel lateral  
- 📱 **Móvil:** tablero ajustado + panel de preguntas fijo abajo  
- 📟 **Tablet:** layout intermedio optimizado  

---

## 🚀 Tecnologías Utilizadas

- Vue.js 3  
- Vue Router  
- HTML5  
- CSS3 (Flexbox & Grid)  
- JavaScript  
- API REST  
- Vite  
- Vercel (deploy)  

---

## 📸 Capturas de Pantalla

<img width="1861" height="940" alt="imagen" src="https://github.com/user-attachments/assets/731ef327-0b77-4c9c-9f2b-37c555d8af6f" />

<img width="1861" height="940" alt="imagen" src="https://github.com/user-attachments/assets/45f53a80-602c-4e94-a5b8-647d36f8bb86" />
<img width="1861" height="940" alt="imagen" src="https://github.com/user-attachments/assets/7644291e-1d83-4a9a-b484-c24d36f4d964" />


<img width="1861" height="940" alt="imagen" src="https://github.com/user-attachments/assets/4149ef0d-6508-4658-8c9c-5f853a407e9e" />


---

## ⚙️ Instrucciones de Ejecución (Local)

### 1️⃣ Clonar el repositorio

\`\`\`bash
git clone https://github.com/Vacuumgentleman/rick-morty-adivina-quien.git
\`\`\`

### 2️⃣ Entrar al proyecto

\`\`\`bash
cd rick-morty-adivina-quien
\`\`\`

### 3️⃣ Instalar dependencias

\`\`\`bash
npm install
\`\`\`

### 4️⃣ Ejecutar en modo desarrollo

\`\`\`bash
npm run dev
\`\`\`

### 5️⃣ Abrir en el navegador

http://localhost:5173

---

## 🌐 Aplicación Desplegada

🔗 **Enlace en Vercel:**  
👉 https://rick-morty-adivina-quien.vercel.app/

---

## 📁 Organización del Proyecto

\`\`\`
src/
│
├── views/        → Vistas principales (Home, Game)
├── components/   → Componentes reutilizables
├── router/       → Configuración de rutas
└── assets/       → Recursos estáticos
\`\`\`

Código modular, legible y bien estructurado.

---

## 👨‍💻 Autor

**Sebastian Gravini**  
Proyecto académico – Semana 2  
Desarrollo de Aplicación Web con Vue y APIs  

EOF
