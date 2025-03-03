# Adding asset

To add a new asset, go to the **Entities** section > **Assets**, and then select the **`+`** icon > **Add new asset**. Then enter the asset name and create the corresponding asset profile.

| Name          | Asset profile  |
| :----------   | :---------     |
| `Office B`    | office         |

# Adding attributes

To add a new attribute, select the Office B, go to the **Attributes** tab, and select the **`+`** icon. Enter the correspoding key, select the value type, and enter the value itself:

| Key            | Value type     | Value                       |
| :----------    | :---------     | :---------------------------| 
| `address`      | String         | 641 Lexington Ave, New York |
| `floor`        | Integer        | 4                           |
| `email`        | String         | office.b@mail.test          |
| `phone`        | String         | +1 121 666 5522             |
| `officeManager`| String         | Millie Brown                |

# Adding devices

To bulk provision devices:
- Go to **Devices**, select the **`+`** icon > **Import device**.
- Attach your CSV file, select the delimiter, and map the data between the columns of the uploaded file and the data types on the platform.
  
Here's the [CSV file](resources/devices_b.csv) we use in this tutorial. 

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
