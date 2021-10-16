# Unidad 3 

## Escribir 3 frases de no más de 10 palabras y pasarlas por los mecanismos de algoritmos, postearlo en el foro (al final de la unidad, links de ayuda)

```console
$ echo "no creo que hoy llueva, es fin de semana largo" | md5
a865bc57fea62eca77b9231e0b98f3af

$ echo "creo que hoy voy a comer pastas" >> mi-archivo.txt
$ openssl enc -aes-256-cbc -salt -in mi-archivo.txt -out file.enc
enter aes-256-cbc encryption password:
Verifying - enter aes-256-cbc encryption password:
$ cat file.enc 
Salted__$n a�`�`
                �t\�.�Z��ʕ�mfM3�Ԣ�|�h4������fއ�C�>Ї/&

$ echo "hola mundo" | base64
aG9sYSBtdW5kbwo=
$ echo aG9sYSBtdW5kbwo= | base64 -d
hola mundo
```

## Completar el ejemplo

1. David tiene un texto que quiere enviar a Ana.
2. David usa su clave para cifrar el texto y crear un texto cifrado.
3. David envía el documento a través de internet.
4. Ana recibe el texto cifrado
5. Ana usa _la misma clave_ que usó David para desencriptar el texto cifrado y poder leer el documento.

Este modelo simétrico asume que tanto el emisor como el receptor tienen la misma clave (shared key).

## Ejercicio LAB

CODIGO DESCIFRADO

