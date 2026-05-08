import streamlit as st
import requests

st.set_page_config(page_title='Weather App-Kumar',layout='wide')

st.title('🌦 Live Weather App - Kumar')

api_key = '040c8bba4e7c43b180e114138260605'

base_url = 'http://api.weatherapi.com/v1/current.json'

st.sidebar.header('Settings')

unit = st.sidebar.selectbox("Temperature Unit:", ['Celcius','Fahrenheit'])

days = st.sidebar.slider('Forecast days', 1, 7, 3)

show_humidity = st.sidebar.checkbox("Show Humidity", value=True)

show_wind = st.sidebar.checkbox("Show Wind Speed", value=True)
city = st.text_input("Enter City Name:")

if st.button("Get Weather") and city:

    url = f'{base_url}/forecast.json?key={api_key}&q={city}&days={days}&aqi=no'

    r = requests.get(url)
    if r.status_code == 200:

        data = r.json()
        loc = data["location"]["name"]
        country = data["location"]["country"]
        temp = data["current"]["temp_c"]
        cond = data["current"]["condition"]["text"]
        icon = "https:"+ data["current"]["condition"]["icon"]
        humidity = data["current"]["humidity"]
        wind = data["current"]["wind_kph"]

        if unit == "Celcius":
            temp = data["current"]["temp_c"]
        else :
            temp = data["current"]["temp_f"]


        st.subheader(f'{loc},{country}')
        st.image(icon,width=80)

        col1, col2 = st.columns(2)

        with col1:
            st.write(f' Temperature: {temp} {unit[0]}')

        with col2:
            st.write(f'☁ Condition: {cond}')

        if show_humidity:
            st.write(f"💧Humidity: {humidity}%")
        if show_wind:
            st.write(f"🌬Wind Speed: {wind}kph")

        st.markdown("---")

        st.header(f"{days}-Days Forecast")

        forecast_day = data['forecast']['forecastday']

        for day in forecast_day:
            date = day["date"]
            if unit == "Celcius":
                min_temp = day["day"]["mintemp_c"]
                max_temp = day["day"]["maxtemp_c"]
            else:
                min_temp = day["day"]["mintemp_f"]
                max_temp = day["day"]["maxtemp_f"]

            condition = day["day"]["condition"]["text"]
            icon_url = "https:" + day["day"]["condition"]["icon"]

            col1, col2, col3, col4 = st.columns([2, 2, 2, 2])
            with col1:
                st.write(f'{date}')
            with col2:
                st.image(icon_url, width=50)
            with col3:
                st.write(f'🌡Min: {min_temp}{unit[0]}')
            with col4:
                st.write(f'🌡Max: {max_temp}{unit[0]}')

            st.write(f"{condition}")
            st.markdown("---")








