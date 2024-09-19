# Documentación de la Automatización Reporte Servidores
**Autor**: Miguel Rincon Gutierrez
**Fecha**: 19-09-2024

## Descripción

Este script genera un reporte en Notebook de los servidores que se encuentren en Dynatrace. Utiliza consultas DQL (Dynatrace Query Language) para obtener datos de CPU, memoria y disco de cada servidor, y luego estructura estos datos en secciones que se añaden al JSON. Al finalizar, el reporte se guarda como un documento en Dynatrace y se comparte con al grupo Documentos_Shared.

## Dependencias

El código utiliza los siguientes módulos de Dynatrace:
- `@dynatrace-sdk/client-document`: Para [crear documentos en Dynatrace](https://developer.dynatrace.com/develop/sdks/client-document/#documentsclient).
- `@dynatrace-sdk/client-query`: Para [ejecutar consultas DQL en Dynatrace](https://developer.dynatrace.com/develop/sdks/client-query/).
- `crypto`: Para generar UUIDs aleatorias.

## Funciones

### `reporte_server(f_jsondata, f_hostname, f_hostId, f_startOfLastMonthISO, f_endOfLastMonthISO)`

Genera las secciones del reporte JSON para un servidor específico.

#### Parámetros:
- `f_jsondata`: JSON base donde se añadirán las secciones.
- `f_hostname`: Nombre del host (servidor) para el cual se generará el reporte.
- `f_hostId`: ID del host.
- `f_startOfLastMonthISO`: Fecha de inicio del mes pasado en formato ISO.
- `f_endOfLastMonthISO`: Fecha de fin del mes pasado en formato ISO.

#### Retorno:
Devuelve el JSON actualizado con las secciones correspondientes.

#### Secciones generadas:
1. **Markdown**: Contiene el nombre del servidor.
2. **DQL Max CPU**: Consulta de uso máximo de CPU.
3. **DQL Memory**: Consulta de uso de memoria.
4. **DQL Disk**: Consulta del estado del disco.

#### Pasos en el codigo:
1. **Obtener la lista de servidores**: Ejecuta una consulta DQL para obtener todos los servidores (`fetch dt.entity.host`).
2. **Crear el reporte**: Para cada servidor, llama a `reporte_server` para añadir sus datos al JSON.
3. **Guardar el reporte**: Crea el reporte en un Notebook de Dynatrace.
4. **Compartir el documento**: Comparte el Notebook con el grupo `Documentos_Shared` con permisos de lectura y escritura.

#### Pasos ejecución usuario:
1. **Ejecutar *RUN* para Generar Notebook**
  ![image](https://github.com/user-attachments/assets/fe5727d1-5bdb-4a70-b387-a25979ada4e3)
3. **Ingresar al link Generado**
2. **Ejecutar *Rerun sections***
   
   ![image](https://github.com/user-attachments/assets/273ba794-549b-42bd-8cb8-ecc01de0c8f8)

   ![image](https://github.com/user-attachments/assets/382dd65e-90da-4782-b574-d64a46fb2086)




- El documento se guarda con el nombre `Reporte [Mes] [Año]`.

#### Pasos ejecución usuario:

