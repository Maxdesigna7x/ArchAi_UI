# Diseno de ArchAi

Este documento define la organizacion visual y de experiencia para ArchAi. Su objetivo es guiar el diseno de la interfaz antes de comenzar la implementacion.

## Principio central

ArchAi debe sentirse como un **editor de escena arquitectonica**, no como una lista de herramientas de IA.

El usuario trabaja siempre sobre una escena visible. Las herramientas cambian segun el workflow activo, pero el centro de la experiencia se mantiene estable: una imagen arquitectonica sobre la que se toman decisiones visuales.

## Layout principal

La interfaz base tendra un canvas central.

Estructura recomendada:

```txt
+--------------------------------------------------------------------------------+
| Top bar: proyecto, escena, estado, acciones principales                         |
+----------------------+----------------------------------+----------------------+
| Herramientas         | Canvas de escena                 | Panel contextual     |
|                      |                                  |                      |
| - Estilizar          | Imagen activa                    | Prompt               |
| - Editar zona        | Mascaras                         | Referencias          |
| - Objeto 2D          | Objetos colocados                | Parametros           |
| - Objeto 3D          | Preview de profundidad           | Generar              |
| - Assets             | Comparacion antes/despues        | Avanzado             |
|                      |                                  |                      |
+----------------------+----------------------------------+----------------------+
| Timeline / versiones / ramas / outputs                                          |
+--------------------------------------------------------------------------------+
```

## Areas de la interfaz

### Top bar

Debe mostrar:

- Nombre del proyecto.
- Nombre de la escena.
- Estado de guardado.
- Acciones globales:
  - Exportar.
  - Comparar.
  - Deshacer/rehacer cuando aplique.
  - Acceso a configuracion.

Debe mantenerse discreta para no competir con la imagen.

### Panel izquierdo

Contiene la navegacion de herramientas.

Herramientas principales:

- Estilizar.
- Editar zona.
- Objeto 2D.
- Objeto 3D.
- Biblioteca.
- Versiones.

Cada herramienta representa un workflow, no una pagina desconectada.

### Canvas central

Es el area mas importante.

Debe permitir:

- Ver la imagen activa.
- Hacer zoom y pan.
- Comparar antes/despues.
- Ver overlays de mascara.
- Ver objetos colocados.
- Seleccionar objetos.
- Mover, escalar y rotar objetos.
- Visualizar oclusion/profundidad en modo avanzado.

El canvas debe evitar decoracion innecesaria. La imagen debe ser el foco.

### Panel derecho

Es contextual segun la herramienta activa.

Puede contener:

- Prompt.
- Templates.
- Imagenes de referencia.
- Controles basicos.
- Parametros avanzados.
- Boton de generacion.
- Estado del proceso.
- Resultado o preview reciente.

El panel derecho debe tener secciones plegables para no saturar.

### Timeline inferior

Muestra versiones y ramas.

Debe permitir:

- Ver versiones generadas.
- Identificar la version activa.
- Volver a versiones anteriores.
- Comparar dos versiones.
- Crear ramas desde una version antigua.
- Marcar favoritos.

## Navegacion conceptual

La jerarquia debe ser:

```txt
Dashboard
  -> Proyecto
    -> Escena
      -> Workflow activo
        -> Version generada
```

El usuario no debe perder de vista en que proyecto y escena esta trabajando.

## Pantallas principales

### Dashboard de proyectos

Objetivo:

Permitir entrar rapidamente a un proyecto existente o crear uno nuevo.

Elementos:

- Lista/grid de proyectos.
- Nombre del proyecto.
- Miniatura de escena reciente.
- Fecha de ultima modificacion.
- Boton para crear proyecto.

### Vista de proyecto

Objetivo:

Mostrar las escenas y assets del proyecto.

Elementos:

- Escenas del proyecto.
- Biblioteca de assets.
- Outputs finales.
- Acceso a templates guardados.
- Accion para crear nueva escena.

### Editor de escena

Objetivo:

Ser el espacio principal de trabajo.

Elementos:

