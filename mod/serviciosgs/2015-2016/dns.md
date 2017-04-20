---
layout: index

title: Servicios de Red e Internet
tagline: CFGS ASIR
---
### Práctica: Servidor DNS

#### (8 tareas - 25 puntos)(3 tareas obligatorias - 10 puntos)

#### Escenario

1. En nuestra red local tenemos un [servidor Web](web) que sirve dos páginas web: *www.iesgn.org*, *departamentos.iesgn.org*
2. Vamos a instalar en nuestra red local un servidor DNS (lo puedes instalar en el mismo equipo que tiene el servidor web)
3. Voy a suponer en este documento que el nombre del servidor DNS va a ser *pandora.iesgn.org*

#### Servidor DNSmasq

Instala el servidor dns **dnsmasq** en *pandora.iesgn.org* y configúralo para que los clientes puedan conocer los nombres necesarios.

<div class='ejercicios' markdown='1'>

* **Tarea 1 (2 punto)(Obligatorio):** Modifica los clientes para que utilicen el nuevo servidor dns. Realiza una consulta a www.iesgn.org, y a www.josedomingo.org. Realiza una prueba de funcionamiento para comprobar que el servidor dnsmasq funciona como cache dns. Documenta la tarea en redmine.
</div>

#### Servidor bind9 

Desinstala el servidor **dnsmasq** del ejercicio anterior e instala un servidor dns **bind9**.  Las características del servidor DNS que queremos instalar son las siguientes:

* El servidor DNS se llama *pandora.iesgn.org* y por supuesto, va a ser el servidor con autoridad para la zona *iesgn.org*.
* Vamos a suponer que tenemos un servidor para recibir los correos que se llame correo.iesgn.org y que está en la dirección x.x.x.200 (esto es ficticio).
* Vamos a suponer que tenemos un servidor ftp que se llame ftp.iesgn.org y que está en x.x.x.201 (esto es ficticio)
* Además queremos nombrar a los clientes.
* También hay que nombrar a los virtual hosts de apache: www.iesgn.org y departementos.iesgn.org
* Se tienen que configurar la zona de resolución inversa.

<div class='ejercicios' markdown='1'>
* **Tarea 2 (4 puntos)(Obligatorio):** Realiza la instalación y configuración del servidor bind9 con las características anteriomente señaladas. Muestra el resultado al profesor.
* **Tarea 3 (4 puntos)(Obligatorio):** Realiza las consultas dig/nslookup desde los clientes preguntando por los siguientes:
	* Dirección de *pandora.iesgn.org*, www.iesgn.org, ftp.iesgn.org
	* El servidor DNS con autoridad sobre la zona del dominio iesgn.org
	* El servidor de correo configurado para iesgn.org
	* La dirección IP de www.josedomingo.org
	* Un resolución inversa
</div>

#### Servidor DNS esclavo

El servidor DNS actual funciona como **DNS maestro**. Vamos a instalar un nuevo servidor DNS que va a estar configurado como **DNS esclavo** del anterior, donde se van a ir copiando periódicamente las zonas del DNS maestro. Suponemos que el nombre del servidor DNS esclavo se va llamar *afrodita.iesgn.org*.

<div class='ejercicios' markdown='1'>

* **Tarea 4 (3 puntos):** Realiza la instalación del servidor DNS esclavo. Documenta los siguientes apartados:
	* Entrega la configuración de las zonas del maestro y del esclavo.
	* Comprueba si las zonas definidas en el maestro tienen algún error con el comando adecuado.
	* Comprueba si la configuración de named.conf tiene algún error con el comando adecuado.
	* Reinicia los servidores y comprueba en los logs si hay algún error. **No olvides incrementar el número de serie en el registro SOA si has modificado la zona en el maestro**.
	* Muestra la salida del log donde se demuestra que se ha realizado la transferencia de zona.
* **Tarea 5 (3 puntos):** Docuemnta los siguientes apartados:
	* Configura un cliente para que utilice los dos servidores como servidores DNS.
	* Realiza una consulta con dig tanto al maestro como al esclavo para comprobar que las respuestas son autorizadas. ¿En qué te tienes que fijar?
	* Solicita una copia completa de la zona desde el cliente ¿qué tiene que ocurrir?. Solicita una copia completa desde el esclavo ¿qué tiene que ocurrir?
* **Tarea 6 (2 puntos):** Muestra al profesor el funcionamiento del DNS esclavo:
	* Realiza una consulta desde el cliente y comprueba que servidor está respondiendo.
	* Posteriormente apaga el servidor maestro y vuelve a realizar una consulta desde el cliente ¿quién responde?
</div>


#### Delegación de dominios

Tenemos un servidor DNS que gestiona la zona correspondiente al nombre de dominio *iesgn.org*, en esta ocasión queremos delegar el subdominio *informatica.iesgn.org* para que lo gestione otro servidor DNS. Por lo tanto tenemos un escenario con dos servidores DNS:

* *pandora.iesgn.org*, es servidor DNS autorizado para la zona **iesgn.org**.
* *ns.informatica.iesgn.org*, es el servidor DNS para la zona **informatica.iesgn.org** y, está instalado en otra máquina.

Los nombres que vamos a tener en ese subdominio son los siguientes:

* **www.informatica.iesgn.org** corresponde a un sitio web que está alojado en el servidor web del departamento de informática.
* Vamos a suponer que tenemos un servidor ftp que se llame **ftp.informatica.iesgn.org** y que está en la misma máquina.
* Vamos a suponer que tenemos un servidor para recibir los correos que se llame **correo.informatica.iesgn.org**.

<div class='ejercicios' markdown='1'>
* **Tarea 7 (4 puntos):** Realiza la instalación y configuración del nuevo servidor dns con las características anteriomente señaladas. Muestra el resultado al profesor.
* **Tarea 8 (3 puntos):** Realiza las consultas dig/neslookup desde los clientes preguntando por los siguientes:	

	* Dirección de www.informatica.iesgn.org, ftp.informatica.iesgn.org
	* El servidor DNS que tiene configurado la zona del dominio informatica.iesgn.org. ¿Es el mismo que el servidor DNS con autoridad para la zona iesgn.org?
	* El servidor de correo configurado para informatica.iesgn.org
</div>

[Volver](index)

