2do Parcial - Parte Practica
Que se solicita:

El codigo tiene 10 errores. Recae en usted analizar que es un error dentro del codigo.
Los Alumnos tendran que forkear este repo como propio, hacer un issue desde Github con Comentarios refiriendo en que linea esta el error, y como se debe solucionar.
La respuesta sera con el link a ese Fork, y adentro deben estar los issues. Los profesores tenemos que poder ingresar al mismo. Recae en los alumnos asegurarse de que los profesores puedan ingresar.
Tambien pueden editar el Archivo Readme y poner los resultados dentro de sus propios forks.
https://github.com/ExBattou/SimpsonsApp

Errores del repositorio SimpsonsApp
1- Error en configuración del JDK(no compila): En el archivo gradle.properties se define org.gradle.java.home con una ruta local. Esto esta mal porque esa ruta solo existe en una computadora específica. Si otra persona clona el proyecto o lo abre desde otra PC, Gradle no va a encontrar ese JDK y la compilación puede fallar. Lo correcto sería no dejar esa ruta fija en el proyecto y configurar el JDK desde Android Studio o en la configuracion local de cada usuario.

2- Error en Episode.kt: En el archivo Episode.kt hay un init con un return Episode que no corresponde que este, ese codigo esta fuera de lugar. El archivo deberia quedar solo como una data class con los datos del episodio.

3- Falta importar SimpsonsApi: En EpisodeRepositoryImpl se usa SimpsonsApi, pero no esta importado. Hay que agregar el import correspondiente para que el repository pueda usar la API.La solucion seria importar com.example.simpsonsapp.data.remote.SimpsonsApi.

4- Error en Retrofit: En DataModule se crea Retrofit sin poner una baseUrl. Esto esta mal porque Retrofit necesita una URL base para poder hacer las llamadas a la API. La solucion seria agregar la baseUrl en el builder de Retrofit.

5- SimpsonsApi está mal ubicado: La interfaz SimpsonsApi esta declarada dentro del archivo EpisodeRemoteMediator.kt. No deberaa estar ahi, porque son responsabilidades distintas. Lo mejor seria moverla a un archivo propio llamado SimpsonsApi.kt.

6- Error de recomposicion en MainScreen: En MainScreen se llama a viewModel.refreshSeasons() directamente dentro del composable. Esto esta mal porque Compose puede recomponer varias veces y esa funcion podria ejecutarse mas de una vez sin control. Deberia hacerse con LaunchedEffect.

7- Uso de collectAsState(): En MainScreen y DetailScreen se usa collectAsState() para observar estados del ViewModel. Seria mejor usar collectAsStateWithLifecycle() para respetar mejor el ciclo de vida de la pantalla.

8- Las temporadas no se actualizan solas: availableSeasons se carga una vez desde el ViewModel, pero no queda observando cambios de Room. Si despues se cargan nuevos episodios en la base local, las temporadas no se actualizan automaticamente. Lo mejor seria que Room devuelva un Flow con las temporadas y que el ViewModel lo observe.

9- Uso peligroso de episode!!: En DetailScreen se usa episode!! para forzar que el episodio no sea nulo. Esto puede ser peligroso y no es una buena practica. Lo mejor seria usar episode?.let.

10- Falta manejo de errores de red: En MainScreen se muestra el loading, pero no se maneja bien el caso de error cuando falla la API o no hay conexion. Deberia mostrarse un mensaje de error y alguna opcion para reintentar. Se podria manejar con LoadState.Error y un boton para reintentar.