- Canvas central.
- Herramientas.
- Panel contextual.
- Timeline.
- Biblioteca accesible.

## Workflows de interfaz

### Workflow: Estilizar

Panel derecho:

- Buscador de templates.
- Galeria de templates con miniaturas.
- Prompt editable.
- Intensidad de cambio.
- Imagen de referencia opcional.
- Boton Generar.

Canvas:

- Imagen activa.
- Comparacion antes/despues despues de generar.

Timeline:

- Nueva version con tipo `style_transfer`.

Estados:

- Sin template seleccionado.
- Template seleccionado.
- Generando.
- Resultado listo.
- Error de generacion.

### Workflow: Editar zona

Panel derecho:

- Boton para detectar zonas.
- Toggle para mostrar segmentacion.
- Prompt de edicion.
- Imagen de referencia.
- Ajustes basicos de mascara:
  - Expandir.
  - Suavizar borde.
  - Invertir.
  - Limpiar.
- Seccion avanzada:
  - Feather.
  - Preservar geometria.
  - Preservar iluminacion.

Canvas:

- Imagen activa.
- Overlay de segmentacion.
- Mascara seleccionada.
- Click para seleccionar zona.
- Herramientas de refinamiento cuando aplique.

Timeline:

- Nueva version con tipo `masked_edit`.

Estados:

- Segmentacion pendiente.
- Segmentando.
- Zonas detectadas.
- Mascara seleccionada.
- Generando.
- Resultado listo.

### Workflow: Objeto 2D

Panel derecho:

- Prompt para generar objeto.
- Imagen de referencia opcional.
- Variantes generadas.
- Accion para guardar en biblioteca.
- Controles de objeto seleccionado:
  - Posicion.
  - Escala.
  - Rotacion.
  - Opacidad de preview.
- Boton Integrar en escena.

Canvas:

- Objeto superpuesto sobre la imagen.
- Controles visuales de transformacion.
- Preview antes de integrar.

Timeline:

- Version al integrar el objeto.

Estados:

- Sin objeto.
- Generando objeto.
- Objeto listo.
- Objeto colocado.
- Integrando.
- Resultado listo.

### Workflow: Objeto 3D/2.5D

Panel derecho:

- Seleccion de objeto.
- Estado de conversion a 3D.
- Estado del depth map.
- Controles:
  - X/Y.
  - Profundidad.
  - Escala.
  - Rotacion.
  - Oclusion.
  - Contacto/sombra.
- Boton Generar integracion.

Canvas:

- Preview 2.5D.
- Objeto posicionado.
- Visualizacion opcional de profundidad.
- Oclusion aproximada.

Timeline:

- Version al integrar el objeto 3D.

Estados:

- Falta objeto.
- Convirtiendo a 3D.
- Generando depth.
- Objeto posicionable.
- Integrando.
- Resultado listo.

## Biblioteca visual de templates

Los templates deben verse como opciones visuales, no como una lista tecnica.

Cada tarjeta debe mostrar:

- Miniatura.
- Nombre corto.
- Categoria.
- Indicador de si usa referencia o no.

Al seleccionar un template:

- El prompt se copia al panel de edicion.
- El usuario puede modificarlo.
- Los parametros recomendados se cargan automaticamente.

Categorias iniciales:

- Fachada.
- Interior.
- Material.
- Iluminacion.
- Paisajismo.
- Comercial.
- Conceptual.

## Biblioteca de proyecto

Debe funcionar como un drawer o panel accesible.

Filtros:

- Imagenes.
- Referencias.
- Materiales.
- Objetos 2D.
- Objetos 3D.
- Mascaras.
- Depth maps.
- Outputs.

Acciones:

- Insertar en escena.
- Usar como referencia.
- Renombrar.
- Eliminar.
- Marcar favorito.

## Timeline ramificado

El timeline debe mostrar la historia de la escena.

Cada item debe indicar:

- Miniatura.
- Tipo de operacion.
- Hora/fecha.
- Prompt resumido.
- Version padre si es una rama.
- Favorito.

