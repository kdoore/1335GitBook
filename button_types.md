#Button Types

Based on the simple button state example in the previous section, now we'll look at how we can use buttons to create user-interface behaviors in a customized drawing application.

##Examples of Button-Types
###Light-Switch
In the previous example, the button had visually distinct on and off behavior-states, and it controlled 2 different color-states of an ellipse. This 2-state behavior button (ignoring hover-states), is similar to a wall light switch, where we can look at the switch and observe that it in 1 of 2 possible physical configuration states.  We modeled this system with a 2-state finite state machine, where the states of the button were `on` or `!on`. 

###Door Bell
A door-bell type button behaves in a more instantaneous manner. The button can be thought of as generating an impulse-signal, which is sometimes referred to as a 'bang' in data-flow systems.  This pulse can be used to trigger an event, but the button's state-change behavior isn't visually obvious. This is the type of button behavior that we'll use in our drawing application to control clearing the canvas.  The main difference between this button and the light switch button is that the button state is primarily used to control another object, so that the button itself doesn't display 2-state behavior.  For these buttons, it's important to remember to include code to switch the button state to `!on` once it's done triggering the controlled event.

###Radio Buttons
Radio Buttons, like those used to select a car's radio station or used in web pages, represent another functional style of button behavior.  In this case, several buttons are linked together as a group, which is controlled by a single 'activeButton' state, where the currently selected button represents the active state for the system.  For our drawing application, we'll use this type of button to allow the user to select the drawing tool (either one of several patterns or the eraser).  