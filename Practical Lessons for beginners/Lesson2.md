# Introduction

These are the learning materials for the **second practical video** of the **ThingsBoard CE course**. 
During this lesson, you will learn how to:
- Add your first **devices** and **configure relations** between entities.
- Visualize devices on the **Entities table** widget.
- Configure **device telemetry emulators** in the **Rule chain**.
- Display the **latest telemetry data** of your devices in the widget. 

# Adding devices

To bulk provision devices:
- Go to **Devices**, select the **`+`** icon > **Import device**.
- Attach your CSV file, select the delimiter, and map the data between the columns of the uploaded file and the data types on the platform.
  
Here's the [CSV file](resources/devices.csv) we use in this tutorial. 

# Configuring generator nodes

Paste the corresponding code into the generator function for each sensor:

- **Indoor air quality data emulator**
  
    ```
    var temperature = toFixed(Math.random()*10 + 20, 2);
    var humidity = toFixed(Math.random()*15 + 30, 2);
    var co2 = toFixed(Math.random()*70 + 440, 2);
    var msg = { temperature: temperature, humidity: humidity, co2: co2 };
    var metadata = { data: 40 };
    var msgType = "POST_TELEMETRY_REQUEST";
    
    return { msg: msg, metadata: metadata, msgType: msgType };
    ```
- **Power consumption data emulator**
  
    ```
    var powerConsumption = toFixed(Math.random() * 4.3, 2);
    var msg = { powerConsumption: powerConsumption};
    var metadata = { data: 40 };
    var msgType = "POST_TELEMETRY_REQUEST";

    return { msg: msg, metadata: metadata, msgType: msgType };
    ```
- **Water consumption data emulator**
  
    ```
    var waterConsumption = toFixed(Math.random()*0.6 + 2, 2);
    var batteryLevel = toFixed(Math.random()*1 + 45, 2);
    var msg = { waterConsumption: waterConsumption, batteryLevel: batteryLevel };
    var metadata = { data: 40 };
    var msgType = "POST_TELEMETRY_REQUEST";

    return { msg: msg, metadata: metadata, msgType: msgType };
    ```

# Adding cell content function

To combine multiple telemetry values into single column:

- Select the **gear** icon next to the **Telemetry value** row.
- Turn on the **Use cell content function** option.
- Insert the function into the corresponding field:

    ```
    if (entity.temperature && entity.humidity && entity.co2){
        return '<div style="display:flex;flex-direction:row;flex-wrap:wrap;gap:7px;margin:10px 0;align-items:center">' +  
            '<div style="padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;background:#e0e0e0;border-radius:20px;">Temp: ' + entity.temperature.toFixed(0) + ' °C</div>' + 
            '<div style="padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;background:#e0e0e0;border-radius:20px">Hum: ' + entity.humidity.toFixed(0) + ' %</div>' + 
            '<div style="padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;background:#e0e0e0;border-radius:20px">CO2: ' + entity.co2.toFixed(0) + ' ppm</div>'
        + '</div>';
    }
    else if (entity.powerConsumption){
        return '<div style="display: inline-block;padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;background:#d3d3d3;border-radius:20px">' + entity.powerConsumption.toFixed(2) + ' kWh per hour</div>';
    }
    else if (entity.waterConsumption){
        return '<div style="display: inline-block;padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;background:#d3d3d3;border-radius:20px">' + entity.waterConsumption.toFixed(2) + ' gal per hour</div>';
    }
    return value;
    ```
- Save the changes.