Acciones:

- Activar version.
- Comparar.
- Duplicar como rama.
- Marcar como final.

## Modos basico y avanzado

La interfaz debe abrir siempre en modo basico.

Modo basico muestra:

- Prompt.
- Template.
- Referencia.
- Seleccion visual.
- Generar.
- Comparar.

Modo avanzado muestra:

- Proveedor/modelo.
- Seed.
- Intensidad.
- Resolucion.
- Feather.
- Expansion de mascara.
- Preservar geometria.
- Oclusion.
- Depth map.
- Parametros de integracion.

Los controles avanzados deben estar plegados por defecto.

## Reglas de experiencia

- La imagen debe ser siempre el foco principal.
- Nunca ocultar el contexto de proyecto y escena.
- Cada generacion debe guardar una version.
- Nunca sobrescribir la imagen original.
- Mostrar preview de mascara antes de editar.
- Mostrar preview de objeto antes de integrar.
- Permitir comparar antes/despues facilmente.
- Evitar lenguaje demasiado tecnico en el modo basico.
- Los estados de carga deben explicar que proceso esta ocurriendo.
- Los errores deben decir que fallo y que puede intentar el usuario.

## Estados vacios

### Sin proyecto

Mostrar accion principal:

- Crear proyecto.

### Proyecto sin escenas

Mostrar accion principal:

- Crear escena.
- Subir imagen base.

### Escena sin versiones

Mostrar:

- Imagen original.
- Acciones sugeridas:
  - Estilizar.
  - Editar zona.

### Biblioteca vacia

Mostrar:

- Subir referencia.
- Generar objeto.
- Guardar resultado como asset.

## Estados de carga

Procesos esperados:

- Subiendo imagen.
- Analizando imagen.
- Segmentando zonas.
- Generando estilo.
- Editando mascara.
- Generando objeto.
- Convirtiendo a 3D.
- Generando depth map.
- Integrando objeto.

Cada estado debe mostrar progreso textual o visual, aunque el porcentaje no sea exacto.

## Errores esperados

La interfaz debe contemplar:

- Fallo al subir imagen.
- Imagen no compatible.
- Segmentacion no detecta zonas utiles.
- Generacion fallida.
- Proveedor IA no disponible.
- Imagen de referencia invalida.
- Error al crear depth map.
- Error al convertir a 3D.
- Error al guardar version.

Cada error debe permitir:

- Reintentar.
- Cambiar parametros.
- Cancelar operacion.
- Volver al estado anterior.

## Criterios visuales

Estilo recomendado:

- Interfaz sobria y profesional.
- Prioridad a imagenes grandes.
- Paneles densos pero ordenados.
- Botones claros para acciones principales.
- Iconos para herramientas.
- Miniaturas para templates y versiones.
- Colores neutros con acentos discretos.

Evitar:

- Landing page como primera pantalla del producto.
- Decoracion excesiva.
- Gradientes llamativos.
- Cards innecesarias dentro de cards.
- Textos largos explicando funciones dentro de la UI.
- Controles tecnicos visibles todo el tiempo.

## Accesibilidad y usabilidad

Consideraciones:

- Tooltips para iconos.
- Contraste suficiente.
- Estados seleccionados claros.
- Nombres cortos en herramientas.
- Acciones destructivas con confirmacion.
- Navegacion por teclado donde sea viable.
- Textos que no se desborden en paneles.
- Botones con estados disabled/loading.

## Resultado esperado de la experiencia

Un usuario deberia poder:

1. Crear un proyecto.
2. Subir una imagen de una escena arquitectonica.
3. Aplicar un estilo con un template.
4. Seleccionar una zona con segmentacion.
5. Editar esa zona con prompt y referencia.
6. Ver el resultado como una nueva version.
7. Comparar versiones.
8. Generar un objeto.
9. Colocarlo visualmente.
10. Integrarlo en la imagen final.

La parte 3D/2.5D debe quedar como una expansion natural del mismo flujo, no como una aplicacion diferente dentro de ArchAi.

