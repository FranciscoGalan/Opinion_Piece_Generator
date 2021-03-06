# Generador de artículos de opinión

El objetivo de este proyecto es crear un generador de artículos de opinión [1], es decir, un programa que automáticamente escriba artículos de opinión originales sobre hechos nacionales recientes. Además, el generador podrá escribir artículos opinión de acuerdo al estilo de cualquier autor. 


## Equipo



*   Francisco Álvarez
*   Francisco Galán
*   José María Ramos


## **Plan de trabajo**

Planeamos tomar diversos artículos de opinión de la web y utilizarlos como base para entrenar un modelo. Idealmente, buscamos obtener un modelo general que pueda ser entrenado con diferentes datos. De esta forma, podremos entrenarlo con los artículos de un autor en particular y reproducir su estilo. Por tanto, el modelo potencialmente podrá reproducir el estilo de cualquier autor. 

En general, el procedimiento que seguiremos será este: 




1. **Obtener los datos**. Haremos web scraping para obtener los artículos de opinión de al menos tres columnistas. Más adelante, una vez que tengamos un modelo funcional, podremos regresar a este paso y scrapear artículos de otros columnistas. 

2. **Limpiar los datos**. Debemos decidir cómo vamos a estructurar los datos. Por un lado, habrá que decidir si mantener la división de párrafos (quizá sea importante al momento de entrenar al modelo) y cómo. Por otro lado, sospechamos que es importante conservar caracteres especiales como acentos, comas, dos puntos, etc. **  
**
3. **Entrenar el modelo**. Nos falta investigar qué librerías y modelos podemos utilizar para crear el generador. Por lo pronto, estos son algunos candidatos: 
    *   Semantic brand score
    *   Topic modeling
    *   LDA
    *   Gensim
    *   Stanza
    *   Spacy
    *   NLTK 

4. **(Opcional) Enlazar con Twitter. **Si da tiempo, intentaremos que el modelo tome información en tiempo real de Twitter. Así, los artículos que se escriban serán sobre noticias recientes del país.


## Fechas de entrega



*   _1 - 8 marzo_: Scrapear información de internet. 
*   _8 - 12 marzo_: Limpiar y estructurar la información.
*   _12 - 20 marzo_: Seleccionar y entrenar el modelo.
*   _20 - 27 marzo_: Pulir detalles del modelo y elaborar la presentación para el HackShow.


## División del trabajo

Lo iremos planeando sobre la marcha. 


<!-- Footnotes themselves at the bottom. -->
## Notas

[1] En este tipo de artículos, un autor emite su opinión sobre hechos recientes de relevancia nacional. Por lo general, estos artículos suelen aparecen en la sección de Opinión de periódicos como_ Reforma_, _El Universal_, _La Jornada_, entre otros. 
