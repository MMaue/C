# Learn C

## Editor und Compiler

In Linux im Terminal lassen sich mit z.B. `gedit`, `emcs`, `nano`, `vim` Dateien erstellen und bearbeiten.
```bash
gedit file.cpp &
```
Das `&` am ende der Zeile wird verwendet, um den gedit-Prozess vom Terminal zu trennen.
Mit dem Compiler, in unserem Fall `gcc` lassen sich die c und cpp Dateien in eine ausführbare Datei umwandeln.
```bash
gcc file.cpp -o file.out
```
Die kompilierte Datei kann man vom Terminal ausführen.
```bash
./file.out
```

In der `CodeBlocks` IDE lassen sich ebenfalls Dateien erstellen und mit `gcc` kompilieren.

Ein erstes Beispiel-Programm:
```cpp
#include <stdio.h>

int main(){
	printf("Hello World!\n");
	return 0;
}
```

## code Basics

### Includes

In this section there will be a few examples to see the syntax and a few build in functions of c.  
Other Libraries can be included using:
```c
#include <stdio.h>
#include <stdlib.h>
```
Eigene header files können mit 
```c
#include "path/to/header.h"
```
eingebunden werden.  

### Präprozessordirektiven

Präprozessordirektiven werden unterhalb der Includes verwendet.
```c
#define PI 3.141592653589793
// an stelle von const float PI = 3.14159265;
```

### Kommentare

```c
/*
some multiline or inline comment
*/
// singleline or endofline comment
```

### Variablen und Pointer

Variablen lassen sich mit dem `type` und dem `namen` definieren. Mit dem `=` operator kann man der Variable einen Wert Zuweisen. Als `type` kann man `int`, `float`, `double` und `char` wählen. Mit brackets `[]` hinter einer variablen kann man ein array erzeugen. Bei der Zuweisung eines `char`s verwendet man single quotation marks `'`, wenn man einen string, also eine Zeichenkette, erzeugen will muss man ein array aus `char`s bilden. Hierzu kann man dann double quotation marks `"` verwenden, oder das array mit braces `{}` und einzelnen `char`s aufbauen. Wichtig ist hierbei `\0` als letzten `char` zu verwenden.
```c
int i; // Definition
i = 1; // Zuweisung
int j = -1; // Definition + Initialisierung
int age = 40;
const int numero = 5;
int array_of_int[] = {2, 4, 7, 3};
float num = 4.2;
double gpa = 3.6;
char grade = 'A';
char char_array[] = {'H', 'i', '\0'};
char myString[] = "Vatkio";
int array_xy[3][2] = {
    {1, 2},
    {3, 4},
    {5, 6}
};
```
Mehrdimensionale arrays können gebildet werden indem man mehrere brackets hintereinander schreibt. hier kann man außerdem die Dimensionen der array angeben.  

Pointer zeigen auf einen Wert, dass heißt sie enthalten den Wert der Speicheradresse.
```c
int a = 12;
double b = 3.4;
char c = 'A';
// prints out the memory address of a
printf("a: %p\n", &a);  
//pointers
int * ptr_a = &a;
double * ptr_b = &b;
char * ptr_c = &c;
```
>`*` is the dereference operator; it will grab the value at a memory address.  
>it is also used to declare a pointer variable.  
>`&` is the address-of operator; it will grab the memory address of a variable.
```c
// Declare integer x to be 45.
int x = 45;	
int *int_ptr = &x;
// int_ptr now points to the value of x.
// Any changes made to the value at int_ptr will also modify x.
x = 5;
// Now, the value of x is 5.
// This means that the value at int_ptr is now 5.	
*int_ptr = 2;
// Now, the value at int_ptr is 2
// This means that x is now 0.
int_ptr = NULL;
// int_ptr now no longer points to anything.
// Make sure you never leave a dangling pointer!   
```

### Structs

Mit structs lassen sich gleichartige werte für mehrere objekte speichern.
```c
struct Student{
    char name[50];
    char major[50];
    int age;
    double gpa;
};
```
Dieses struct kann folgendermaßen verwendet werden:
```c
struct Student stu;
stu.age = 29;
stu.gpa = 3.2;
strcpy(stu.name, "Jim");
strcpy(stu.major, "Business");
```

### printf

