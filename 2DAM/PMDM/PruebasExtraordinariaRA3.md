Perfecto, aquí tienes un ejemplo completo de una pequeña app Android que:

Muestra la cámara en pantalla con CameraX

Graba un video

Guarda la ruta del archivo en una base de datos Room

Muestra una lista de videos usando un ViewModel + LiveData

Reproduce el video con MediaPlayer



---

📁 Estructura general del proyecto

com.example.videorecorder
│
├── data/
│   ├── Video.kt               → @Entity
│   ├── VideoDao.kt            → @Dao
│   └── AppDatabase.kt         → Room database
│
├── ui/
│   ├── MainActivity.kt        → UI principal con CameraX y botones
│   └── VideoViewModel.kt      → ViewModel
│
└── utils/
    └── VideoPlayer.kt         → Función para reproducir video


---

1. 📦 Room

📄 Video.kt

@Entity
data class Video(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val name: String,
    val filePath: String
)

📄 VideoDao.kt

@Dao
interface VideoDao {
    @Query("SELECT * FROM Video ORDER BY id DESC")
    fun getAllVideos(): LiveData<List<Video>>

    @Insert
    suspend fun insert(video: Video)
}

📄 AppDatabase.kt

@Database(entities = [Video::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun videoDao(): VideoDao

    companion object {
        private var INSTANCE: AppDatabase? = null

        fun getInstance(context: Context): AppDatabase {
            return INSTANCE ?: synchronized(this) {
                Room.databaseBuilder(context, AppDatabase::class.java, "video-db")
                    .build().also { INSTANCE = it }
            }
        }
    }
}


---

2. 🧠 ViewModel

📄 VideoViewModel.kt

class VideoViewModel(application: Application) : AndroidViewModel(application) {
    private val videoDao = AppDatabase.getInstance(application).videoDao()
    val videos: LiveData<List<Video>> = videoDao.getAllVideos()

    fun saveVideo(video: Video) {
        viewModelScope.launch {
            videoDao.insert(video)
        }
    }
}


---

3. 📷 MainActivity con CameraX

📄 MainActivity.kt

@AndroidEntryPoint
class MainActivity : AppCompatActivity() {

    private lateinit var videoCapture: VideoCapture<Recorder>
    private lateinit var previewView: PreviewView
    private val viewModel: VideoViewModel by viewModels()
    private lateinit var outputDirectory: File

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        previewView = findViewById(R.id.previewView)
        outputDirectory = getOutputDirectory()

        startCamera()

        findViewById<Button>(R.id.btnRecord).setOnClickListener {
            startRecording()
        }

        viewModel.videos.observe(this) { videos ->
            // mostrar en lista (por ejemplo RecyclerView)
        }
    }

    private fun startCamera() {
        val cameraProviderFuture = ProcessCameraProvider.getInstance(this)
        cameraProviderFuture.addListener({
            val cameraProvider = cameraProviderFuture.get()

            val preview = Preview.Builder().build().also {
                it.setSurfaceProvider(previewView.surfaceProvider)
            }

            val recorder = Recorder.Builder()
                .setQualitySelector(QualitySelector.from(Quality.HIGHEST))
                .build()

            videoCapture = VideoCapture.withOutput(recorder)

            val cameraSelector = CameraSelector.DEFAULT_BACK_CAMERA

            cameraProvider.unbindAll()
            cameraProvider.bindToLifecycle(
                this, cameraSelector, preview, videoCapture
            )
        }, ContextCompat.getMainExecutor(this))
    }

    private fun startRecording() {
        val name = "video_${System.currentTimeMillis()}.mp4"
        val file = File(outputDirectory, name)

        val outputOptions = FileOutputOptions.Builder(file).build()
        val recording = videoCapture.output
            .prepareRecording(this, outputOptions)
            .withAudioEnabled()
            .start(ContextCompat.getMainExecutor(this)) { recordEvent ->
                if (recordEvent is VideoRecordEvent.Finalize) {
                    viewModel.saveVideo(Video(name = name, filePath = file.absolutePath))
                    Toast.makeText(this, "Video guardado", Toast.LENGTH_SHORT).show()
                }
            }
    }

    private fun getOutputDirectory(): File {
        val mediaDir = externalMediaDirs.firstOrNull()?.let {
            File(it, "videos").apply { mkdirs() }
        }
        return mediaDir ?: filesDir
    }
}


---

4. 🎵 Reproducción de video

📄 VideoPlayer.kt

fun playVideo(context: Context, filePath: String) {
    val mediaPlayer = MediaPlayer().apply {
        setDataSource(context, Uri.parse(filePath))
        setOnPreparedListener { start() }
        prepareAsync()
    }
}


---

5. 🖼 Layout básico (activity_main.xml)

<androidx.camera.view.PreviewView
    android:id="@+id/previewView"
    android:layout_width="match_parent"
    android:layout_height="300dp"
    android:layout_margin="16dp" />

<Button
    android:id="@+id/btnRecord"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Grabar Video"
    android:layout_margin="16dp"/>


---

6. 🧷 Dependencias necesarias (Gradle)

// build.gradle (nivel módulo)
dependencies {
    implementation("androidx.camera:camera-camera2:1.3.0")
    implementation("androidx.camera:camera-lifecycle:1.3.0")
    implementation("androidx.camera:camera-video:1.3.0")
    implementation("androidx.camera:camera-view:1.3.0")

    implementation("androidx.room:room-runtime:2.6.1")
    kapt("androidx.room:room-compiler:2.6.1")

    implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0")
    implementation("androidx.lifecycle:lifecycle-livedata-ktx:2.7.0")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
}


---

¿Quieres que te prepare este ejemplo como un proyecto completo en ZIP para que lo abras en Android Studio directamente?

