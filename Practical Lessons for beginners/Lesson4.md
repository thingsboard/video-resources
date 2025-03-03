# Introduction
These are the learning materials for the **fourth practical video** of the **CE educational course**. During this lesson, you'll learn how to:
- Add **images** and **device coordinates** as attributes. 
- Visualize **devices location** on the **Office plan image widget**.
- Set **custom icons** as **image markers**. 
- Customize the **widget appearence** with **code**.

# Adding office plan image
To add the image, go to the **Resources** tab and select **Upload image**. You can use the [image from this tutorial](resources/office-a-plan.png) or your own.

# Adding devices coordinates

Use the corresponding **server attributes** values for each sensor:

- **Energy Meter**
  
	| Key           | Value type     | Value                 |
	| :----------   | :---------     | :---------------------|
	| `xPos`        | Double         | 0.14                  |
	| `yPos`        | Double         | 0.95                  |

- **Indoor Air Quality Sensor**
  
	| Key            | Value type     | Value                |
	| :----------    | :---------     | :--------------------| 
	| `xPos`         | Double         | 0.51                 |
	| `yPos`         | Double         | 0.68                 |

- **Water Flow Meter**
  
	| Key            | Value type     | Value                |
	| :----------    | :---------     | :--------------------| 
	| `xPos`         | Double         | 0.14                 |
	| `yPos`         | Double         | 0.32                 |


# Customizing device label

To customize the label, go to the **Appearence** tab and scroll to the **Lable** section. In the corresponding field, paste the following code:

```
<div style='position: relative; white-space: nowrap; text-align: center; font-size: 14px; top: 2px;'><span style='margin-left: -500%;'></span><div style='border: 2px solid #00695c; border-radius: 10px; color: #000; background-color: #fff;  padding-left: 12px; padding-right: 12px; padding-top: 4px; padding-bottom: 4px;'>${entityLabel}</div></div>

```

# Adding image marker

To set custom icons as markers,  remove the default ones in the **Marker image** section. Then, paste the following code in the the corresponding field:

```
var type = dsData[dsIndex]['Type'];
if (type == 'air-sensor') {
	var res = {
	    url: images[0],
	    size: 50
	}
	return res;
} else if (type == 'energy-sensor') {
    var res = {
	    url: images[1],
	    size: 50
	}
	return res;
} else if (type == 'water-sensor') {
    var res = {
	    url: images[2],
	    size: 50
	}
	return res;
}
```

After this step, select **Browse from gallery** and upload the corresponding icons as new image markers:
- [Air sensor](resources/air-sensor.svg)
- [Energy sensor](resources/energy-sensor.svg)
- [Water sensor](resources/water-sensor.svg)

# Customizing widget appearence 

To make widget labels opaque, go to the **Widget card** > **Widget CSS** and paste the following code:

```
.leaflet-tooltip-pane .leaflet-tooltip-top{
    opacity: 1 !important;
}
```