Mit der `printf` Funktion können Ausgaben in die Konsole geschrieben werden.
```c
printf("Hallo");
```
Man kann auch ein oder mehrere Variablen ausgeben.  
Wichtig ist hierbei einen format specifier anzugeben, der zeigt um welchen datentyp es sich handelt. Hier verwendet man `%i` oder `%d` für integer, `%f` für floating point numbers. Man kann den angezeigten Wert mit `%.3f` auf 3 Nachkommastellen begrenzen. Für einen double kann man `%lf` (long float) verwenden. Für einen char verwendet man `%c`, für einen string `%s`. Um einen Pointer auszugeben braucht man `%p`.
```c
char var[] = "a variable";
printf("some text and %s", var);
int a = 12;
printf("a: %i is stored at %p\n", a, &a);
float myFloat = 12.456793;
printf("%.3f", myFloat);
```
Es gibt noch [einige weitere format specifier](https://www.freecodecamp.org/news/format-specifiers-in-c/), wie `%e` für die scientific notation, `%x` für die hexadecimal Darstellung.
```c
printf("Characters: %c %c \n", 'a', 65);
printf("Decimals: %d %ld\n", 1977, 650000L);
printf("Preceding with blanks: %10d \n", 1977);
printf("Preceding with zeros: %010d \n", 1977);
printf("Some different radices: %d %x %o %#x %#o \n", 100, 100, 100, 100, 100);
printf("floats: %4.2f %+.0e %E \n", 3.1416, 3.1416, 3.1416);
printf("Width trick: %*d \n", 5, 10);
printf("%s \n", "A string");
```
output:
```
Characters: a A
Decimals: 1977 650000
Preceding with blanks:       1977
Preceding with zeros: 0000001977
Some different radices: 100 64 144 0x64 0144
floats: 3.14 +3e+000 3.141600E+000
Width trick:    10
A string
```
In strings kann man außerdem spezielle escape character verwenden, wie `\n` für eine new line, `\t` für einen tab, `\\` um ein backslash anzuzeigen, `\b` für backspace, `\'` für eine single quotation mark und `\"` für eine double quotation mark. 

### scanf und fgets

Mit der `scanf` Funktion kann man Werte einlesen und Variablen zuweisen. Die Funktion braucht die Speicheradresse der Variable, der der Wert zugewiesen werden soll. Daher wird der `&` operator hier verwendet.
```c
int number;
printf("Enter an integer:");
scanf("%d", &number);
```
Wenn man mehrere Werte gleichzeitig einlesen will, müssen die Werte mit einem Leerzeichen getrennt Werden.
```c
int number_1;
int number_2;
printf("Enter 2 integers:");
scanf("%d %d", &number_1, &number_2);
```
Wenn man Zeichenketten einlesen will, wird der `&` operator hier nicht benötigt. Das liegt daran, dass ein array, wie eine zeichenkette, auch als Pointer ausgewertet werden kann. 
```c
char mystring[12];
printf("Enter a string:");
scanf("%s", mystring);
// no '&' needed... array can be evaluated as a pointer
```
Wenn man als string mehrere mit Leerzeichen getrennte Wörter einlesen will braucht man die `fgets` Funktion, sie liest eine ganze Zeile ein, jedoch auch den `\n` newline character den man braucht, um die Eingabe zu bestätigen.
```c
char mystring[20];
printf("Enter fgets:");
fgets(mystring, 20, stdin);
```

### Funktionen

Ein ausführbares Programm in c hat immer eine `main` Funktion. Diese wird beim ausführen des Programms aufgerufen. Als Rückgabewert für einen erfolgreichen Programmdurchlauf wird hier 0 verwendet. Wenn es während des Programms zu Fehlern kommt sollte -1 zurückgegeben werden. 
```c
int main(int argc, char *argv[]){
	//main part of the programm
	return 0;
}
```
Nach Kompilieren des Programms in die `a.out` Datei kann man das Programm ausführen und Parameter an die `main` Funktion übergeben.
```bash
./a.out -o foo -vv
```
Die Variable `argc` enthält die Anzahl der Argumente von `argv`, dem Argument Vektor. In diesem Beispiel enthält `argv` folgende Werte:
```c
argv = {"/path/to/a.out", "-o", "foo", "-vv"};
```
`argv[0]` enthält immer den ganzen Pfad zur ausgeführten Datei.
[Hier findest du mehr information](https://opensource.com/article/19/5/how-write-good-c-main-function) zum Aufbau einer guten `main.c` Datei und der `main` Funktion.

Vor der `main` Funktion werden eigene Funktionen und Structs definiert.  
Wenn eine Funktion keinen Rückgabe Wert hat, gibt man als Typ `void` an. Wenn der Funktion Parameter übergeben werden sollen, müssen diese in den Parentheses angegeben werden.
```c
void some_function(char some_characters[]){
    printf("function called %s\n", some_characters);
}
```
Mit dem `return` keyword können werte einer Funktion zurückgegeben werden.
```c
double square_this_number(double num){
    double res = num * num;
    return res;
}
```
Wenn einer Funktion eine unbestimme Anzahl an Parametern übergeben werden soll wird eine `va_list` und die Anzahl der Argumente benötigt. Die Anzahl der Argumente wird hier als `num` übergeben. 
```c
int sum(int num, ...){
    va_list valist;
	va_start(valist, num);

    int summe = 0;
    int i;
    for (i=0;i<num;i++){
		// each call of va_arg will give next argument
        summe += va_arg(valist, int);
    }
    va_end(valist);
    return summe;
}
```
Die Funktion kann folgendermaßen verwendet werden.
Die erste 5 ist hier die Anzahl der Argumente, aus allen weiteren Zahlen wird die Summe gebildet und zurückgegeben.
```c
printf("Summe: %d\n", sum(5, 1,2,3,4,5));
```

### if-else

Mit der if-else Struktur, als Kontrollstruktur, können bedingte Anweisungen implementiert werden. Erst wenn eine bestimmte Bedingung erfüllt ist wird bestimmter code ausgeführt.
```c
if (condition) {
	code
} else if (condition) {
	code
} else {
	code
}
```
Das wird in diesem Beispiel verwendet werden, um die größere zweier Zahlen zu finden.
```c
double max(double num1, double num2){
    if (num1>num2) {
        return num1;
    } else {
        return num2;
    }
}
```

### switch-case

Wie mit if-else kann hier zwischen verschiedenen Fällen unterschieden werden. Wenn allerdings ein bestimmter Ausdruck ausgewertet werden soll ist es einfacher und übersichtlicher switch-case zu verwenden.
```c
char grade = 'A';
switch(grade){
case 'A':
    printf("really good grade");
	break;
case 'B':
    printf("good grade");
    break;
case 'C':
    printf("ok grade");
    break;
default:
    printf("._.");
}
```

### Schleifen

Mit einer for-loop kann man mit einer Zählvariable, in dem Fall `i` code mehrfach hintereinander ausführen. `i` wird hier zuerst definiert und bekommt anschließend in der loop den Startwert 1 zugewiesen. Während jedem Schleifendurchlauf wird `i` um 1 inkrementiert, `i++`. Die Schleife läuft solange `i<=5` erfüllt ist. 
```c
int i;
for(i=1;i<=5;i++){
    printf("%d\n", i);
}
```
Gleiches kann auch mit einer while-loop erzeugt werden.
```c
int i = 1;
while(i<=5){
    printf("%d\n", i);
    i++;
}
```
Gleiches kann auch mit einer do-while-loop erzeugt werden, allerdings wird der code innerhalb der Schleife mindestens einmal ausgeführt, auch wenn die Bedingung, in dem Fall `i<=5` hier vor Schleifenbeginn nicht erfüllt ist.
```c
int i = 6;
do {
    printf("%d\n", i);
    i++;
}while(i<=5);
```
Wenn man für jedes Element einer Array eine bestimmte berechnung durchführen will könnte man das folgendermaßen machen.
```c
// loop through array
int i, length, myArray[5]= {1, 2, 3, 4, 5};
length = sizeof(myArray) / sizeof(int); // 20/4=5

for(i=0;i<length;i++){
    printf("%d,", myArray[i]);
}
```
Wenn man eine 2-Dimensionales Array hat braucht man eine nested loop.
```c
int array_xy[3][2] = {
    {1, 2},
    {3, 4},
    {5, 6}
};
int i, j, rows, cols;
cols = sizeof(array_xy[0]) / sizeof(int);
rows = (sizeof(array_xy) / sizeof(int))/cols;

for(i=0;i<rows;i++){
    for(j=0;j<cols;j++){
        printf("%d,", array_xy[i][j]);
    }
    printf("\n");
}
```

### write files

Mit der `fprintf` Funktion kann man in Dateien schreiben.  
Wenn man die Datei im `w`wite-mode öffnet wird die Datei erstellt, wenn sie noch nicht existiert, oder überschrieben, wenn sie existiert.  
Wenn man die Datei im `a`ppend-mode öffnet kann man mit `fprintf` an das Ende der Datei schreiben.

```c
FILE * fpointer = fopen("mytextfile.txt", "w");
fprintf(fpointer, "Lelly\nKelly\nKel\nNelle\n");
fclose(fpointer);
```
Alternativ kann man mit der `fputs` Funktion im `a`ppend mode Text an das Ende der Datei schreiben.
```c
fputs("some text\n", fpointer);
```

### read files

Einzelne Zeilen lassen sich folgendermaßen lesen: 
```c
char line[255];
FILE * fpointer_2 = fopen("mytextfile.txt", "r");
fgets(line, 255, fpointer_2); // reads first line
printf("%s", line);
fclose(fpointer_2);
```

Alternativ kann man einzelne Zeichen mit einer loop lesen bis man alles aus der Datei gelesen hat, als bis man das End-Of-File `EOF` erreicht hat.
```c
FILE *ptr;
ptr = fopen("mytextfile.txt", "r");
char c;
c = fgetc(ptr);
while(c!=EOF){
    printf("%c", c);
    c = fgetc(ptr);
}
```

### Manuelle Speicherzuweisung

```c
char * description;
description = malloc(200*sizeof(char));
if(description==NULL){
    return -1;
} else {
    strcpy(description, "Die ist eine Buchbeschriebung");
}
printf("%s\n", description);
//description = realloc(description, 100*sizeof(char));
free(description);
```

## c modules

### math.h

Mit `math.h` kann man auf mathematische funktionen zugreifen.
```c
pow(2, 3)
sqrt(2)
ceil(36.34)
floor(36.34)
``` 
zugreifen.

### string.h

Mit `string.h` kann man auf funktionen zugreifen, die zeichenketten verarbeiten können.
```c
// kopiert myString in ergebnis
strcpy(ergebnis, myString);
// concatonate 2 strings
strcat(myString2, myString);
strlen(myString) // retunrs lentgh
```
