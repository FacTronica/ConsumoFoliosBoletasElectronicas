# Consumo de Folios Boletas Electrónicas
SDK Factronica
<br>A continuación se detalla el Procedimiento para realizar la integración con Software Propio.
<h3>Procesos a Realizar:</h3>
1.-Generar Archivo Plano TXT Consumo de Folios
<br>2.-Enviar Archivo Plano TXT al Servidor de Facturación
<br>3.-Recuperar Archivo XML con TrackID
<br>4.-Recuperar Archivo XML Consumo de Folios
<hr>
<h3>Proceso 1: Generar Archivo Plano Consumo de Folios</h3>
Este proceso Consiste en generar un archivo de texto plano con el formato requerido por el sdk de factronica.
<br>-Servidor Facturación
<br>-Datos de Caratula
<br>-Datos de Emisor
<br>-Datos de Resumen
<br>-Datos de Certificado
<br>Ver Formato del archivo TXT para Consumo de Folios.
<br>Ejemplo: https://gitlab.com/factronica/consumofolios/blob/master/consumofolios_ejemplo.txt
<br>
<hr>
<h3>Proceso 2: Enviar Archivo Txt</h3>
<b>Enviar archivo desde Consola Linux:</b>
<br>curl --form "archivotxt=@consumofolios.txt" http://www.factronica.cl/servidores/servidor_v727/recibe_txt_consumofolios.php
<br>
<br><b>Enviar archivo txt desde Consola Windows:</b>
<br>c:\curl\curl.exe --form "archivotxt=@c:\curl\consumofolios.txt" http://www.factronica.cl/servidores/servidor_v727/recibe_txt_consumofolios.php
<br>
<hr>
<h3>Proceso 3: Recuperar el XML con TrackID:</h3>
Este proceso es necesario para poder validar que el SII Chile haya recibido el documento emitido.
<br>
<br><b>Recuperar Archivo Xml desde Linux:</b>
<br>curl -o cfolios20160712_trackid.xml http://www.factronica.cl/servidores/servidor_v727/consumofolios/cfolios20160712_trackid.xml
<br>
<br><b>Recuperar archivo xml desde Windows:</b>
<br>c:\curl\curl.exe -o c:\curl\cfolios20160712_trackid.xml http://www.factronica.cl/servidores/servidor_v727/consumofolios/cfolios20160712_trackid.xml
<hr>
<h3>Proceso 4: Recuperar el XML Consumo de Folios:</h3>
Este proceso es necesario para poder obtener una copia del xml del archivo Consumo de folios.
<br>
<br><b>Recuperar archivo Xml desde linux:</b>
<br>curl -o cfolios20160712_consumo.xml http://www.factronica.cl/servidores/servidor_v727/cfolios20160712_consumo.xml
<br>
<br><b>Recuperar archivo Xml desde Windows:</b>
<br>c:\curl\curl.exe -o c:\curl\cfolios20160712_consumo.xml http://www.factronica.cl/servidores/servidor_v727/cfolios20160712_consumo.xml