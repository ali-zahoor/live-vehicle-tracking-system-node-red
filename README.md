# Vehicle Delivery Tracking System

## Specification

A refrigerated delivery vehicle drives through a city to deliver packages. There are five short routes for the delivery vehicle, for five customers, created for testing purposes. This means that five packages will be delivered, one package being delivered per route. Messages are to be sent from the vehicle (which is the IoT device on local PC) to Google Cloud. 

## Description of the Vehicle Simulator

The following features are delivered by the vehicle simulator, which is provided for you. Please examine the output of the simulator to understand the various message types referred-to below:

- Each route has a set of n locations (lat-lon). The locations come from a (simulated) GPS unit on the vehicle as it is moving. The value of n can be different for each route.
- As the vehicle moves, a message including “msgType”: “vehicle” is emitted, comprising:
  - The current vehicle location is sent as a set of (lat, lon) coordinates.
  - The current Delivery-ID.
- The Delivery-ID is a unique ID for the package to be delivered to a customer.
- The current refrigeration temperature inside the vehicle.
- When a new route starts then a message including "msgType": "arrival_estimate" is emitted.
- When the nth location is sent for a particular route, then the destination has been reached, and that route is complete (package is delivered). A message including msgType: "delivered" is emitted to indicate that the package has been delivered.
- When one route is completed then the vehicle starts on the next route. When the final route is completed then the first route starts again. Since this is a simulation, the following also applies:
- The simulator starts, delivers messages for several routes, and then stops. Please refer to the video to ascertain how you can control the number of routes before the simulator stops.
- A message is emitted regularly with msgType: "refrigeration_status". This contains the current refrigeration temperature inside the vehicle.
- The delivery vehicle has inbuilt monitoring and when there is some type of vehicle fault then a message including msgType: "fault" is emitted. For testing purposes, such messages are generated regularly. 

## Node-Red Delivery Dashboard

- Current vehicle location values (Lat, Lon), as text.
- A chart of the vehicle refrigeration temperature over the last 10 minutes.
- A gauge with the current refrigeration temperature.
- The current Delivery-ID for the item being delivered, as text.
- The last fault message from the vehicle, as text.
- Button 1 yields the number of vehicle faults in the past 24 hours.
- Button 2 yields the number of "battery_charging_fault" events over the past week.
- Button 3 yields the highest, lowest, and mean refrigeration temperatures over the past 12 hours.
- Button 4 yields the number of times that the refrigeration temperature exceeds 3.5 degrees, in the past day.
- A ‘Clear’ button, to clear all the Dashboard items.
- A ‘Simulate’ button, to start the vehicle simulator, by sending an IoT Core ‘Command’ to the IoT device.

## Customer Google Map

A Google Map is provided, only for the use of one of the five customers. This map is based specifically upon the customer with "delivery_id": 456.
On the map there is a
- A marker to show the current location of the delivery vehicle.
- The marker will normally to be coloured blue, except when the vehicle is travelling on the route that has "delivery_id": 456; then the marker is coloured green.
- The marker has a pop-up infoWindow. 
  - When the vehicle is travelling on a route that is not "delivery_id": 456, then the popup should say “Delivery will be soon”.
  - When the vehicle is travelling on a route that is "delivery_id": 456, then the popup should say “Deliver ID 456 due for arrival”.

## A customer Slack Messaging feed!


Consider that the customer with "delivery_id": 456 has a Slack Messaging channel. Appropriate customer messages (with a clear sentence format) will be sent to this channel under the following two circumstances:
- When the route for "delivery_id": 456 starts (i.e. when the device sends the "msgType": "arrival_estimate" message for that delivery_id) then it must indicate to the customer that a delivery, with delivery_id, will arrive at the estimated time.
- It must convert the estimated UTC time into a date-time string. 
  - When the delivery has been completed for "delivery_id": 456 then it must indicate to the customer that the package with delivery_id has been delivered. Include the current time as a date-time string.




