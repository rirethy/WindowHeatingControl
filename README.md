# Window - Heating Control (Open/Close)

This Home Assistant blueprint automates your heating system by responding to window open and close events, ensuring energy efficiency while maintaining comfort. 

## Features
- **Disable heating when a window is opened**: Automatically turns off the heating in the specified room(s) when a window is detected as open for a configurable duration.
- **Restore heating when the window is closed**: Automatically resumes heating after the window has been closed for a configurable duration.
- **Real-time notifications** (optional): Sends notifications to selected mobile devices with details about the action taken, including the room name, temperature, and timestamp.

## Requirements
1. **Window Sensor**: A binary sensor that detects whether the window is open or closed.
2. **Climate Entities**: Climate devices (e.g., thermostats) to control the heating.
3. **Notification Devices** (optional): Devices integrated with Home Assistant's mobile app to receive notifications.
4. **Input Boolean**: An input boolean to track if the window has been opened.

## Blueprint Inputs
| Input Name                | Description                                                                 | Default Value         |
|---------------------------|-----------------------------------------------------------------------------|-----------------------|
| **`window_sensor`**       | Binary sensor to detect if the window is open or closed.                    | Required              |
| **`climate_entities`**    | List of climate devices to control.                                        | Empty list (optional) |
| **`notify_devices`**      | List of mobile devices for notifications. Leave empty to disable.          | Empty list (optional) |
| **`room_name`**           | Name of the room for use in notifications.                                 | Required              |
| **`window_opened_flag`**  | Input boolean to indicate if the window has been opened.                   | Required              |
| **`window_open_duration`**| Time (in seconds) before turning off heating after the window is opened.   | 45 seconds            |
| **`window_close_duration`**| Time (in minutes) before resuming heating after the window is closed.      | 15 minutes            |

## Variables
| Variable Name             | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `room_name`               | Name of the room where the automation is applied.                          |
| `climate_entities`        | List of climate entities passed as input.                                  |
| `notify_devices`          | List of devices for sending notifications.                                 |
| `window_opened_flag`      | Input boolean to indicate if the window has been opened.                   |
| `current_temperature`     | The current outdoor temperature (replace with your temperature sensor).    |
| `temperature_unit`        | Unit of measurement for temperature (e.g., °C or °F).                      |

## Automation Flow
### When the Window is Opened:
1. If the window remains open for the specified `window_open_duration`:
   - Sets the `window_opened_flag` to `on`.
   - Turns off the specified climate devices in `auto` mode.
   - Sends a notification (if configured) to the selected devices with room and temperature details.

### When the Window is Closed:
1. If the window remains closed for the specified `window_close_duration`:
   - Turns the `window_opened_flag` back to `off`.
   - Restores the climate devices to `auto` mode.
   - Sends a notification (if configured) to the selected devices.

## Installation
1. **Copy the Blueprint**: Copy the YAML code into a new blueprint in Home Assistant.
2. **Import the Blueprint**: Navigate to **Settings > Automations & Scenes > Blueprints**, and create a new blueprint by pasting the YAML code.
3. **Create an Automation**:
   - Use the imported blueprint to create an automation.
   - Fill in the required inputs, such as the window sensor, climate entities, and room name.
4. **Test the Automation**:
   - Open and close the window to verify the behavior.
   - Check logs for any issues.

## Example Notification
- **Title**: "Heating Management"
- **Message (window opened)**: "Heating stopped in Living Room, 5°C outside (14:30:45)"
- **Message (window closed)**: "Heating resumed in Living Room, 5°C outside (14:45:30)"

## Notes
- Update the `current_temperature` variable to match your temperature sensor entity.
- Notifications are optional. If you don't want notifications, leave `notify_devices` empty.
- Ensure the input boolean (`window_opened_flag`) is created in Home Assistant before using this blueprint.

## Contributing
Feel free to contribute to this blueprint by submitting a pull request or opening an issue on [GitHub](https://github.com/your-repo/your-blueprint).

## License
This blueprint is licensed under the MIT License.

