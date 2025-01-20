## Crea tu bot de Amazon Lex

**Caso de Uso**

En este caso de uso, crearemos un bot de Lex que saludará a nuestros clientes cuando llamen a nuestro entorno de Service Cloud Voice. El bot de Lex saludará a la persona que llama y determinará la intención de la llamada. Una vez determinada la intención de la llamada, el bot dirigirá la llamada al destino apropiado para el servicio.

En nuestro caso de uso, vamos a implementar un bot de Amazon Lex con tres intenciones: "Nuevas ventas", "Soporte técnico" y "Soporte de pedidos". En un escenario de caso de uso real, el bot se puede mejorar agregando intenciones adicionales como "Soporte de estado de pedido", "Detalles de envío" o incluso "Pedido de autoservicio" para nuevos componentes. Cada una de estas funciones estaría representada como intenciones separadas.

**Construye tu bot de Amazon Lex**

1. **Accede a Amazon Lex:** En la barra de búsqueda de tu consola de AWS, escribe "Lex" y selecciona "Amazon Lex" en los resultados.
2. **Verifica la región:** Asegúrate de que la región seleccionada sea la misma en la que está implementada tu instancia de Amazon Connect. Puedes hacerlo seleccionando la región en la esquina superior derecha de la consola de AWS y eligiendo la región adecuada.
3. **Crea un bot:** Si ves la pantalla de bienvenida, selecciona "Crear bot".

    **Nota:** Asegúrate de estar en la Consola de Lex V2 y de estar en la región de AWS correcta.

4. **Configura el bot:**
    * Selecciona "Crear bot".
    * Elige "Crear bot en blanco" como método de creación.
    * Para Nombre del bot, ingresa "ventasforce_combinado".
    * Para Permisos de IAM, selecciona "Crear un rol con permisos básicos de Amazon Lex".
    * Para la opción COPPA, selecciona "No".
    * Para el tiempo de espera de la sesión inactiva, ingresa "5" y deja la selección en "minutos".
    * Selecciona "Siguiente".
5. **Agrega el idioma:** En la pantalla "Agregar idioma al bot", ingresa la siguiente información y elige "Listo".
    * Para Idioma, selecciona "Español (US)" (o el idioma que sea apropiado para tu caso de uso).
    * Para Interacción de voz, selecciona una voz en español apropiada.
6. **Renombra la intención predeterminada:** Cámbiala a "soporte_orden".
7. **Agrega enunciados de ejemplo:** Ingresa los siguientes mensajes y selecciona "Agregar enunciado" después de cada uno:

    * Tengo un problema con mi cuenta
    * Problema de cuenta
    * Número de cuenta {account_id}
    * Tengo un problema con la cuenta número {account_id}
    * Soporte de cuenta
    * Necesito ayuda con mi cuenta
    * Necesito ayuda con la cuenta número {account_id}
    * ¿Puedes ayudarme con la cuenta número {account_id}?
8. **Agrega una ranura:** 
    * Ve a la sección "Ranuras" y selecciona "Agregar ranura" (datos que el usuario debe proporcionar para cumplir con la intención).
    * Nombre de la ranura: "account_id"
    * Tipo de ranura: "Amazon.Number"
    * Solicitud: "¿Podrías proporcionar tu número de cuenta, por favor?"
    * Asegúrate de que la casilla de verificación "Requerido para esta intención" esté seleccionada.
    * Selecciona "Agregar ranura".
9. **Configura las solicitudes de confirmación:**
    * Expande "Solicitudes" para confirmar la intención.
    * Solicitud de confirmación: "De acuerdo, tengo tu número de cuenta como {account_id}. ¿Es correcto?"
    * Respuesta de rechazo: "OK, gracias."
10. **Configura las solicitudes de cumplimiento:**
    * Expande "Solicitudes" para confirmar la intención.
    * Cumplimiento exitoso: "Gracias por la información de tu cuenta."
    * Error de cumplimiento: "Lo siento, algo salió mal."
11. **Desactiva el cumplimiento:** Asegúrate de que el interruptor "Activo" esté desactivado en la sección "Cumplimiento".
12. **Guarda la intención:** Selecciona "Guardar intención" en la parte inferior de la página.
13. **Crea la intención "soporte_tecnico":**
    * Selecciona "Volver a la lista de intenciones" en el menú de navegación izquierdo.
    * Selecciona "Agregar intención" y luego elige "Agregar intención vacía".
    * Nombra la intención como "soporte_tecnico" y selecciona "Agregar".
