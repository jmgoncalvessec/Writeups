# 🧾 Resolución técnica – User ID Controlled by Request Parameter

## 🔍 Pasos realizados

1. **Revisión del código fuente:**
   - Comencé inspeccionando el código fuente de la página principal para verificar si había información sensible expuesta o comentarios dejados por el desarrollador. No encontré nada relevante.

2. **Acceso a la cuenta:**
   - Seguí la indicación del laboratorio, que mencionaba que la vulnerabilidad se encontraba en la página de la cuenta del usuario.
   - Usé las credenciales proporcionadas:
     ```
     Usuario: weiner  
     Contraseña: Peter
     ```

3. **Inspección del perfil del usuario:**
   - Una vez dentro, observé que la página mostraba una API KEY asociada al usuario autenticado.
   - En la URL del navegador noté que el parámetro `id` estaba vinculado al nombre de usuario. Ejemplo:
     ```
     https://example.com/account?id=weiner
     ```

4. **Prueba de escalado horizontal:**
   - Cambié el valor del parámetro `id` en la URL por el nombre de otro usuario conocido:
     ```
     https://example.com/account?id=carlos
     ```
   - Esto me permitió acceder al perfil de otro usuario (Carlos) sin restricciones, exponiendo su API KEY.
---

## 🧠 Reflexión final

Este laboratorio demuestra que muchas veces no es necesario utilizar herramientas sofisticadas para encontrar fallos graves. Observar los parámetros que se manejan en las URLs puede revelar vulnerabilidades de control de acceso que podrían ser explotadas fácilmente si no se implementan medidas de validación adecuadas en el servidor.

