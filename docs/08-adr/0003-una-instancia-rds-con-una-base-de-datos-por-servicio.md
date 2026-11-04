---
tipo: adr
estado: borrador
responsable: Joel
---

# ADR 0003: Una instancia RDS con una base de datos por servicio

- **Estado:** propuesto
- **Fecha:** 2026-10-27
- **Autores:** Joel

## Problema

Cada microservicio con estado debe tener su propio almacenamiento (§4.1) y ningún servicio
escribe en los datos de otro ([propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md)).
El equipo usa PostgreSQL con una base de datos por servicio. Pueden ser hasta quince servicios.

Hay que decidir cómo se despliega PostgreSQL en AWS. El equipo dispone de unos 100 € de
créditos por persona, así que el coste importa, pero sin renunciar a las buenas prácticas.

## Alternativas

1. **Una instancia RDS por servicio**: aislamiento completo, porque un fallo o una sobrecarga
   solo afecta a un servicio. Inconveniente: el coste se multiplica por el número de
   servicios, cada instancia cobra por hora aunque no se use, y hay que gestionar muchos
   recursos.
2. **Una instancia RDS con una base de datos y un usuario por servicio**: cada servicio tiene
   su propia base de datos dentro de la instancia, y un usuario que solo tiene permisos sobre
   ella. Ventajas: un solo coste por hora y propiedad de datos garantizada por permisos.
   Inconveniente: la instancia es un punto único de fallo, y un servicio con mucha carga
   afecta a los demás.
3. **Una sola base de datos con un esquema por servicio**: más barato todavía de gestionar,
   pero la separación es más débil y es fácil acabar haciendo consultas entre esquemas.
4. **Aurora Serverless v2**: escala con la carga. Inconveniente: tiene un coste mínimo por hora
   que no compensa con este volumen.

## Decisión

Usar **una instancia RDS PostgreSQL con una base de datos y un usuario por servicio**:

- Cada servicio se conecta solo a su base de datos, con un usuario propio. El usuario no tiene
  permisos sobre las bases de datos de otros servicios.
- Las credenciales de cada servicio se guardan en Secrets Manager, nunca en el repositorio.
- Las tablas de cada servicio se crean con migraciones versionadas (p. ej. Flyway) dentro del
  propio servicio.
- En local se crea la misma instancia con el RDS de LocalStack (Student Plan), desde el mismo
  Terraform.
- Instancia pequeña, en una sola zona de disponibilidad, con copias de seguridad automáticas.

Motivo principal: es la opción más barata que mantiene la propiedad de datos de verdad. La
separación de una base de datos por servicio es real, porque se aplica con permisos, y si un
servicio lo necesita puede pasar a su propia instancia sin cambiar el código: solo cambia la URL
de conexión.

## Consecuencias

- **Positivas:**
  - Un único coste de instancia por hora en AWS.
  - La propiedad de datos se garantiza con permisos, no solo por convención.
  - Separar un servicio crítico (p. ej. Reservas) en su propia instancia es un cambio de
    configuración.
- **Negativas o riesgos:**
  - **Punto único de fallo:** si cae la instancia, caen todos los servicios con estado. Esto se
    explica en el PDF como compromiso consciente de coste. La alternativa en producción sería
    Multi-AZ o separar los servicios críticos.
  - **Vecinos ruidosos:** un servicio con mucha carga puede frenar a los demás. Es candidato a
    cuello de botella (§7.2).
  - **Creación de bases de datos y usuarios:** hay que crear una base de datos y un usuario por
    servicio dentro de la instancia, lo que exige un paso de inicialización.
- **Ficheros del vault afectados:**
  - [propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md)
  - [infraestructura.md](../07-devops/infraestructura.md)
  - [entorno-local.md](../07-devops/entorno-local.md)
  - [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)

> PENDIENTE: decidir cómo se crean las bases de datos y los usuarios de cada servicio (proveedor `postgresql` de Terraform, script de inicialización o tarea al arrancar).

> PENDIENTE: elegir el tamaño de la instancia. El sandbox de AWS Academy admite PostgreSQL sin Multi-AZ hasta tamaño `medium`, así que la decisión es compatible con él. Secrets Manager está bloqueado en el sandbox: allí las credenciales van en Parameter Store (`SecureString`).
