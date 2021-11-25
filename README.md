# Measurement-of-air-pollution
#Measurement of air pollution by using live api .To find the measurement of air pollution at any  cities  and also find the components of air pollution present 
import json
import tkinter as tk
import requests 
import time
 

def getapi(canvas):
    city = textField.get()
    apicity = "https://api.openweathermap.org/data/2.5/weather?q="+city+"&appid=06c921750b9a82d8f5d1294e1586276f"
    
    json_dataCity = requests.get(apicity).json()
    getlong=json_dataCity['coord']['lon']
    getlat=json_dataCity['coord']['lat']
    apiaqi="https://api.openweathermap.org/data/2.5/air_pollution?lat="+str(getlat)+"&lon="+str(getlong)+"&appid=f933656ce83dd109793ccd42921b2e92"
    json_data = requests.get(apiaqi).json()
    condition = json_data['list'][0]['components']
    co = condition['co'] 
    no = condition['no'] 
    no2 = condition['no2'] 
    o3 = condition['o3'] 
    so2 = condition['so2'] 
    pm2_5 = condition['pm2_5'] 
    pm10 = condition['pm10'] 
    nh3 = condition['nh3']
    # cloud_info="test"
    if pm2_5>=0 and pm2_5<=50:
        cloud_info="Good"
    elif pm2_5>=51 and pm2_5<=101:
        cloud_info="Moderate"
    elif pm2_5>=101 and pm2_5<=150:
        cloud_info="cloud is unhealthy for sensitive groups"
    elif pm2_5>=151 and pm2_5<=200:
        cloud_info="cloud is unhealthy"
    elif pm2_5>=201 and pm2_5<=300:
        cloud_info="cloud is Very unhealthy"
    elif pm2_5>=301 and pm2_5<=800:
        cloud_info="cloud is Hazardous"
        
    
    cityName="\n" 
    final_info = "City Name: " + city + "" + "\n" 
    final_data = "\n"+ "Co: " + str(co) + "" + "\n" + "no: " + str(no) + "" +"\n" + "no2: " + str(no2) + "\n" +"o3: " + str(o3) + "\n" +"So2: " + str(so2) + "\n" + "pm2_5: " + str(pm2_5) + "\n" + "pm10: " + str(pm10) + "\n" + "nh3: " + str(nh3)
    label1.config(text = final_info)
    label2.config(text = cloud_info)
    label3.config(text = final_data)
    
canvas = tk.Tk()
canvas.geometry("600x500")
canvas.title("AQI App")
f = ("poppins", 15, "bold")
t = ("poppins", 25, "bold")
label4 = tk.Label(canvas, text="Enter City Name:")
label4.pack(pady = 20)
textField = tk.Entry(canvas, justify='center', width = 20, font = t)
textField.pack(pady = 20)
textField.focus()
textField.bind('<Return>', getapi)

label1 = tk.Label(canvas, font=t)
label1.pack()
label2 = tk.Label(canvas, font=f)
label2.pack()
label3 = tk.Label(canvas, font=f)
label3.pack()
canvas.mainloop()
