## 🔎 Metodología  

1. **Captura de tráfico:**  
   Utilicé Burp Suite para interceptar la solicitud enviada al seleccionar una categoría del sitio. Allí identifiqué el parámetro vulnerable.

2. **Enumeración de columnas:**  
   Usé el siguiente *payload* para verificar el número de columnas disponibles:  '+UNION+SELECT+'abc','def'--

   Determiné que existían **2 columnas** disponibles para la consulta.

3. **Descubrimiento de tablas:**  
Luego empleé esta carga útil para listar las tablas existentes:   '+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--

  Con esto, descubrí una tabla llamada `users_******`.

4. **Descubrimiento de columnas dentro de la tabla:**  
Utilicé el siguiente *payload* para listar las columnas dentro de la tabla `users_******`:  '+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_******'--

Así encontré las columnas `username_******` y `password_******`.

5. **Extracción de datos sensibles:**  
Para visualizar el contenido de esas columnas, usé este *payload*:  '+UNION+SELECT+username_*********,+password_******+FROM+users_******--

Esto reveló las credenciales del usuario **administrator**.

6. **Acceso al sistema:**  
Finalmente, utilicé esas credenciales para iniciar sesión como **administrator**, resolviendo exitosamente el laboratorio.

## 🗝️ Datos clave

- **Tabla descubierta:** `users_******`  
- **Columnas sensibles:** `username_******`, `password_******`  
- **Usuario afectado:** administrator  

---

## 💬 Reflexión personal  

Este laboratorio fue más extenso que otros que había realizado, pero también más enriquecedor. Me permitió comprender en mayor profundidad la estructura de las bases de datos, y cómo la inyección SQL puede ser utilizada para explorar tablas, columnas y extraer datos críticos.

Lo más interesante fue ver cómo pequeños ajustes en los *payloads* pueden significar la diferencia entre una consulta fallida y una extracción exitosa de datos.

---

## 🔚 Conclusión  

Las inyecciones SQL son extremadamente peligrosas si no se controlan adecuadamente. Si una aplicación no filtra correctamente las entradas del usuario y muestra directamente los resultados de la base de datos, puede exponer datos sensibles y comprometer todo el sistema. Este laboratorio refuerza la importancia de la validación de entradas y la implementación de consultas preparadas para prevenir este tipo de ataques.



