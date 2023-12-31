# PARCIAL 2

## Arreglos y cadenas

**Como funcionan?**  
Estructuras de datos que almacenan valores. Los arreglos almacenan valores del mismo tipo, mientras que cadenas es un arreglo de caracteres.

**Como se cargan, muestran y copian?**  
Se pueden cargar asignando cuando se crean, o ingresando por teclado. Para cargar un arreglo o cadena, se debe tener en cuenta la capacidad maxima del mismo. Para cargar por teclado se hace con una interacion **for** que recorre desde el indice 0 hasta la cantidad (que no es lo mismo que la capacidad). En las cadenas se puede saber cuando se termina por el terminado /0.  
Se muestran recorriendo los indices del arreglo (en caso de que se quiera mostrar de manera separada) o mostrando directamente la cadena con **%s** . Se copian recorriendo con un bucle el arreglo original y guardando los valores en otro arreglo.

**Que implica la capacidad de un arreglo?**  
La capacidad de un arreglo es el numero maximo de elementos que puede contener un arreglo. Esto se define al declarar el arreglo y no puede cambiarse despues. En caso de sobrepasar esta capacidad, se podria provocar que acceda a memoria reservada para otros programas.

**Como se pasa a una funcion?**  
Por referencia o copia. Se le asigna como **funcion(arreglo);** sin la capacidad del arreglo

## Matrices

**Como funcionan?**  
Son arreglos bidimensionales, arreglos de arreglos. Se las puede asociar a tablas, tableros, etc. De forma: arreglo[fila][columna].

**Como se crean, cargan, muestren y copian?**  
Se crean primero declarando el numero de filas y columnas, y despues inicializandola con los valores.

```c
int fila = 3;
int columna = 3;
int matriz[fila][columna];
```

En este caso es una matriz de 3x3.
Se muestran con un bucle. Se copia de la misma forma, utilizando bucles.

**Como se pasan a funcion?**  
Especificando sus dimnesiones, o utilizando punteros de matrices:

```c
funcion(matriz); //Especificando dimensiones

void funcion_matriz(int (*matriz)[3], int filas, int columnas) //Funcione que recibe un puntero a una matriz
funcion_matriz(matriz,3,3) // Asignando a la funcion los parametros
// La matriz se modifica dentro de la funcion y los cambios se reflejan en la matriz original
```

## Punteros

**Como funcionan?**  
Son variables que almacenas direcciones de memorias en lugar del valor directo. Por ejemplo, en vez de guardar el valor de numero = 42, almacena la direccion de memoria en donde se encuentra almacenado el valor.

**Como se opera con ellos?**  
Con los operadores de direccion & o de desreferencia \* (Desrefenciar es obtener el valor que esta almacenado en la direccion de memoria a donde hace referencia el puntero). Ejemplo:

```c
int numero = 30;
int *ptr_numero = &numero;
```

**numero** es una variable de tipo entero que contiene el valor 30. Este valor sera almacenado en algun lugar de la memoria.  
**&numero** indica precisamente en que direccion de memoria esta almacenado el 30.
**ptr_numero** es otra variable que en vez de contener un entero, contiene direcciones de memoria, en este caso la direccion de memoria de la variable numero. Esta direccion se expresa en hexadecimal y para mostrarla es con 0x%p (0x es por el hexadecimal)

**Como se pasa a una función?**  
Se pasan como argumentos. Cualquier modificacion en la funcion a la que se le pasa como parametro, se vera modificada en el valor al que apunta, sin que sea necesario un return de la funcion.

**En que se diferencian de los arreglos?**  
Los punteros pueden apuntar a diferentes ubicaciones de memoria, mientras que los arreglos son coleccion de elementos contiguos en memoria.

**Como afectan el pasaje de argumentos?**  
Los punteros afectan el pasaje de argumentos porque cualquier modificacion realizada en la funcion se vera reflejada en el main, ya que la modificacion se realiza en el valor al que apunta en direccion de memoria

## Archivos

**Como se abren?**  
Para trabajar con archivos primero hay que abrirlos. Se necesita un puntero al archivo para poder leerlo y escribir, esto se hace con un puntero al archivo de tipo FILE.

```c
FILE *archivo;
archivo = fopen(nombre_archivo, "modo de apertura");
```

Si el archivo que se quiere abrir no existe, se crea automaticamente con el nombre especificado.

