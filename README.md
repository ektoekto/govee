# Control Function for Govee API

## Overview
This function handles all the needed communication with the Govee API. You can input simple control messages, and the function does the rest. You don't need to install anything to your Node-RED, just put the code into a function or import the flow.

## API Key Setup
You need to apply for the Govee API through the Govee app. Once you have the key, just copy it to **line 8** inside the parentheses. This is a simple and fast process.

## Initial Setup
For the very first time, send out this object to the function:
```json
{ "command": "devices" }
```
This initializes all the global objects and retrieves all your lights from Govee. If you add more lights or change their names, you should send this command again.

## Example Control Messages
![kuva](https://github.com/user-attachments/assets/d3b8d276-d729-4b24-90f6-477c4ad47ade)
The flow includes example messages that you can input into your lighting function. You can also connect the examples to a debug node for easy copying.

### Turning a Light On
```json
{ "command": "control", "name": "Table", "instance": "powerSwitch", "value": 1 }
```

### Adjusting Brightness
```json
{ "command": "control", "name": "Table", "instance": "brightness", "value": 50 }
```

### Multi-Message Control
You can set multiple settings in one message. For example, to turn **Light1** on, enable `gradientToggle`, call a `snapshot`, and set the `brightness`:
```json
{
    "command": "multi",
    "name": "Light1",
    "powerSwitch": 1,
    "gradientToggle": 1,
    "snapshot": "Day",
    "brightness": 10
}
```

## Using Snapshots
Using snapshots is the easiest way to get the light into your desired mode. Use the phone app to set up your desired settings, scene, and colors, then save it as a snapshot.

To call a snapshot, use:
```json
{ "command": "control", "name": "Table", "instance": "snapshot", "value": "Morning" }
```

## Handling Multiple Messages
You can send multiple messages at once. The function will store and handle them in order. Due to Govee API limitations, only one message can be sent at a time.

For example, if you have **5 lights** and each receives a multi-message with **4 parameters**, the function needs to send **20 individual messages**. This process happens quickly enough.

## Global Object Storage
The function stores the last parameter in the global object. For example, if the last message was **brightness**, you will see its value, but `gradientToggle` is `undefined`.

![kuva](https://github.com/user-attachments/assets/34ba09eb-3e40-47b2-b289-69b4199eedaa)

You can also check the global object to see the capabilities of a light, helping you determine which instances you can call when controlling the light.

---
This function streamlines Govee API integration with Node-RED, making smart lighting control simple and efficient.

