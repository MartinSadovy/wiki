# Steps to setup Compose app

Compose project

before:
update dependencies

### DI (Hilt) + viewModel + navigation 

./build.gradle:
```
	id 'com.google.dagger.hilt.android' version '2.43.2' apply false
```


app/build.gradle
```
plugins { 
	id 'kotlin-kapt'  
	id 'dagger.hilt.android.plugin'
}
```


```
dependencies {
	implementation 'androidx.lifecycle:lifecycle-viewmodel-compose:2.5.1'  
	  
	implementation "androidx.navigation:navigation-compose:$nav_version"  
	  
	implementation 'com.google.dagger:hilt-android:2.43.2'  
	kapt 'com.google.dagger:hilt-compiler:2.43.2'  
	implementation 'androidx.hilt:hilt-navigation-compose:1.0.0'
```

App.kt
```
@HiltAndroidApp  
class App: Application()
```

manifest:
```
<application android:name=".App" ...
```

viewModel:
```
  
@HiltViewModel  
class WelcomeViewModel @Inject constructor(): ViewModel() {  
  
    var state by mutableStateOf(State(0))  
        private set  
  
	data class State(  
		val value: Int,  
	)  

    fun increase() {  
        state = state.copy(  
            value = state.value + 1  
        )  
    }  
}
```

Activity:
```
@AndroidEntryPoint  
class MainActivity : ComponentActivity() {
```

```
val navController = rememberNavController()  
NavHost(  
	navController = navController,  
	startDestination = "/",  
) {  
	composable("/") {  
		WelcomeScreen(  
			viewModel = hiltViewModel<WelcomeViewModel>(it)  
		) {  
			navController.navigate(
				"/",  
				NavOptions.Builder().setPopUpTo("/", inclusive = true).build()  
			)
		}  
	}
}
```

- TODO:
	- [ ] proguard
	- [ ] paparazzi - UI tests for compose