**Como funcionan?**

1. Abrir el archivo.
2. Realizar las operaciones de entrada/salida (lectura y/o escritura de datos en el archivo).
3. Cerrar el archivo.

Una vez abierto y especificado el modo de apertura es como se va a manejar el archivo. Los modos son:
**r**: Abre el archivo solo para lectura.  
**w**: Abre el archivo para escritura (crea un archivo nuevo o sobreescribe el existente)  
**a**: Abre el archivo para escritura, si existe, agrega datos al final; si no existe, crea uno nuevo  
**r+** : Abre el archivo para lectura / escritura  
**w+**: Crea un archivo para lectura / escritura  
**a+**: Añade o crea un archivo de texto para lectura / escritura.  
**b**: Abre el archivo binario

**fprintf(FILE \*archivo, formato, valores que se imprimen)**: Escribe contenido dentro del archivo. Se puede utilizar las veces que se quiera, salvo que se cierre el archivo. En caso de error, devuelve un valor negativo.

**fscanf(FILE \*archivo, formato, donde se guarda)** : Lee contenido dentro del archivo. Devuelve el numero de valores que han sido leidos y almacenados en variable. Si no ha podido leer mas valores es porque llego al final del archivo, devuelve EOF.

**int fputc(int caracter, FILE \*archivo)**: Escribe en el archivo el caracter contenido en el parametro caracter. Devuelve el valor de escritura. En caso de errorm devuelve EOF.

**char *fgets( char cadena[], int max, FILE *archivo )**: Lee una secuencia de caracteres del archivo asociado al parámetro archivo y los almacena en el parámetro cadena. La lectura termina cuando se hayan leído max-1 caracteres, se encuentre un salto de línea o se acabe el archivo. Si se encuentra un salto de línea, este se incluirá en la cadena.

**int fgetc( FILE \*archivo )**: Lee un caracter del archivo asociado al parametro archivo. Devuelve el carácter leído. Si no se puede leer ningún carácter, devuelve el valor EOF.

**int feof( FILE \*fich )**: Cuando la posición de lectura del archivo se encuentra al final del archivo, no se puede seguir leyendo. Durante la lectura de datos de un archivo, el programa debe comprobar si se ha llegado al final del archivo. Devuelve verdadero (distinto de 0) si se ha intentado leer despues de llegar al final del archivo y falso (0) en caso contrario.

**fclose(FILE \*archivo)**: Cuando se termina de utilziar el archivo, se tiene que cerrar. La variable de tipo FILE \* queda libre y puede ser utilizada para acceder a otro fichero. Devuelve 0 si cerro correctamente, EOF en caso contrario

**¿Cómo sé cuando una operación falló? ¿Cómo puedo obtener detalles?**  
La macro NULL, este método detecto cualquier error al abrir un archivo: como por ejemplo disco lleno o protegido contra escritura antes de comenzar a escribir en él. Utilizar **errno** para valor de retorno y **perror** para imprimir un mensaje de error asociado al valor de **errno**

## Estructuras

**¿Entiendo como funcionan?**  
Permite agrupar varios campos con diferentes tipos de datos

Se declara utilizando la palabra clave **struct**

```c
struct Persona
{
    char nombre[50];
    int edad;
    float altura;
};
//Se crea una variable con la instancia de la estructura
struct persona persona1;
// Se puede acceder al nombre usando persona1.nombre
// Se inicializa de la siguiente forma:
struct Persona persona2 = {"Jean", 24, 1.70}; // Inicialización al declarar
persona1.nombre = "Pepito"; // Inicialización después de la creación
persona1.edad = 25;
persona1.altura = 1.80;
// Se accede:
printf("Nombre: %s\n", persona2.nombre);
printf("Edad: %d\n", persona1.edad);
printf("Altura: %.2f\n", persona1.altura);
// Para pasar a funcion
void imprimir_persona(struct Persona p)
{
    printf("Nombre: %s\n", p.nombre);
    printf("Edad: %d\n", p.edad);
    printf("Altura: %.2f\n", p.altura);
}
imprimir_persona(persona1);
imprimir_persona(persona2);

// Se pueden crear estructuras anidadas:
struct Direccion
{
    char calle[50];
    int numero;
};

struct Contacto
{
    char nombre[50];
    struct Direccion direccion;
};
```

Se puede utilizar **typedef** para darle un nombre mas corto a la estructura:

