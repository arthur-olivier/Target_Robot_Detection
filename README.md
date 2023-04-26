# Target Robot Detection

This project aims to detect a target with a robot and determine its position using a Raspberry Pi and a STM32 microcontroller. The program was developed in Python with an object-oriented approach to allow for easy modification and addition of features.

# Classes

## Class Form
The Form class identifies and registers the shape of the target robot in the image. It has the following attributes:

* sommets: an integer that stores the number of vertices of the shape.
* pol: a string that stores the name of the recognized shape. If there is no shape, it takes the name 'undefined'.
* cX, cY: the coordinates on the X and Y axis of the center of the shape. These coordinates are 0 if there is no shape.
* collec_poly: a Python dictionary that matches the number of vertices with the name of the shape in string format. This allows for easy deduction of the name of the shape from the sommets attribute.

The following methods can be called:

* set_form(): updates the sommets and pol attributes.
* clear_form(): sets the pol attribute to 'undefined'.
* forme_exist(): returns True if a shape is present in the image.
* get_centre(): returns the coordinates of the center of the shape cX and cY.
* display_info(): writes certain information to the terminal output. This method is only useful for debugging purposes.

## Class Zone
The Zone class determines in which zone the target robot is located based on the shape found on it and the coordinates of its center. The different zones have been detailed in the previous section. The following methods are defined:

* get_zoneNb(): returns the zone number.
* get_name(): returns the name of the zone (e.g. "bottom left" for the zone_BG class).
* in_zone(cX, cY): returns True if the coordinates of the center cX, cY are within the specified zone.

This class uses inheritance to make it easy to add a new zone without breaking the program. By redefining the in_zone() function for each zone and changing the default attributes like zoneNb or name, new zones can be added without affecting the rest of the program.

## Class Robot
The Robot class facilitates the programming of messages to be sent to the STM32 microcontroller. It has the following attributes:

* cible: a string that stores the zone in which the target robot is located. This allows the program to send the correct message to the STM32 when a target is detected.
* dist: an integer value of the distance sent by the STM32.
* message: a string of the message to be sent to the STM32.

The following methods are defined:

* get_message(): returns the string with the message to be sent to the STM32.
* maj_distance(distance_parametre): updates the value of the distance sent by the STM32.
* maj_cible(): updates the cible attribute based on the information returned by the different Zone objects in the program.
* tempo(): allows for a delay using the time.sleep() function. This method is not used in the final recipe.

# Conclusion

This project demonstrates how to use object-oriented programming to develop a target robot detection program using a Raspberry Pi and a STM32 microcontroller. The implementation of three different classes allows the Raspberry Pi to interact with the STM32 microcontroller correctly and make decisions based on the information gathered from the image. This project can be easily modified or extended to include additional features
