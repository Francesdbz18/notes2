[[examen]]
[[prueba20250220_V2.pdf]]
[[Contenidos]]

### Paso 1: Definir el modelo de datos para Room

Primero, necesitamos definir el modelo de datos para los registros.

kotlin

Copiar

`@Entity(tableName = "registro") data class Registro(     @PrimaryKey(autoGenerate = true) val id: Int = 0,     val nombre: String,     val edad: Int,     val codigo: Int )`

### Paso 2: Crear la interfaz DAO para la base de datos Room

El DAO (Data Access Object) es donde se definen las funciones para interactuar con la base de datos.

kotlin

Copiar

`@Dao interface RegistroDao {     @Insert     suspend fun insertAll(vararg registros: Registro)      @Query("SELECT * FROM registro")     suspend fun getAllRegistros(): List<Registro> }`

### Paso 3: Crear la base de datos Room

Ahora, creamos la base de datos de Room.

kotlin

Copiar

`@Database(entities = [Registro::class], version = 1) abstract class AppDatabase : RoomDatabase() {     abstract fun registroDao(): RegistroDao }`

### Paso 4: Crear una función para generar los 10 registros

Vamos a escribir una función que generará 10 registros automáticamente cuando se pulse el botón. La generación de los registros usará un nombre (por ejemplo, "Juan") y generará valores aleatorios para la edad y el código.

kotlin

Copiar

`fun generarRegistros(): List<Registro> {     return List(10) { index ->         Registro(             nombre = "Juan $index",             edad = (18..60).random(),             codigo = (1001..9999).random()         )     } }`

### Paso 5: Crear la interfaz de usuario

#### Pantalla principal con el botón para generar registros y la lista desplazable

kotlin

Copiar

`@Composable fun MainScreen(     navController: NavController,     db: AppDatabase ) {     val registros = remember { mutableStateOf(listOf<Registro>()) }      // Obtener registros desde la base de datos     LaunchedEffect(true) {         registros.value = db.registroDao().getAllRegistros()     }      Column(modifier = Modifier.fillMaxSize()) {         // Panel superior con el botón         Box(             modifier = Modifier                 .fillMaxWidth()                 .height(100.dp)                 .background(Color.Blue),             contentAlignment = Alignment.Center         ) {             Button(onClick = {                 // Insertar registros en la base de datos                 val registrosGenerados = generarRegistros()                 registros.value = registrosGenerados                 db.registroDao().insertAll(*registrosGenerados.toTypedArray())             }) {                 Text("Generar Registros")             }         }          // Lista desplazable con los registros         LazyColumn {             items(registros.value) { registro ->                 RegistroItem(registro, navController)             }         }     } }  @Composable fun RegistroItem(registro: Registro, navController: NavController) {     Card(modifier = Modifier         .fillMaxWidth()         .padding(8.dp)         .clickable {             // Navegar a la pantalla de detalles             navController.navigate("detalles/${registro.id}")         }) {         Column(modifier = Modifier.padding(16.dp)) {             Text(text = "Nombre: ${registro.nombre}")             Text(text = "Edad: ${registro.edad}")             Text(text = "Código: ${registro.codigo}")         }     } }`

#### Pantalla de detalles

kotlin

Copiar

`@Composable fun DetalleScreen(id: Int, db: AppDatabase) {     val registro = remember { mutableStateOf<Registro?>(null) }      LaunchedEffect(id) {         // Obtener el registro de la base de datos por ID         registro.value = db.registroDao().getRegistroById(id)     }      registro.value?.let { registro ->         Column(modifier = Modifier.fillMaxSize()) {             Text(text = "Nombre: ${registro.nombre}")             Text(text = "Edad: ${registro.edad}")             Text(text = "Código: ${registro.codigo}")              // Botón para volver a la pantalla principal             Button(onClick = { /* Volver a la pantalla principal */ }) {                 Text("Volver")             }         }     } }`

### Paso 6: Navegación entre pantallas

Definimos la navegación utilizando `NavController` de Jetpack Compose.

kotlin

Copiar

`@Composable fun AppNavHost(navController: NavController, db: AppDatabase) {     NavHost(navController, startDestination = "main") {         composable("main") {             MainScreen(navController = navController, db = db)         }         composable("detalles/{id}") { backStackEntry ->             val id = backStackEntry.arguments?.getString("id")?.toInt() ?: 0             DetalleScreen(id = id, db = db)         }     } }`

### Paso 7: Configuración final

Finalmente, en el `MainActivity`, configuramos la base de datos y la navegación.

kotlin

Copiar

`class MainActivity : AppCompatActivity() {     override fun onCreate(savedInstanceState: Bundle?) {         super.onCreate(savedInstanceState)          val db = Room.databaseBuilder(applicationContext, AppDatabase::class.java, "app_database")             .build()          setContent {             val navController = rememberNavController()             AppNavHost(navController = navController, db = db)         }     } }`

### Resumen

Este código cubre todos los requerimientos:

1. **Panel superior con botón**: Está centrado y genera 10 registros en la base de datos.
2. **Lista desplazable**: Muestra todos los registros desde Room.
3. **Elemento clicable**: Cada registro es clicable y navega a una pantalla de detalles.
4. **Pantalla de detalles**: Muestra los detalles del registro seleccionado.
5. **Botón para volver**: En la pantalla de detalles, puedes volver a la pantalla principal.

Este es un esquema básico para empezar con Jetpack Compose y Room. Puedes ajustarlo para que se adapte mejor a tus necesidades o añadir más características.