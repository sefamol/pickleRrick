Pickle Rick es un CTF de nivel inicial de THM, en el cual se nos encomienda convertir nuevamente en humano a rick, que en esos momentos se encuentra convertido en pepinillo. Para esa tarea debemos encontrar en la computadora de Rick los 3 ingredientes necesarios para que este regrese a su estado de humano.
Para ello primero realizamos a enumeración y el reconocimiento del sistema investigado
Enumeración
## nmap
Utilizando el comando `nmap -sC -sV 10.10.242.104 -oN nmapPick` obtenemos los siguientes resultados:

![Pasted image 20230218112511](https://user-images.githubusercontent.com/24280145/222928607-be1992f4-4dd1-4fa3-90a8-a47f34a60522.png)

**puertos abiertos**

`http 80`

`ssh 22`

## curl
utilizando el comando  `curl 10.10.242.104 > cPick`

![Pasted image 20230218110137](https://user-images.githubusercontent.com/24280145/222929129-a3ba3365-6c73-4dac-93e1-e80f1da6bb2b.png)

Encontramos un nombre de usuario en el documento HTML 

`Username: R1ckRul3s`


## Gobuster
Utilizando el comando `gobuster -u http://10.10.242.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt` obtenemos lo siguiente

![Pasted image 20230218113243](https://user-images.githubusercontent.com/24280145/222929984-b355969d-1b50-49a6-a771-f3c85499b9b2.png)

Buscamos directorios con extensión .php y .html  `gobuster -u http://10.10.242.104 -t 50 -w /usr/share/wordlists/dirbuster/common.txt -x .php,.html`

**Nota**: La lista common.txt fue extraida de: https://gitlab.com/kalilinux/packages/dirb/blob/f43c03a2bef91118debffd6cec9573f21bb5f9e8/wordlists/common.txt
Utilizamos el comando `sudo mv common.txt /usr/share/wordlists/dirbuster/common.txt` para mover el archivo a la carpeta dirbuster (no es obligatorio)
