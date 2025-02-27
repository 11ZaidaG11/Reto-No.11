# Reto-No.11
### 1. Consulte que hacen los siguientes métodos de strings en python:  
Estos metodos regresan True cuando... :  
- ```endswith```: La cadena empieza con un prefijo dado, se le pueden dar más parametros (prefijo, start, stop)
- ```startswith```: La cadena termina con un sufijo dado, se le pueden dar más parametros (sufijo, start, stop)
- ```istitle```: La primera letra de cada palabra es mayúscula.  
- ```islower```: Todas las letras en la cadena son minúsculas.  
- ```isupper```: Todas las letras en la cadena son Mayúsculas.  

...todos los caracteres de la cadena son:
- ```isalpha```: Letras.  
- ```isalnum```: Letras y/o números.  
- ```isdigit```: Números.  
- ```isspace```: Espacios.  

### 2. Procesar el archivo y extraer:
- Cantidad de vocales  
- Cantidad de consonantes  
- Listado de las 50 palabras que más se repiten

```
def vocales(archivo) -> int:
    vocal = "aeiouAEIOU"
    cuenta_v = 0 # Inicializar

    for i in archivo: # Por cada linea en el archivo
        for j in i: # Por cada caracter en cada linea
            if j in vocal:
                cuenta_v += 1
            else:
                pass
    return cuenta_v

def consonantes(archivo) -> int:
    conso = "bcdfghjklmnpqrstvwxyzBCDFGHJKLMNPQRSTVWXYZ"
    cuenta_c = 0

    for i in archivo: # Por cada linea en el archivo
        for j in i: # Por cada caracter en cada linea
            if j in conso:
                cuenta_c += 1
            else:
                pass
    return cuenta_c

def repetidas(archivo) -> list:
    palabras = []
    for i in archivo: # Separa el texto en plabras
        palabras += i.split()

    conteo = {} # key= palabra : Value= No. de apariciones
    for i in palabras: # For para contar las palabras
        if i not in conteo: # Si la palabra no esta en el dicionario inicia la cuenta
            conteo[i] = 1
        else:
            conteo[i] += 1

    # http://docs.python.org/es/3.13/howto/sorting.html
    orden = sorted(conteo.items(), key=lambda item: item[1], reverse=True) # Orden de mayor a menor
    orden_dic = dict(orden)

    cuenta = 0 # Inicializar cuenta
    cincuenta = []
    while True: # Para guardar los primeros 50 elementos del diccionario
        for i in orden_dic:
            cincuenta.append(i)
            cuenta += 1
            if cuenta == 50:
                break
        
        return cincuenta


if __name__ == "__main__":
    with open("mbox.txt") as archivo:
        uno = vocales(archivo)
        archivo.seek(0) # Regresar al inicio del archivo
        dos = consonantes(archivo)
        archivo.seek(0)
        tres = repetidas(archivo)

        print(f"Vocales: {uno}\nConsonantes: {dos}")
        print("Las 50 palabras más repetidas son:")
        indice = 0
        for i in tres:
            indice += 1
            print(indice, "-", i)
```
