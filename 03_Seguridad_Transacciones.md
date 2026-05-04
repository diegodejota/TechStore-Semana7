# 03 · Seguridad en Transacciones
 
## Riesgos identificados
 
### Riesgo 1: Inyección SQL
Un atacante introduce código SQL en un formulario
(ejemplo: ' OR '1'='1) para saltarse el login o robar datos.
 
### Riesgo 2: Fraude de pago
Tarjetas robadas, manipulación de montos, transacciones falsas.
 
### Riesgo 3: Robo de datos
Si la BD es comprometida, contraseñas y datos personales
quedan expuestos.
 
### Riesgo 4: Intercepción en tránsito
Datos viajando sin cifrar pueden ser leídos por terceros
(ataques man-in-the-middle).
 
## Medidas de seguridad
 
### 1. Consultas parametrizadas (Prepared Statements)
**Mal (vulnerable):**
```sql
"SELECT * FROM users WHERE email = '" + input + "'"
```
 
**Bien (seguro):**
```sql
SELECT * FROM users WHERE email = ?
```
El motor trata el input como dato, no como código.
 
### 2. Validación en el backend
- Nunca confiar en el frontend
- Validar tipo, longitud y formato de cada campo
- Sanitizar caracteres especiales
 
### 3. Cifrado
- **HTTPS / TLS 1.3** para datos en tránsito
- **bcrypt** para almacenar contraseñas (nunca en texto plano)
- Cifrado en reposo de la base de datos
 
### 4. Autenticación y control de acceso
- Tokens JWT para sesiones
- Roles diferenciados (admin / usuario)
- Tokens anti-CSRF en formularios
 
## Resumen
| Riesgo | Mitigación |
|---|---|
| Inyección SQL | Consultas parametrizadas |
| Fraude de pago | Validación en backend + tokens |
| Robo de datos | Hash bcrypt + cifrado |
| Tránsito inseguro | HTTPS / TLS 1.3 |