```c
typedef struct
{
    char nombre[50];
    int edad;
} Persona_t;

// En vez de usar struct persona persona1, se usaria:
Persona_t persona1; //_t para indicar que es estructura
```

## Memoria dinamica

**¿Entiendo por qué existe aparte de la automática?**  
Es memoria que se reserva en tiempo de ejecucion. El tamaño puede variar durante la ejecucuion del mismo, es necesaria la memoria dinamica cuando no se sabe cuantos datos o elemenentos se van a tratar. Una vez que el programa termine, hay que liberar la memoria para que otros programas puedan utilizarla
**¿Entiendo como se usa?**  
Suele estar almacenada en el heap, o almacenamiento libre, mientras que la memoria estatica esta en el stack o pila. En el heap, el tamaño de memoria podria estar limitado a lo que use el programa durante la ejecucion y a la memoria disponible del sistema operativo. A su vez, es mas dificil de manejar que la estatica, porque se reserva de forma explicita y continua existiendo hasta que sea liberada.  
**¿Entiendo que es un ALV/VLA?**  
VLA significa **variant lenght array**, significa que se determina el tamaño del array en la ejecucion del programa, sin especificarlo antes de que arranque, su tamaño puede ir variando a lo largo de la ejecucion segun la cantidad de datos que se trate.  
**¿Entiendo que es un puntero genérico?**  
Es un puntero void (void *), puede apuntar a la direccion de cualquier tipo de dato, sin tener que hacer una conversion explicita del mismo. Si se referencia una variable de tipo int, la variable referenciada por el puntero es de tipo int, si es tipo float la variable, la referenciada por el puntero es de tipo float. Esto se logra mediante un casteo, el compilador no sabe a que tipo de dato se esta apuntando durante la ejecucion del programa, asi que se realiza el casteo al tipo de dato. 
 
 ``` c
 void * voidptr;
 int numero = 50;
 int arreglo[3] = {33,10,22};
 voidptr = &numero;
 * (int*)voidptr = 345 

 voidptr = arreglo;
 printf("Valor %d", *(int *)voidptr);
 ```

**Comos se asigna?** 
sizeof: Devuelve el numero de bytes que se utilizan para almacenar un tipo de dato.
malloc: Asigna el numero especificado en bytes
realloc: Aumenta o disminuye el tamaño de bloque de memoria. Reasigna si es necesario
calloc: Asigna el numero especificado en bytes y lo inicializa en 0 a todos los bloques.
free: Libera el bloque de memoria especificado.

## Argumentos por línea de comandos 

**¿Entiendo como funcionan?**  
Son argumentos que se escriben en la terminal que se va a ejecutar el programa. Por ejemplo
```
gcc -o ejercicio1.c multiplicacion
./multiplicacion.exe 2 3   
```
En la funcion main, se va a tener : 
``` c
int main(int argc, char* argv[])
{
    //resto del codigo
}
```
Le estoy pasando como parametros a la funcion main, el numero 2 y 3. El primer valor de los argumentos por linea de comandos, el 0, es el nombre del programa, en este caso multiplicacion. Despues se tienen el valor numerico 2 en la posicion 1, y 3 en la posicion 2.  

**¿Entiendo como se usan?**  
Asi como el nombre del programa es el indice 0 del argv[], si se desea verificar que tengan la cantidad de argumentos, se tiene que saber que se ingresa. Por ejemplo si tengo la suma de dos numeros, ya tengo la posicion 1 y 2 con los respectivos numeros, si cuando ejecuto el programa, argc, que es la cantidad de argumentos, es distinto de 3, ya se que me estan faltando o sobrando argumentos.  
Para usar los valores pasado por argumentos, se guardan en variables, segun el tipo de dato que sea. Al ser ingresados por teclado, son caracteres, para tipo de dato numerico se tiene que hacer una conversion. Ejemplo:

```c
int main (int argc, char*argv[])
{
    if (argc!= 3) 
    {
        printf("Faltan argumetnos.");
    }
    int numero1 = atoi(argv[1]); //atoi convierte una serie de caraceteres en un valor entero 
    char[20] = argv[2]; //al ser una serie de caracteres, no es necesario la conversion.
}
```

Para mostrar los argumentos podemos usar un bucle que recorra todos los argument value y los muestre por pantalla, como es por indice, se haria con un for. 
