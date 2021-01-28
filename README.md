# Curso teorico Super intensivo de Vagrant, Ansible, Packer, Docker y Jenkins: #

### by Exequiel Germano ###

### Vagrant: ###

Vagrant es una herramienta la cual nos permite crear, iniciar, parar o destruir a nuestro antojo, la cantidad de Maquinas Virtuales que querramos (VM).

Esto lo podemos hacer gracias a la edición de un Vagrantfile, el cual es iniciado cuando previamente utilizamos mediante linea de comandos el comando:

     <vagrant init>

Este comando, nos crea en el directorio en el que nos encontremos, un archivo llamado Vagrantfile, el cual vamos a editar especificando todo lo necesario para que se levante la VM con lo que nosotros querramos.

Cosas como:

-Sistema Operativo
-Nombre de la VM
-Placa de Red
-Puertos por el cual acceder (entrada y salida)
-Software con el cual queremos que inicie la instancia
-etc etc…

Comandos a tener en cuenta:

     -vagrant init (crea nuestro Vagrantfile)
     -vagrant status (Ver el estado de nuestras VM)
     -vagrant up (Levanta nuestras VM)
     -vagrant ssh <nombre-de-vm> (conectamos a la VM)
     -vagrant halt (paramos nuestra VM)
     -vagrant destroy (Destruimos nuestra VM)

Despues hay muchas otras cosas que se pueden hacer con Vagrant como la de aprovisionar nuestra maquina sin la necesidad de destruirla, etc etc.

### Ansible: ###

Ansible es una herramienta de automatizacion muy poderosa que nos permite hacer cosas como el aprovisionamiento de una o de varias maquinas virtuales (o instancias, ya sean de manera local o de manera efimera como el cloud de AWS)

La magia de ansible se encuentra en la facilidad que nos da a la hs de instalar software o tools dentro de una maquina en especifico o en un conjunto de maquinas, permitiendonos automatizar procesos que de hacerlos de manera manual uno a uno, nos terminaria pareciendo una tarea engorrosa o tediosa, dejando lugar a la equivocacion humana y a muchos otros problemas que puedan ir surgiendo.

Para evitar todo tipo de problemas o equivocaciones humanas, gracias a Ansible, podemos mediante un archivo llamado inventori indicarle la VM, o al grupo o conjunto de VM que querramos aprovisionar.

Esto lo hacemos siguiendo una serie de parametros, clave valor, donde iremos especificando:

-grupo al que pertenece la VM
-nombre de la VM
-conexion a la VM
-puerto por el cual nos conectaremos de manera local a la VM (siempre el puerto 22 de ssh)
-directorio donde se encuentra la llave publica y privada (verificar cual de las dos)
-etc etc…

Ansible quizas paresca algo complejo, pero es bastante simple.

Solo hay que entender algunos conceptos de como trsabaja ansible.

El primero es entendiendo sobre la carpeta roles
y el segundo es entendiendo como podemos llamar a esta carpeta roles mediante un archivo llamado playbook.yml

Roles: la carpeta roles es una carpeta en la cual vamos a especificar los nombres de las carpetas con el rol que queremos instalar.

Ejemplo: /roles /apache2 /task /main.yml

Basicamente, mas o menos de esta manera se estructura un rol de ansible.

Dentro de la carpeta roles podemos tener varios roles como por ejemplo: apache, nginx, elasticsearch, mongo, mysql, etc etc…

Dentro de cada rol, tendremos una serie de carpetas que podemos ir editando, pero la mas importante (o por lo menos en este momento) es la carpeta task, la cual dentro contiene un archivo en formato yml, donde especificaremos mediante modulos, lo que queremos que se instale dentro de nuestras instancias (VM).

Una vez que tenemos nuestro archivo <main.yml> el siguiente paso es corroborar o verificar si nuestro archivo playbook.yml esta bien configurado.

Esto es depende de cada uno, quizas la mejor manera de hacerlo, es primero editar el playbook.yml con los softwares que queremos aprovisionar, para luego no olvidarnos, y a continuacion pasar a editar en la carpeta roles, uno a uno los roles que queremos agregar.

Dentro de nuestro archivo playbook.yml especificaremos a que maquinas vamos a querer aprovisionar, y que roles queremos que esa maquina luego levante.

Asique repasando, primero creamos un archivo llamado inventory en el cual indicamos la forma en la que ansible se va a comunicar con cual o cuales VM.

Luego creamos el archivo playbook.yml donde indicaremos a que VM queremos aprovisionar y que roles vamos a querer que levante.

A continuacion, dentro de la carpeta roles crearemos mediante el comando <ansible-galaxi init <nombre-del-rol>> la carpeta con el rol que vamos a estar creando.

Una vez que mas o menos tenemos esto encaminado, podemos ir probando los roles de ansible.

Ansible es una herramienta muy poderosa la cual entiende que si una tarea esta hecha, pasa a la otra. SI una tarea esta mal configurada, podremos ir a arreglarla y volver a tirar el comando necesario para que corra ese rol, y como dije anteriormente, es una herramienta la cual entiendde que si una tarea fue bien realizada, proseguira con la siguiente hasta que todo lo que vayamos instalando nos salga de manera exitosa.

Comandos:

     -sudo ansible-playbook -i inventory playbook.yml

(-i inventori especifica a que VM queremos llegar)
(playbook.yml contiene los roles que creamos previamente dentro de la carpeta roles, a los cuales ira a buscar)

Si todo sale bien, lo veras en la pantalla salir de color verde jeje, si sale mal te vas a dar cuenta.

Me estoy salteando cosas como la prueba que hicimos en la cursada donde creabamos 3 virtuales, una master la cual tenia acceso o conexion con el node1 y node2.

Un comando para corroborar dicha conexion, era habiendo configurado previamente nuestro <inventory>:

     -ansible -i inventory -m ping

(Tenemos que corroborar donde estamos parados, podemos usar pwd)

Si estamos dentro de la maquina <master> y le queremos pegar a la VM <node1> tenemos que especificarlo en la linea de comandos.
(Esto no lo recuerdo con seguridad pero cuando veas las clases lo vas a entender, no es para nada complejo)

Y bueno, basicamente esto es lo que hacemos con Ansible, como pudiste observar es una herramienta muy poderosa y que nos permite automatizar bastante nuestro trabajo, con lo cual, a ansible lo queremos mucho <3
