# Random Image using c++/sfml

## idea of works
The app works as shown in figure below, We can divied the app into two main parts are backend and frontend.

-   The backend is Public API from Weatherbit it gives a forcast of status weather for 7 days as a JSON struct.
-   The frontend built by Flutter, it's work by requesteing for public API (Weatherbit ), after that will display it.
 <img width=600 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/flow.png"/>
<hr>

    

## The Frontend

As mentioned before, we used Flutter framework for frontend, for information about this framework and go to this link

We used the provider as state management of app

    class  WeatherViewModel extends  ChangeNotifier {
    Future<void> getCity() async {....}
    void saveCity() async {...}
    void fetchWeatherData() async {
    ...
    try {
    var url = Uri.parse('https://api.weatherbit.io/.....');
    response = await http.get(url,);
    var json = jsonDecode(response.body);
    curDay = WeatherAPI.fromJson(json);
    ...
    }
    ...
    notifyListeners();}}
This code above is model for featch data from the server. Also it's extend from ChangeNotifier, this class will be notify any widget subscribe to any function in this class, if any change happen in theses funcations and will reload state of widget. For example, if i call fetchWeatherData() function then all widgets that subscribe to this function will be reloaded

    body: RefreshIndicator(
    key: refreshKey,
    onRefresh: () async {
    context.read<WeatherViewModel>().fetchWeatherData();
    },
    child:[....] 
    )`
So any widgets in child will be reloaded.

## Flow of work
1-first run<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/5.png"/>
<hr>
2-first fetch data from server<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/7.png"/>
<hr>
3-loaded data and display it<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/1.png"/>
<hr>
4-change city<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/3.png"/>
<hr>
5-reloading only widgets subscribe to our model<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/7.png"/>
<hr>
5-if not there nay connection to internet<br>
 <img width=200 src="https://github.com/MohammadTeeU/weather-app/blob/main/screenshots/6.png"/>
<hr>
