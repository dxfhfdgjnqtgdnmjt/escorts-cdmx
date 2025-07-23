# Escorts en Ciudad de México: README de un proyecto web de acompañantes CDMX

Este README describe la arquitectura, instalación y uso de un “software–sitio” (PHP/HTML/JS/CSS) que documenta y facilita el servicio de alquiler de compañía platónica bajo la marca **Escorts en Ciudad de México**. Aquí encontrarás módulos, configuraciones, políticas de seguridad y FAQ para desplegar la plataforma y orientar a usuarios finales.

¿Listo para implementar o simplemente quieres conocer perfiles verificados y reservar con seguridad? Visita [escorts-cdmx.com](https://escorts-cdmx.com) y descubre cómo conectar con Escorts en Ciudad de México desde hoy mismo.
¡Despliega el proyecto, personalízalo y facilita experiencias sociales seguras y transparentes!

> **Nota:** Todos los ejemplos de precios y reseñas en este documento son ilustrativos.

---

## 1. Descripción general (Overview)

**Objetivo:**  
Proveer una interfaz clara para que clientes y acompañantes coordinen actividades sociales, turísticas o profesionales sin componente romántico o sexual. El sistema prioriza transparencia en tarifas, reseñas verificables y límites de seguridad.

**Público meta:**  
- Residentes  
- Turistas  
- Nómadas digitales  
- Quienes buscan compañía puntual para eventos o recorridos

### Características clave

- Gestión de perfiles con intereses y zonas de operación  
- Módulo de tarifas y políticas de cancelación  
- Sistema de reseñas (internas y externas)  
- Flujos de contacto vía WhatsApp, formularios y redes  
- Guías de seguridad y legalidad integradas  

---

## 2. Requisitos del sistema

- **Servidor:** Apache o Nginx con PHP 8.x  
- **Base de datos:** MySQL/MariaDB 10+ (o adaptador PDO para PostgreSQL)  
- **Front‑end:** HTML5 / CSS3 / JS vanilla (compatible con frameworks ligeros)  
- **Extensiones PHP:** PDO, OpenSSL, mbstring, json  
- **Opcional:** Composer para dependencias y npm para tareas de build (minificación, bundling)  

---

## 3. Instalación

```bash
git clone https://escorts-cdmx.com/escorts-cdmx.git
cd escorts-cdmx
composer install                # Dependencias PHP
npm install && npm run build    # Opcional: pipeline front-end
cp .env.example .env            # Configura variables
php artisan key:generate        # (si usas un microframework tipo Laravel/Lumen)
```

Configura el host virtual y apunta el DocumentRoot a /public.

## 4. Configuración (.env)

```dotenv
APP_NAME="Escorts CDMX"
APP_ENV=production
APP_URL=https://tu-dominio.com

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=escorts_cdmx
DB_USERNAME=usuario
DB_PASSWORD=contraseña

MAIL_MAILER=smtp
MAIL_HOST=smtp.tudominio.com
MAIL_PORT=587
MAIL_USERNAME=notificaciones@tudominio.com
MAIL_PASSWORD=mailpass
MAIL_ENCRYPTION=tls
```

### Parámetros relevantes

Variable	Descripción	Ejemplo
ZONE_DEFAULT	Zona por defecto para búsquedas	Roma Norte
PRICE_CURRENCY	Moneda de tarifas	MXN
REVIEW_PROVIDER	Fuente externa de reseñas	GoogleMaps
CONTACT_CHANNELS	Canales habilitados	whatsapp,form,instagram

## 5. Estructura de carpetas

```bash
app
├── Controllers
├── Models
│   ├── Zone.php       # CRUD de colonias y áreas
│   ├── Service.php    # Tipos de acompañamiento
│   ├── Agency.php     # Agencias y colectivos
│   ├── Review.php     # Reseñas internas/externas
│   └── Price.php      # Tarifas y políticas
├── Views
public
resources
├── css
├── js
└── templates
routes
tests
```

## 6. Módulos funcionales

### 6.1 Zonas de operación

El módulo Zone permite listar y filtrar perfiles por colonias/áreas de mayor demanda:

- Roma Norte / Roma Sur
- La Condesa / Hipódromo
- Polanco / Lomas
- Coyoacán
- Centro Histórico
- Narvarte / Del Valle / Nápoles
- Santa María la Ribera / San Rafael
- Zona Sur (San Ángel, Tlalpan)

Uso (pseudo-API):

```http
GET /api/zones
GET /api/zones?name=Condesa
```

### 6.2 Servicios ofrecidos

El modelo Service define categorías de actividades:

- Acompañamiento social (eventos, comidas, conciertos)
- Turismo local (museos, mercados, street food tours)
- Intercambio de idiomas
- Hobbies compartidos (ciclismo, cine, juegos de mesa)
- Eventos profesionales (networking, ferias, congresos)
- Escucha activa (no sustituto de terapia)

### 6.3 Plataformas y canales de promoción

En el front‑end se listan enlaces a plataformas donde se anuncian perfiles:
- Sitio propio: Conoce más detalles en Escorts en Ciudad de México
- Marketplaces de experiencias
- Redes sociales: Instagram, TikTok, Facebook (#RentAFriendCDMX)
- Comunidades (Reddit, foros específicos)
- Grupos de WhatsApp/Telegram gestionados por agencias/colectivos

### 6.4 Agencias y colectivos

El modelo Agency agrupa perfiles y estandariza procesos:
- Colectivos de acompañantes que comparten protocolos
- Agencias boutique con verificación de identidad
- Startups con contratos y pagos integrados
- Ventajas: soporte, filtros de seguridad.
- Desventajas: comisiones que elevan la tarifa final.

### 6.5 Reseñas y valoración

El modelo Review integra calificaciones desde:
- Google Maps, Trustpilot (si aplica)
- Redes sociales (historias destacadas)
- Foros y subreddits
- Sistema interno de estrellas/comentarios

Ejemplos ilustrativos:
- “Excelente guía por el Centro Histórico, puntual y con datos curiosos.”
- “Profesional y bilingüe para un evento corporativo, todo claro desde el inicio.”
- “Cancelación por lluvia: recibí reembolso parcial en menos de 24 horas.”

## 7. Precios y políticas

El módulo Price maneja rangos y condiciones. Rango ilustrativo (MXN):

Modalidad	Duración	Rango (MXN)*	Incluye	Política básica
Charla casual en café	1–2 h	$250–$550	Tiempo, conversación, traslado cercano	Prepago parcial, 24 h de aviso
Tour temático a pie	2–3 h	$650–$1 300	Ruta planificada, entradas básicas	Reembolso parcial si llueve
Evento social formal	3–5 h	$1 100–$2 700	Vestimenta acorde, coordinación previa	Depósito 50 %, NDA opcional
Jornada completa (extendida)	6–8 h	$2 600–$5 200	Acompañamiento continuo, pausas acordadas	Contrato simple, penalización tardía

* Cifras ilustrativas, confirma siempre con la persona o agencia.

Para comparar ofertas entre diferentes Escorts en Ciudad de México, activa el comparador dentro del panel /pricing.

### Formas de pago

- SPEI / transferencia
- PayPal, Mercado Pago
- Efectivo (solo en espacios públicos y con comprobantes)

## 8. Flujo de contratación (User Journey)

1. Explorar perfiles (filtros por zona/actividad)
2. Contacto inicial: via WhatsApp, formulario o DM con fecha, duración y actividad
3. Negociación: tarifa, punto de encuentro, política de cancelación
4. Verificación mutua: videollamada corta, redes verificadas
5. Pago seguro
6. Encuentro y evaluación: deja reseña para retroalimentar el ecosistema

Endpoint de ejemplo:

```http
POST /api/contact
Content-Type: application/json

{
  "profile_id": 123,
  "date": "2025-08-15",
  "duration_hours": 3,
  "activity": "Tour de tacos en Coyoacán"
}
```

Respuesta:

```json
{
  "status": "pending",
  "message": "Solicitud enviada al acompañante. Recibirás confirmación."
}
```

## 9. Legalidad y riesgos

Se aplica el marco general de prestación de servicios, protección de datos y normas fiscales.

Buenas prácticas legales y de seguridad:

- Dejar por escrito límites y acuerdos (mensajes como evidencia)
- No compartir datos sensibles innecesarios
- Verificar perfiles para evitar fraude o suplantación
- Reunirse inicialmente en lugares públicos e informar a un tercero
- Declarar ingresos si la actividad es recurrente (obligación fiscal)

## 10. Seguridad (Security Guidelines)

Recomendaciones de usuario:

- Compartir ubicación en tiempo real con alguien de confianza
- Palabra clave de emergencia acordada previamente
- Uso moderado de alcohol/sustancias durante la actividad
- Prever rutas de regreso y límite de efectivo en mano

Implementación técnica:

- Cifrado TLS en todas las comunicaciones
- Hashing de contraseñas (bcrypt/argon2)
- Sanitización de inputs contra XSS/SQL Injection
- Logs de actividad para auditoría (cumplimiento de privacidad)

## 11. FAQ

1. ¿Es legal contratar este servicio? Sí, siempre que cumpla con leyes civiles y fiscales. Evita actividades ilícitas o fuera del acuerdo.
2. ¿Qué pasa si cancelo el mismo día? Depende de la política acordada. Muchos perfiles cobran entre 20 % y 50 % por cancelaciones tardías (ejemplo ilustrativo).
3. ¿Puedo pedir un NDA? Sí. Útil en eventos corporativos o información sensible. Redáctalo en lenguaje claro.
4. ¿Cómo sé si un perfil es confiable? Revisa reseñas verificables, historial en redes y solicita videollamada previa. Plataformas con verificación de identidad aportan seguridad.
5. ¿Qué hago si me siento incómodo durante la actividad? Comunícalo de inmediato, termina el encuentro y reporta a la plataforma o agencia. Conserva evidencias de chat.

## 12. Contribuir (Contributing)

1. Haz un fork del repositorio.
2. Crea una rama feature:

```bash
git checkout -b feature/nueva-seccion
```

3. Realiza cambios y haz commit:

```bash
git commit -m "Agrega módulo de reservas"
```

4. Haz push:

```bash
git push origin feature/nueva-seccion
```

5. Abre un Pull Request con descripción detallada.

Se agradecen aportes en accesibilidad, seguridad y UX.

## 13. Licencia
Este proyecto de documentación se distribuye bajo licencia GNU General Public License (GNU GPL). Los contenidos y ejemplos de precios/reseñas son orientativos y no constituyen asesoría legal ni contractual.
