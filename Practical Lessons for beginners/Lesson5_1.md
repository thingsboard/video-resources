# Introduction

These are the learning materials for the **fifth practical video** of the **ThingsBoard CE course**.
During this lesson, you will learn how to:
- Create separate **states** for each device
- Configure **actions** to navigate between states
- Add widgets for temperature, humidity, and CO₂ monitoring
- Visualize real-time and historical data

# Adding states

To add a new state, enter the dashboard edit mode, select the "Manage dashboard states" menu option, and then select the "plus" icon. Then enter the state name and state Id:

| Name                      | State ID      |
| :----------               | :---------    |
| Indoor Air Quality Sensor | air_sensor    |
| Energy Meter              | energy_sensor |
| Indoor Air Quality Sensor | water_sensor  |

## Customize Office sensors list widget

Custom action function:

```
const $injector = widgetContext.$injector;
const deviceService = $injector.get(widgetContext.servicesMap.get('deviceService'));

deviceService.getDevice(entityId.id).subscribe(device => {
    if (device.type === 'energy-sensor') {
        openDashboardState('energy_sensor');
    } else if (device.type === 'water-sensor') {
        openDashboardState('water_sensor');
    } else {
        openDashboardState('air_sensor');
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
