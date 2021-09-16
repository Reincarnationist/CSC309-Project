# CSC309-Project
Only the README file because team project is private.
Below is the README.
# Vaccinity

'Vaccinity' is a a platform that improves the experience and process surrounding vaccinations.

## Installation

Use the npm to install necessary modules.

```bash
npm install
```

## Usage

Start scripts by npm start.
```bash
npm start
```

## Heroku Link

https://pure-savannah-70273.herokuapp.com/

# Home Page
## Menu bar
  The home button is linking to the home page. The Article button is linking to article pages. The Appointment button is linking to booking of appointment (login is not required for now ).

## Tabs Section

### First Tab (Who and When)
In this section, you can find information on vaccine schedules on childhood, school-age, and adult immunization. You'll also find information on vaccines and pregnancy, travel vaccines, and vaccination for immigrants. You can simply click on the button of interest and that will lead you to an information page. Please be aware that you cannot access the information pages solely through url, please start from the home page.

### Second Tab (What Vaccination Do You Need)
You can select and input birth-dates of interest and location of interest and find vaccination information regarding the location or age group. Clicking the Search button will lead you to a page with all the information.

## Articles
You can click on an article of interest to view the article. You can also click on the "Explore All" button in the articles section on Home page or the "Articles" button on the navbar to view all available articles. If your account has the admin status, then you can choose to edit a specific article by selecting that article and the "Edit" button on the top right. Admins can also all articles by going to the page with all articles and selecting the "Add Article" button on the top right. 

## Slideshow
A slideshow with different images that direct users to different pages, a small gallery that shows info about vaccine.

# Book Appointment
Appointment contains three pages in total. In order to make an appointment user has to log in first. <br />

The first page is a welcome page with some important infomation that user should know, and there's a giant "book now" button in the certer of the screen, after user clicks this button they will be directed to the next page.

The second page is for user to choose their preferences for the booking. The user will have to choose the booking date they want first through a date picker which can only select the next three days. All the other invalid date inputs will prevent the user to move forward. After user selects a valid date they can see available time slots on that day, the system will check the database to see which slots are not available and disable the choice. User can also pick a different date at this point. After the user has selected a time slot it will appear as a pink-color button, and a dialog will pop up that asks user if they want to use a different phone number for this booking. If the user tries to click a selected button then an alert will pop up. After making all these choices the user can move forward to the next page which is the result page. <br />

The last page is a result table that shows the booking is done with all the choices that the user just made. <br />
The user can review and cancel their bookings in dashboard/Appointment.

# Login Page
On the top right corner there is a LOGIN button from which you could log in to access the dashboard. There are 2 pre-created accounts in the database. Please select the correct type for login.
General User: username="user" password="user"
Health Professional (Admin): username="admin" password="admin"

From the login page, you could press the register button to redirect you to the registration page. You should be automatically logged in after making a new account successfully. There is also a link to go back to the log in page from the registration page.

# User Dashboard
After logging in, you will be redirected to the Dashboard Home page. On the top is the menu bar for you to access the website, while on the left there is a side navigation bar to redirect to different pages for user functionalities.
  1. Dashboard Home: A first page that greets you after logging in.
  2. My profile: A whole section to access your personal information and changing them, including password.
  3. Immunization record (eIR): A detailed history of your vaccination.
  4. Appointment: A page to check all your upcoming appointments.

# Admin Dashboard
Very similar to User Dashboard. After logging in, you will be redirected to the Dashboard Home page. On the top is the menu bar for you to access the website, while on the left there is a side navigation bar to redirect to different pages for admin functionalities.
  1. Dashboard Home: A first page that greets you after logging in.
  2. My profile: A whole section to access your personal information and changing them, including password.
  3. Search User: A search page to search for specific user(s) and modify their information, including the ability to add new vaccination history.
  4. Appointment: A page to check all your upcoming appointments.
  
# Overview of Routes
## "/images"
### post 
a POST route to *create* an image
### get 
a GET route to get all images
### delete 
a DELETE route to remove an image by its id.

## "/users/login"
### post
A route to login (for general user) and create a session
  Request body expects:
  {
  "username": <username of the user>
  "password": <password of the user>
  }

## "/admins/login"
### post
A route to login (for health professional) and create a session

## "/check-session"
### get
A route to check if a user/admin is logged in on the session cookie

## "/logout"
### get
A route to logout a user/admin

## "/users/register"
### post
A route to *create* a user

## "/users"
### get
For Admin to get all users

## "/users/:id"
### get
A route to get a user by their id
### put
A route to update User's information
### delete
A route to delete a user by their id


## "/users/:id/password"
### put
A route to update User's password

## "/users/:id/vaccine"
### post
A route to add Vaccination History of a user

## "/users/:id/vaccine/:vid"
### delete
A route to delete a Vaccination History from a user
### put
A route to edit Vaccination History of a user

## "/admins/register"
### post
A route to *create* an admin

## "/admins/:id"
### get
A route to get an admin by their id
### put 
A route to update Admin's information

## "/admins/:id/password"
### put
A route to update Admin's password

## "/users/:id/bookings"
Request body expects:<br />
{<br />
"userName": username of the user <br />
"date": date of the booking <br />
"time": time of the booking <br />
}<br />
  
This is the route for booking features
### post
A route to *create* a booking for the user <br />
  It only occurs in /Date which is when the user is making an appointment. <br />
 <br />
  After the user completes their choices on the appointment, a post request will be sent to the server contains <br />
  "date": the booking date (required),<br />
  "time": the booking time (required), <br />
  "phoneNum": the phone number that is stored in user's profile (required), <br />
  and a "temp_phone": (required) if a user wants to use a differnet phone number for this booking only then this booking will show this temporarily phone number. This won't change the phone number that in user's profile. Also this value will be set to "New Phone Number" instead of "" to avoid mongoose required field check (mongoose does not allow empty string to pass the required check.)<br />
  <br />
  Returned JSON should have the updated user database   <br />
  document that the user was added to, AND the booking subdocument:   <br />
  { "booking": booking subdocument, "user": entire user document}   <br />
### get
A route for getting information for one user's all booking history   <br />
  Returned An array with JSONs that have all the booking history of the user   <br />
  [{booking 1}, {booking 2}]
## "/users/:id/bookings/:bookingId"
### delete
A route for delete booking by bookingId <br />
  Returned JSON should have the updated user database <br />
  document from which the user was deleted, AND the user subdocument deleted: <br />
  { "booking_got_deleted": booking subdocument, "user": entire user document} <br />


## "/articles"
Request body expects: <br />
{ <br />
  "title1": title <br />
  "date": "date YYYY/MM/DD" <br />
  "author": "name"
  "contetn1": "serve as summary" <br />
  "title2": "title2" <br />
  "content2": "content" <br />
  "title3": "title3" <br />
  "content3": "content" <br />
  "content4": "content" <br />
}
  
### post
A route to *create* an article 
### get
A route to get all articles

## "/articles/:id"
### get
A route to get a single article by id
### delete
A route to delete an article by id
### put
A route to update article specified by id

## "/vaccines"
### get
A route to get all the recommended vaccines for EIR
### post
A route to add recommended vaccines for EIR