14. **Agrega enunciados de ejemplo para "soporte_tecnico":**

    * Mi {equipment_type} no funciona
    * Soporte para {equipment_type}
    * Tengo un problema con mi {equipment_type}
    * Mi {equipment_type} siempre está roto
    * Soporte técnico
    * Necesito ayuda con mi {equipment_type}
    * Mi {equipment_type} está roto
    * Mis cosas están rotas
    * Necesito ayuda con mi compra
    * No puedo hacer que este equipo funcione
15. **Agrega una ranura para "soporte_tecnico":**
    * Ve a la sección "Ranuras" y selecciona "Agregar ranura".
    * Nombra la ranura "equipment_type" y deja el tipo de ranura en blanco.
    * En la sección de solicitud, agrega "¿Con qué tipo de equipo tienes problemas?" y asegúrate de que la casilla de verificación "Requerido para esta intención" esté marcada.
    * Selecciona "Agregar".
16. **Crea un tipo de ranura personalizado:**
    * Expande la sección "Ranuras" y selecciona "Opciones avanzadas" en la parte inferior izquierda.
    * Selecciona "Crear tipo de ranura".
    * En el campo "Nombre del tipo de ranura", ingresa "equipment_type" y luego selecciona "Agregar".
    * Agrega lo siguiente a la sección "Valores del tipo de ranura":
        * molino de viento
        * generador
        * panel solar
        * batería
    * Selecciona "Guardar tipo de ranura".
17. **Asigna el tipo de ranura personalizado:**
    * Selecciona "< Tipos de ranura" en la parte superior izquierda de la pantalla.
    * Elige "Intenciones" en el menú de navegación lateral.
    * Selecciona la intención "soporte_tecnico", ve a la sección "Ranuras" y expándela.
    * Cambia el "Tipo de ranura" al tipo de ranura personalizado "equipment_type".
    * Selecciona "Guardar intención" en la parte inferior de la página.
18. **Crea la intención "nueva_venta":**
    * Selecciona "Volver a la lista de intenciones".
    * Selecciona "Agregar intención" y luego elige "Agregar intención vacía".
    * Nombra la intención como "nueva_venta" y selecciona "Agregar".
19. **Agrega enunciados de ejemplo para "nueva_venta":**

    * Estoy interesado en un {equipment_type}
    * Quiero comprar un {equipment_type}
    * Necesito ayuda con un pedido de {equipment_type}
    * Necesito información sobre un producto
    * Ventas
    * Quiero un nuevo {equipment_type}
    * Necesito más {equipment_type}
    * Tengo dinero para gastar
    * Necesito ayuda para comprar cosas
20. **Agrega una ranura para "nueva_venta":**
    * Ve a la sección "Ranuras" y selecciona "Agregar ranura".
    * Nombra el tipo de ranura "equipment_type" y elige "equipment_type" como "Tipo de ranura".
    * Establece las "Solicitudes" en "¿En qué tipo de producto estás interesado?" y asegúrate de que la casilla de verificación "Requerido para esta intención" esté marcada.
    * Selecciona "Agregar".
21. **Desactiva el cumplimiento para "nueva_venta":** Asegúrate de que el interruptor "Activo" esté desactivado en la sección "Cumplimiento".
22. **Guarda la intención:** Selecciona "Guardar intención" en la parte inferior de la página.
23. **Construye el bot:** Selecciona "Construir" para construir tu bot.

    **Nota:** Si recibes un error que indica que tu bot no se puede construir debido a un problema de Lambda, debes asegurarte de que la opción "Cumplimiento" para cada intención no esté configurada en "Activo". Esta configuración requiere una función de AWS Lambda para el cumplimiento final y este módulo no usa esta opción.

**Prueba el bot**

1. Una vez que el bot se haya construido correctamente, pruébalo seleccionando "Probar".
2. Prueba el bot escribiendo un enunciado en la ventana "Probar". Comienza ingresando "Mi equipo está roto". Cuando se te solicite el tipo de equipo, ingresa "molino de viento". El bot debería devolver un cumplimiento de la intención de soporte técnico.
3. Ahora prueba una segunda interacción ingresando "Necesito ayuda con un pedido". El bot te pedirá el tipo de producto. Ingresa "panel solar". El bot debería devolver un cumplimiento de la intención de ventas.
