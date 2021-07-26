# Teacherbuilt Timer
## A remote based classroom timer. 

-Allows users to create timers, remotely control a display. 
-Building out with 'room codes' initially, before implmenting user accounts.
-Tailwind CSS for responsive, simple clean design.
-Building novel time displays, giving users multiple options. Bars, circles, etc.



## Build Log
### 07.24.2021
* Auth set up. Using Google for the time being.
* Auth state passing as prop through layout route.
* Tailwind not making it to all pages?

### 07.25.2021
* Abandoning authentication right now for 'Room Codes'. Able to create and join rooms. Need to implment the time functionality. 
* Need to pass button press events down from JoinRoom to CreateRoom components.
* Rename components to Remote and Display?
* Really unsure of using Supabase for this. I need something realtime, easy to listen to event changes. Will likely rebuild into Firebase.
* Maybe try to pass up an event dispatcher?

### 07.26.2021
* Experimenting with event forwarding. Process should look like this: Remote event > Home page > Display component function