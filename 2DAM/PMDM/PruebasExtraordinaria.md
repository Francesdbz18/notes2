Dado que es una calculadora básica, la segunda pantalla probablemente mostrará el resultado de la operación. Aquí te explico cómo lo implementarías utilizando la navegación de Compose, centrándonos en el enfoque de paso de argumentos en la ruta (URL-like), que es más directo para un solo valor simple como el resultado. Luego, veremos cómo la navegación tipo-segura también se aplicaría.
Escenario:
 * Primera Pantalla (CalculatorScreen): El usuario introduce números, realiza una operación (suma, resta, etc.) y, al presionar un botón "Calcular" o similar, el resultado se pasa a la segunda pantalla.
 * Segunda Pantalla (ResultScreen): Muestra el resultado.
Enfoque 1: Pasar el resultado en la ruta (URL-like)
1. Definir las rutas y el argumento
Primero, define tus rutas en un sealed class o un object para tener un control centralizado de ellas.
// Define tus rutas
sealed class Screen(val route: String) {
    object Calculator : Screen("calculator_screen")
    object Result : Screen("result_screen/{result}") { // 'result' es el nombre del argumento
        fun createRoute(result: Double) = "result_screen/$result"
    }
}

2. Configurar el NavHost en tu MainActivity o Composable principal
import androidx.compose.runtime.Composable
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController
import androidx.navigation.NavType
import androidx.navigation.navArgument

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            CalculatorApp()
        }
    }
}

@Composable
fun CalculatorApp() {
    val navController = rememberNavController()
    NavHost(navController = navController, startDestination = Screen.Calculator.route) {
        composable(Screen.Calculator.route) {
            CalculatorScreen(navController = navController)
        }
        composable(
            route = Screen.Result.route,
            arguments = listOf(navArgument("result") { type = NavType.FloatType }) // Especifica el tipo Double
        ) { backStackEntry ->
            val result = backStackEntry.arguments?.getFloat("result")?.toDouble() ?: 0.0
            ResultScreen(result = result)
        }
    }
}

Explicación:
 * composable(Screen.Result.route, arguments = ...): Aquí le decimos a Compose Navigation que la ruta result_screen/{result} espera un argumento llamado "result".
 * navArgument("result") { type = NavType.FloatType }: Especificamos que el tipo de este argumento es FloatType. Aunque en Kotlin usemos Double, NavType.FloatType es el tipo que mejor se mapea para valores decimales en las rutas de navegación. Luego lo convertiremos a Double al recuperarlo.
 * val result = backStackEntry.arguments?.getFloat("result")?.toDouble() ?: 0.0: Recuperamos el valor como Float, lo convertimos a Double y proporcionamos un valor predeterminado de 0.0 si por alguna razón el argumento no está presente.
3. Pantalla de la Calculadora (CalculatorScreen)
Esta pantalla manejará la lógica de la calculadora y navegará al resultado.
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.unit.dp
import androidx.navigation.NavHostController

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun CalculatorScreen(navController: NavHostController) {
    var num1 by remember { mutableStateOf("") }
    var num2 by remember { mutableStateOf("") }
    var operation by remember { mutableStateOf("+") } // Por simplicidad, asumimos una operación

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        OutlinedTextField(
            value = num1,
            onValueChange = { num1 = it },
            label = { Text("Número 1") },
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(modifier = Modifier.height(8.dp))
        OutlinedTextField(
            value = num2,
            onValueChange = { num2 = it },
            label = { Text("Número 2") },
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(modifier = Modifier.height(16.dp))

        // Botones de operación (ejemplo simple, puedes expandirlo)
        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceAround
        ) {
            Button(onClick = { operation = "+" }) { Text("+") }
            Button(onClick = { operation = "-" }) { Text("-") }
            Button(onClick = { operation = "*" }) { Text("*") }
            Button(onClick = { operation = "/" }) { Text("/") }
        }
        Spacer(modifier = Modifier.height(16.dp))

        Button(
            onClick = {
                val number1 = num1.toDoubleOrNull() ?: 0.0
                val number2 = num2.toDoubleOrNull() ?: 0.0
                val result = when (operation) {
                    "+" -> number1 + number2
                    "-" -> number1 - number2
                    "*" -> number1 * number2
                    "/" -> if (number2 != 0.0) number1 / number2 else Double.NaN // Manejo de división por cero
                    else -> 0.0
                }
                navController.navigate(Screen.Result.createRoute(result)) // Navega con el resultado
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Calcular")
        }
    }
}

Puntos clave:
 * num1.toDoubleOrNull() ?: 0.0: Intenta convertir el texto a Double. Si no es un número válido, usa 0.0.
 * navController.navigate(Screen.Result.createRoute(result)): Esta es la parte crucial. Llamamos a la función createRoute que definimos en Screen.Result para generar la ruta con el resultado insertado, y luego navegamos a esa ruta.
4. Pantalla del Resultado (ResultScreen)
Esta pantalla simplemente recibe el resultado y lo muestra.
import androidx.compose.foundation.layout.*
import androidx.compose.material3.Button
import androidx.compose.material3.Text
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.sp
import androidx.navigation.NavHostController

@Composable
fun ResultScreen(result: Double) {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("El resultado es:", fontSize = 24.sp)
        Spacer(modifier = Modifier.height(16.dp))
        Text(
            text = String.format("%.2f", result), // Formatear a dos decimales
            fontSize = 48.sp,
            fontWeight = FontWeight.Bold
        )
    }
}
