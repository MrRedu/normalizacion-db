# Normalización de bases de datos

Serie de pasos o reglas que se deben seguir seguir para crear bases de datos funcionales. **Evitando redundancia e inconsistencia de los datos** para crear una base de datos optimizada.

Cuenta de varios pasos, conocidos como **Formas Normal (1FN, 2FN, 3FN, Boyce Cood, 4FN y 5FN)**

## Primera FormaNormal **(1FN)** / _Comprobación y cero clonación_

Tabla de películas
| Títulos | Directores | Nacionalidades directores | Formato | Precio | Géneros | Duración | Puntuaciones | Productora ID |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| El padrino | Francis Ford Coppola | Americano | HD | 30 | **Gánsters, Drama** | 175 | A | 1 |
| Toy Story | John Lasseter | Americano | HD | 30 | **Animación, Aventura** | 81 | B | 2 |

1. ### Comprobación:
   Cada celda debe contener 1 dato. <br>
   No deben ser ni arreglos, ni datos divididos; si no, datos atómicos y planos.
2. ### Cero clonación:
   Eliminar grupos repetidos, separándolos.

#### Tabla de películas

|  Títulos   |      Directores      | Nacionalidades directores | Formato | Precio | Duración | Puntuaciones | Productora ID |
| :--------: | :------------------: | :-----------------------: | :-----: | :----: | :------: | :----------: | :-----------: |
| El padrino | Francis Ford Coppola |         Americano         |   HD    |   30   |   175    |      A       |       1       |
| Toy Story  |    John Lasseter     |         Americano         |   HD    |   30   |    81    |      B       |       2       |

#### Tabla de géneros

| ID género | Nombre género |
| :-------: | :-----------: |
|     1     |   Gánsteres   |
|     2     |     Drama     |
|     3     |   Animación   |
|     4     |   Aventura    |

> [!IMPORTANT]  
> Para vincular los géneros de cada película con los IDs correspondientes en la tabla de géneros, necesitas crear una tabla intermedia o de unión *(junction table en inglés)*. Esta tabla se utiliza para establecer una relación de muchos a muchos (many-to-many) entre las películas y los géneros.

#### Tabla de películas-géneros

|  Títulos   | ID género |
| :--------: | :-------: |
| El padrino |     1     |
| El padrino |     2     |
| Toy Story  |     3     |
| Toy Story  |     4     |

3. ### Comprobación:
   Cada tabla debe tener su llave primaria (PK)
