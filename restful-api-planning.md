# Hunters Handbook

## API Selection

The public API i have selected is the Monster Hunter World Database found at https://mhw-db.com
This api provieds structured JSON data relating to Monster Hunter World which includes monsters, amour, weapons, items, skills, locations as well as other in-game information.
The API provides multiple RESTful  resourses that cna be retrieved using standard HTTP GET requests. The data returned will be processed and displayed dynamically within a web application.
The app will mostly use the monster resource to provide users with detailed information about individual monsters, including their species, weaknesses, resistances, locations and what loot they drop.
Rest Principles:
* Resource ID: Each resourse has a dedicated URL, such as /monsters or /weapons
* Stateless Comm: Each request contains the information required to process independently.
* Standard HTTP Methods: The GET requests will retrieve any existing information, while the POST requests will be used by the applications own backend to recieve submitted hunt plans.
* JSON data exchange: Responces are provided in a structured JSON format.
Any submissions will be used seperatly by Pythons backing while the Application will work with the Public API Chosen.

## Endpoint Mapping

public API endpoints
| Endpoint | HTTP method | Purpose |
| :--- | :--- | :--- |
| /monsters | GET | Retrieves all monsters |
| /monsters/{id} | GET | Retrieves an individual monster |
| /weapons | GET | Retrieves available weapons |
| /items | GET | Retrieve available items |
| /skills | GET | Retrieve available skills | 
| /locations | GET | Retrieve available locations in game |

backend endpoints
| /api/monsters | GET | Retrieves monster data from public API
| /api/monsters/{id} | GET | Retrieves information about specific Monster |
| /api/weapons | GET | Retrieves weapon info from API |
| /api/hunt-plans | POST | Accepts a users completed hunt preperation form

The backend will act as an intermediary between the front end and the API where it is necessary.

The POST endpoint will accept JSON data containing the user's hunt prep details. 

## Data Flow Diagram (textual)

Data flow:
1. User opens application: Browser loads HTML, CSS and JavaScript
2. JavaScript Fetch API: GET request to /api/monsters
3. Python Flask backend: Requests data from mhw-db.com
4. Public Monster Hunter API: Returns JSON monster information
5. Flask processes response: Validates response and returns JSON
6. JavaScript renders the interface: Dynamic cards, tables and monsters details

Loading and error handling
* Loading: Display a loading message while the request is processing
* Success: Convert the response into JSON and display the returned info
* Empty results: Display an appropriate message if no matching monsters are found
* Error: Display a user-friendly message if the request fails
* Retry: ALlow users to attempt the request again

Dynamic rendering
The moonsters information will be displayed using dynamicaly generated HTM elements.

For example. each monster in the databace could be represented by a car that contains its name, species, description, and creature type.

JavaScript will loop throughout the returned JSON and generate the relevnt HTML elements

Conditional Styling
CSS classes will be assigned based on Specific JSON values

Examples:
| ## Data Value | ## Conditional Styling |
| type === "large" | Large monster badge |
| type === "small" | Small monster badge |
| Weakness stars 3 | Strong weakness highlighted |
| Weakness stars 2 | Moderate weakness highlighted |
| Weakness stars 1 | Minor weakness highlighted |
| No weakness entries | Neutral styling |

These values will allow the user to identify important information quickly without manually reading every data field.

## Form Handing

The application will include a Hunt Preparation Form that allows users to submit their preferred hunting setup.

Form controls and validation

| Input field | Control | Validation |
| Hunter name | Text input | Required, 2-40 characters |
| Target monster | Dropdown | Required, must select a monster |
| Weapon type | Dropdown | Required, valid weapon category | 
| Preparation notes | Textarea | Optional, maximum 300 characters |
| Hunter rank | Number input | Required, postive integer |

Local validation rules

JavaScript will validate all form inputs before submitting the info

Validation will include:
* Required fields must not be empty.
* Hunter names must meet the minimum and maximum character limits.
* The target Monster must be selected from the monster list available.
* Weapon types must match options available.
* Hunter rank must be a positive whole number.
* Preparation notes must not exceed the character limit.

If validation fails it will display appropriate error message.

JSON payload transformation

Once it passes, the application will display an appropriate error message next to the relevant input.

The JSON object is submitted to the back end using POST

The /api/hunt-plans endpoint will accept the JSON and validate the info submitted.

The backend should return:
* 201 created when a hunt plan is accepted
* 400 Bad Request when information submitted is invalid
* 500 Internal Server Error when an unexpected error orccurs

## Technology Stack

The following will be used to develop the application

| Technology | Purpose |
| HTMLS | Application structure |
| CSS3 | Layout, design and conditional styling |
| JavaScript | Fetch API, form validation and dynamic rendering | 
| Python | Backend programming language |
| Flask | Backend routing and API communication | 
| Request | Python HTTP requests to the public API |
| JSON | Data exchange between front end and backend | 
| Visual Studio Code | Development environment |
| Postman | Testing backend endpoints |
| Browser Developer Tools | Debugging JavaScript and network requests |
| GitHub | Version control and project management

## Implementation Steps
| Stage | Implementation task | Expected outcome | 
| :--- | =--- | =--- |
| 1 | Set up the project structure | Working Project folders and initial files |
| 2 | Configure the flask application and API connetion | Backend can communicate with Monster Hunter World API |
| 3 | Implement GET requests | Monster data successfully retrieved |
| 4 | Add loading and error status | Users recieve feedback during requests | 
| 5 | Implement dynamic rendering | Monsters are displayed in cards or tables | 
| 6 | Add search and filtering | User can find specific monster |
| 7 | Create form controls | Hunt Preperation from what is available |
| 8 | Implement local validation | submissions that are invalid are prevented |
| 9 | Implementation of JSON POST handling | data from form sent to backend |
| 10 | Integrate conditional sytling | Monster types and weaknesses visually distinguished |
| 11 | Test the App | API, rendering and form functionality are verified |
| 12 | Review and document | app is completed and succefull. README created |

Devlopment order
1. Project set up: folders and files created
2. API connection
3. GET requests and loading states
4. Dynamic rendering
5. Search and filtering
6. Form controles and Validation is built
7. POST request defined
8. Conditional styling
9. Testing and documentation 