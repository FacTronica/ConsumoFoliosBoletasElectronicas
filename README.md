# Consumo de Folios Boletas Electrónicas
SDK Factronica
<br>A continuación se detalla el Procedimiento para realizar la integración con Software Propio.
<h3>Procesos a Realizar:</h3>
1.-Generar Archivo Plano TXT Consumo de Folios
<br>2.-Enviar Archivo Plano TXT al Servidor de Facturación
<br>3.-Recuperar Archivo XML con TrackID
<br>4.-Recuperar Archivo XML Consumo de Folios
<hr>
<h3>Proceso 1: Generar Archivo TXT con Consumo de Folios</h3>
Este proceso Consiste en generar un archivo de texto plano con el formato requerido por el sdk de factronica.
<br>-Servidor Facturación
<br>-Datos de Caratula
<br>-Datos de Emisor
<br>-Datos de Resumen
<br>-Datos de Certificado
<br>Ver Formato del archivo TXT para Consumo de Folios.
<br>Ejemplo: https://github.com/FacTronica/ConsumoFoliosBoletasElectronicas/blob/master/ConsumoFoliosEjemplo.txt
<br>
<hr>
<h3>Proceso 2: Enviar Archivo TXT Consumo de Folios</h3>
<b>Enviar archivo desde Consola Linux:</b>
<br>curl --form "archivotxt=@consumofolios.txt" http://www.factronica.cl/sdk/factronica_consumofolios/recibe_txt_consumofolios.php
<br>
<br><b>Enviar archivo txt desde Consola Windows:</b>
<br>c:\curl\curl.exe --form "archivotxt=@c:\curl\consumofolios.txt" http://www.factronica.cl/sdk/factronica_consumofolios/recibe_txt_consumofolios.php
<br>
<hr>
<h3>Proceso 3: Obtener Archivo XML Consumo de Folios:</h3>
Este proceso es necesario para poder obtener una copia del xml del archivo Consumo de folios.
<br>
<br><b>Obtener archivo Xml desde Linux:</b>
<br>curl -o CONSUMOFOLIOS_FECHA31122018_RUT111111111_ENVIO.xml http://www.factronica.cl/sdk/factronica_consumofolios/buzon_documentos/CONSUMOFOLIOS_FECHA31122018_RUT111111111_ENVIO.xml
<br>
<br><b>Obtener archivo Xml desde Windows:</b>
<br>c:\curl\curl.exe -o c:\curl\CONSUMOFOLIOS_FECHA31122018_RUT111111111_ENVIO.xml http://www.factronica.cl/sdk/factronica_consumofolios/buzon_documentos/CONSUMOFOLIOS_FECHA31122018_RUT111111111_ENVIO.xml
<hr>
<h3>Proceso 4: Obtener Archivo XML TrackID:</h3>
Este proceso es necesario para poder validar que el SII Chile haya recibido el documento emitido.
<br>
<br><b>Obtener Archivo Xml desde Linux:</b>
<br>curl -o CONSUMOFOLIOS_FECHA31122018_RUT111111111_TRACKID.xml http://www.factronica.cl/sdk/factronica_consumofolios/buzon_documentos/CONSUMOFOLIOS_FECHA31122018_RUT111111111_TRACKID.xml
<br>
<br><b>Obtener archivo xml desde Windows:</b>
<br>c:\curl\curl.exe -o c:\curl\CONSUMOFOLIOS_FECHA31122018_RUT111111111_TRACKID.xml http://www.factronica.cl/sdk/factronica_consumofolios/buzon_documentos/CONSUMOFOLIOS_FECHA31122018_RUT111111111_TRACKID.xml
