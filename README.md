# Guia de integracion cliente

Este documento describe los pasos que debe seguir un integrador externo para enviar un consumo de folios a la API y procesar la respuesta.

## Paso 1. Crear el archivo TXT

El integrador debe generar un archivo TXT con contenido PHP valido.

Este archivo debe contener:

- Datos de caratula del consumo en `$Caratula`.
- Resumen de folios por tipo de documento en `$Resumen`.
- Datos del certificado digital en `$FACTRONICA`.

El archivo debe enviarse en el campo `archivotxt`.  
  
En la siguiente Url se encuentra el formato de ejemplo del archivo Txt  
https://github.com/FacTronica/ConsumoFoliosBoletasElectronicas/blob/master/ConsumoFoliosEjemplo.txt

## Paso 2. Realizar la peticion HTTP

La peticion debe tener los siguiente atributos:

```http
POST https://consumofolios.factronica.cl/
Content-Type: multipart/form-data
```

Debe enviar estos campos:

| Campo | Tipo | Requerido | Descripcion |
| --- | --- | --- | --- |
| `apikey` | texto | Si | Clave entregada por el proveedor de la API. |
| `archivotxt` | archivo | Si | Archivo TXT/PHP con el consumo de folios. |

### Ejemplo de envio con curl

```bash
curl --form "archivotxt=@consumo.php" --form "apikey=abc123" https://consumofolios.factronica.cl
```

Si el archivo tiene extension `.txt`, el comando seria:

```bash
curl --form "archivotxt=@consumo.txt" --form "apikey=abc123" https://consumofolios.factronica.cl
```

## Paso 3. Recibir la respuesta

La API responde siempre en formato JSON.

Ejemplo de respuesta exitosa:

```json
{
  "acceso": 1,
  "estado": 1,
  "mensaje": "Consumo de Folios recibido por el SII Chile",
  "semilla": "123456789",
  "token": "TOKEN_SII",
  "trackid": "1234567890"
}
```

## 5. Analizar la respuesta JSON

El integrador debe interpretar estos campos:

| Campo | Descripcion |
| --- | --- |
| `acceso` | Indica si la API key fue aceptada. `1` aceptada, `0` rechazada. |
| `estado` | Indica si el consumo fue recibido por el SII. `1` recibido, `0` no recibido o pendiente. |
| `mensaje` | Texto descriptivo del resultado. |
| `semilla` | Semilla obtenida desde el SII. |
| `token` | Token obtenido desde el SII. |
| `trackid` | Identificador entregado por el SII. Si es `0`, no hubo recepcion confirmada. |

## 6. Validaciones recomendadas

El cliente debe considerar el envio exitoso solo si:

```text
acceso = 1
estado = 1
trackid > 0
```

Si `acceso` es `0`, la API key fue rechazada.

Si `estado` es `0`, el consumo no fue confirmado como recibido por el SII y se debe revisar el campo `mensaje`.

## 7. Respuestas de error frecuentes

### Falta API key

```json
{
  "acceso": 0,
  "estado": 0,
  "mensaje": "ERROR: No viene apikey, acceso rechazado"
}
```

### API key invalida

```json
{
  "acceso": 0,
  "estado": 0,
  "mensaje": "ERROR: apikey no valida, acceso rechazado"
}
```

### Falta archivo

```json
{
  "acceso": 1,
  "estado": 0,
  "mensaje": "ERROR: No viene archivotxt"
}
```

### SII no disponible o sin token

```json
{
  "acceso": 1,
  "estado": 0,
  "mensaje": "ERROR: SII Ocupado volver a Intentar"
}
```

