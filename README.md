# Normalización de bases de datos

Serie de pasos o reglas que se deben seguir seguir para crear bases de datos funcionales. **Evitando redundancia e inconsistencia de los datos** para crear una base de datos optimizada.

Cuenta de varios pasos, conocidos como **Formas Normal (1FN, 2FN, 3FN, Boyce Cood, 4FN y 5FN)**

## Primera FormaNormal **(1FN)** / _Comprobación y cero clonación_

Tabla de películas
| Título | Directores | Nacionalidades directores | Formato | Precio | Géneros | Duración | Puntuación | Productora ID |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| El padrino | Francis Ford Coppola | Americano | HD | 30 | **Gánsters, Drama** | 175 | A | 1 |
| Toy Story | John Lasseter | Americano | HD | 30 | **Animación, Aventura** | 81 | B | 2 |

1. ### Comprobación:
   Cada celda debe contener 1 dato. <br>
   No deben ser ni arreglos, ni datos divididos; si no, datos atómicos y planos.
2. ### Cero clonación:
   Eliminar grupos repetidos, separándolos.

#### Tabla de películas

|   Título   |      Directores      | Nacionalidades directores | Formato | Precio | Duración | Puntuaciones | Productora ID |
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
> Para vincular los géneros de cada película con los IDs correspondientes en la tabla de géneros, necesitas crear una tabla intermedia o de unión _(junction table en inglés)_. Esta tabla se utiliza para establecer una relación de muchos a muchos (many-to-many) entre las películas y los géneros.

#### Tabla de películas-géneros

|   Título   | ID género |
| :--------: | :-------: |
| El padrino |     1     |
| El padrino |     2     |
| Toy Story  |     3     |
| Toy Story  |     4     |

3. ### Comprobación:
   Cada tabla debe tener su llave primaria (PK)

## Segunda FormaNormal **(2FN)** / _Divide y vencerás_

1. ### Comprobar la 1FN
2. ### Todos los atributos de una tabla deben tener la misma llave primaria (PK)

#### tbl_peliculas

|   Título   | Formato |      Directores      | Nacionalidades directores | Precio | Duración | Productora ID |
| :--------: | :-----: | :------------------: | :-----------------------: | :----: | :------: | :-----------: |
| El padrino |   HD    | Francis Ford Coppola |         Americano         |   30   |   175    |       1       |
| El padrino |   3D    | Francis Ford Coppola |         Americano         |   60   |   175    |       1       |
| Toy Story  |   HD    |    John Lasseter     |         Americano         |   30   |    81    |       2       |
| Toy Story  |   3D    |    John Lasseter     |         Americano         |   60   |    81    |       2       |

Tenemos una PK compuesta (significa que está compuesta por varios atributos/columnas)

#### Tabla de PK compuesta

|   Título   | Formato |
| :--------: | :-----: |
| El padrino |   HD    |
| El padrino |   3D    |
| Toy Story  |   HD    |
| Toy Story  |   3D    |

En nuestra **tbl_películas**, el atributo de **Precio** depende de nuestra PK compuesta _(Título y Formato)_, pero todos los demás, únicamente dependen de **Título**. Estamos fallando en nuestro paso número dos de la 2FN. <br>

### ¿Cómo lo solucionamos?

Consiste en sacar las columnas que están en conflicto, para que todos los atributos puedan depender de una única PK.

#### tbl_peliculas

|   Título   |      Directores      | Nacionalidades de directores | Duración | Puntuación | Productora ID |
| :--------: | :------------------: | :--------------------------: | :------: | :--------: | :-----------: |
| El padrino | Francis Ford Coppola |          Americano           |   175    |     A      |       1       |
| Toy Story  |    John Lasseter     |          Americano           |    81    |     B      |       2       |

#### tbl_precios

|   Título   | Formato | Precio |
| :--------: | :-----: | :----: |
| El padrino |   HD    |   30   |
| El padrino |   3D    |   60   |
| Toy Story  |   HD    |   30   |
| Toy Story  |   3D    |   60   |

Ahora tenemos dos tablas _(tbl_peliculas y tbl_precios)_, donde la primera tiene como PK al atributo **Título**, y la segunda tiene como PK compuesta a los atributos **Título y Formato**, así cumpliendo con nuestro paso número dos de la 2FN.
