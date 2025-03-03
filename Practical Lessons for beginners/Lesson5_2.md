## Introduction

These are the learning materials for the **fifth practical video** of the **ThingsBoard CE course**.
During this lesson, you will learn how to:
- Add widgets for energy and water consumption monitoring
- Visualize real-time and historical data

## Customize Office plan widget

The tooltip function:

```
let tooltip = '<h1 style="margin: 8px 0; width: 200px; border-bottom: 1px solid #0000000d; padding-bottom: 8px; padding-right: 15px; font-size: 16px; font-weight: 600; line-height: 24px; top: 15px;">${entityLabel}</h1>';
let typeTooltip = '';
if (data.deviceType == 'energy-sensor') {
  typeTooltip = '<div style="display: flex; flex-direction: row; justify-content: space-between;align-items: center; gap: 10px;">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">Power consumption: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${powerConsumption:1} kW</span>' +
          '</div>';
  typeTooltip += '<div style="margin-top: 17px; text-align: center; background: var(--tb-primary-50, #87CEEB); border-radius: 6px;"><link-act name="sensor_details">Details ></link-act></div>';
} else if (data.deviceType == 'air-sensor') {
  typeTooltip = '<div style="display: flex; flex-direction: column">' +
          '<div style="display: flex; flex-direction: row; justify-content: space-between; align-items: center; gap: 10px">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">Temperature: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${temperature:0} °C</span>' +
          '</div>' +
          '<div style="display: flex; flex-direction: row; justify-content: space-between; align-items: center; gap: 10px">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">Humidity: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${humidity:0} %</span>' +
          '</div>' +
          '<div style="display: flex; flex-direction: row; justify-content: space-between; align-items: center; gap 10px;">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">CO2: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${co2:0} ppm</span>' +
          '</div>' +
          '</div>';
  typeTooltip += '<div style="margin-top: 17px; text-align: center; background: var(--tb-primary-50, #87CEEB); border-radius: 6px;"><link-act name="sensor_details">Details ></link-act></div>';
} else if (data.deviceType == 'water-sensor') {
  typeTooltip = '<div style="display: flex; flex-direction: column">' +
          '<div style="font-weight: 600; display: flex; flex-direction: row; justify-content: space-between; align-items: center; gap: 10px">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">Water consumption: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${waterConsumption:1} gal</span>' +
          '</div>' +
          '<div style="font-weight: 600; display: flex; flex-direction: row; justify-content: space-between; align-items: center; gap: 10px">' +
          '<span style="font-weight: 600; font-size: 12px; line-height: 16px; color: #0000008a; max-width: 90px;">Battery Level: </span>' +
          '<span style="font-weight: 600; font-size: 13px; line-height: 20px; color: #000000de">${batteryLevel:0} %</span>' +
          '</div>';
  '</div>';
  typeTooltip += '<div style="margin-top: 17px; text-align: center; background: var(--tb-primary-50, #87CEEB); border-radius: 6px;"><link-act name="sensor_details">Details ></link-act></div>';
}
return tooltip + typeTooltip;
```

<br>
CSS style for the Office plan widget:

```
.leaflet-tooltip-pane .leaflet-tooltip-top{
    opacity: 1 !important;
}
.leaflet-popup-content {
    width: auto !important;
    margin: 8px;
}
a.leaflet-popup-close-button {
    font-size: 20px;
    color: black;
    border-radius: 2px;  
    top: 8px;
    right: 5px;
}
```

<br>
Custom action function:

```
const $injector = widgetContext.$injector;
const deviceService = $injector.get(widgetContext.servicesMap.get('deviceService'));

deviceService.getDevice(entityId.id).subscribe(device => {
    if (device.type === 'air-sensor') {
        openDashboardState('air_sensor');
    } else if (device.type === 'water-sensor') {
        openDashboardState('water_sensor');
    } else {
        openDashboardState('energy_sensor');
    }
});

function openDashboardState(stateId) {
    const params = {
        entityId: entityId,
        entityName: entityName
    };
    widgetContext.stateController.openState(stateId, params, false);
}
```
