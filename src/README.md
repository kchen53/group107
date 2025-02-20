

## API

Pomodoro Planner aids the creation of a study session environment. We make use of a RESTful API to facilitate http requests and responses. Data is accepted and returned in the JSON format.

> Base URL: <br>
> 127.0.0.1:8081/

### Contents  

- [**Todo**](#todo)
    - [Create](#create)  <br>
    - [Get All](#get-all)  <br>
    - [Get By ID](#get-by-id)  <br>
    - [Update](#update)  <br>
    - [Delete](#delete) <br>
- [**Event**](#event)
    - [Create](#create-event)  <br>
    - [Get All](#get-all-events)  <br>
    - [Get By ID](#get-event-by-id)  <br>
    - [Update](#update-event)  <br>
    - [Delete](#delete-event) <br>
- [**User**](#user)
    - [Signup](#signup) <br>
    - [Login](#login) <br>
    - [Logout](#logout) <br>
    - [Get Username](#get-username) <br>

---

### Todo

##### Fields:

> **"id"** number <br>
> Unique key for every todo. Used for updating, deleting, or getting specific todo items

> **"name"** string <br>
> String name for todo describing the task

> **"date"** string <br>
> Due date is held in a string of format "YYYY-MM-DD" where YYYY is the year, MM is the month, DD is the day

> **"time"** number *Format: seconds (null OK)* <br>
> Integer representing time spent/time left for task. Time is in seconds and can be null if not needed.

> **"repeat"** number <br>
> Signifies how often to repeat task. Data is the integer value of a 7 digit binary flags: <br>
>> | Sun | Mon | Tue | Wed | Thu | Fri | Sat |
>> |-----|-----|-----|-----|-----|-----|-----|
>> |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
> Example 1. If todo is to repeat every Sunday, then the value would be bin(1000000) = int(64) <br>
> Example 2. If todo is to repeat every Monday, Wednesday, and Friday, then the value would be bin(0101010) = int(42) <br>

> **"complete"** boolean <br>
> Boolean value signifying whether the task has been completed or not

####  Create

> <font color="orange">POST</font> 127.0.0.1:8081/todo <br>

Creates a new Todo item, returns the created Todo item<br>

##### Input Fields:

>> **"name"** number <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "name":"Pay pomos",
    "date":"2021-03-26",
    "time":3600,
    "repeat":0,
    "complete":false
}
```
 
##### Output Fields:

>> **"id"** number <br>
>> **"name"** string <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 0,
    "name": "Pay pomos",
    "date": "2021-03-26",
    "time": 3600,
    "repeat": 0,
    "complete": false
}
```
          
#### Get All

> GET 127.0.0.1:8081/todo <br>

Returns a list of all stored Todo items <br>

##### Output Fields:

>> **"id"** number <br>
>> **"name"** string <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
[
    {
        "id": 0,
        "name": "Pay pomos",
        "date": "2021-03-26",
        "time": 3600,
        "repeat": 0,
        "complete": true
    },
    {
        "id": 2,
        "name": "Release doros",
        "date": "2021-03-31",
        "time": null,
        "repeat": 2, //Note: Every Friday
        "complete": false
    }
]
```

#### Get by ID

> GET 127.0.0.1:8081/todo/{id} <br>

Returns the Todo item with the id designated by the address

##### Output Fields:

>> **"id"** number <br>
>> **"name"** string <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 0,
    "name": "Pay pomos",
    "date": "2021-03-26",
    "time": 3600,
    "repeat": 64, //Note: Every Sunday
    "complete": true
}
```
#### Update

> PUT 127.0.0.1:8081/todo/{id} <br>

Modifies the Todo item with the id designated by the address, returns the updated Todo item<br>

##### Input Fields:

##### Input Fields:

>> **"name"** number <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "name":"Pay pomos",
    "date":"2021-03-26",
    "time":3600,
    "repeat":0,
    "complete":true
}
```
 
##### Output Fields:

>> **"id"** number <br>
>> **"name"** string <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 0,
    "name": "Pay pomos",
    "date": "2021-03-26",
    "time": 3600,
    "repeat": 0,
    "complete": true
}
```

#### Delete

> DELETE 1270.0.1:8081/todo/{id} <br>

Deletes the Todo items with the id designated by the address, returns the deleted Todo item<br>

##### Output Fields:

>> **"id"** number <br>
>> **"name"** string <br>
>> **"date"** string *Format: "YYYY-MM-DD"* <br>
>> **"time"** number *Format: seconds (null OK)* <br>
>> **"repeat"** number *Format: Binary flags (see Todo)* <br>
>> **"complete"** boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 7,
    "name": "",
    "date": "",
    "time": 0,
    "repeat": 0,
    "complete": false
}
```

### Event

##### Fields:

> **"id"** number <br>
> Unique key for every event. Used for updating, deleting, or getting specific event items

> **"title"** string <br>
> String name for event describing the task

> **"start"** string *Format: YYYY-MM-DDTHR:MT:SC.MSCZ* <br>
> Time the event begins in a string of format "YYY-MM-DDTHH:MM:SS.MSSZ" where:
> - YYYY is the year
> - MM is the month
> - DD is the day
> - HR is the hour (00-23)
> - MT is the minute (00-59)
> - SC is the second (00-59)
> - MSS is the milisecond (000-999)

> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
> Time the event ends in a string of format "YYY-MM-DDTHH:MM:SS.MSSZ" where:
> - YYYY is the year
> - MM is the month
> - DD is the day
> - HR is the hour (00-23)
> - MT is the minute (00-59)
> - SC is the second (00-59)
> - MSS is the milisecond (000-999)

> **"color"** string *Format: #RRGGBB* <br>
> Used to color code the events in a string formatted with the hexcode for the color where:
> - RR is the red channel in hexadecimal
> - GG is the green channel in hexadecimal
> - BB is the blue channel in hexadecimal

####  Create Event

> <font color="orange">POST</font> 127.0.0.1:8081/event <br>

Creates a new Event item, returns the created Event item<br>

##### Input Fields:

>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "title": "Trip",
    "start": "2023-04-28T04:00:00.000Z",
    "end": "2023-04-30T04:00:00.000Z",
    "color": "#ad2121"
}
```
 
##### Output Fields:

>> **"id"** number <br>
>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 17,
    "title": "Trip",
    "start": "2023-04-28T04:00:00.000Z",
    "end": "2023-04-30T04:00:00.000Z",
    "color": "#ad2121"
}
```
          
#### Get All Events

> GET 127.0.0.1:8081/event <br>

Returns a list of all stored Event items <br>

##### Output Fields:

>> **"id"** number <br>
>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Output:

```json
[
    {
        "id": 17,
        "title": "Trip",
        "start": "2023-04-28T04:00:00.000Z",
        "end": "2023-04-30T04:00:00.000Z",
        "color": "#ad2121"
    },
    {
        "id": 18,
        "title": "SWE Project Due",
        "start": "2023-04-19T04:00:00.000Z",
        "end": "2023-04-19T04:00:00.000Z",
        "color": "#ad2121"
    }
]
```

#### Get Event by ID

> GET 127.0.0.1:8081/event/{id} <br>

Returns the Event item with the id designated by the address

##### Output Fields:

>> **"id"** number <br>
>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 17,
    "title": "Trip",
    "start": "2023-04-28T04:00:00.000Z",
    "end": "2023-04-30T04:00:00.000Z",
    "color": "#ad2121"
}
```
#### Update

> PUT 127.0.0.1:8081/event/{id} <br>

Modifies the Event item with the id designated by the address, returns the updated Event item<br>

##### Input Fields:

##### Input Fields:

>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "id": 17,
    "title": "Trip",
    "start": "2023-04-28T00:00:00.000Z",
    "end": "2023-04-31T04:00:00.000Z",
    "color": "#ad2121"
}
```
 
##### Output Fields:

>> **"id"** number <br>
>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 17,
    "title": "Trip",
    "start": "2023-04-28T00:00:00.000Z",
    "end": "2023-04-31T04:00:00.000Z",
    "color": "#ad2121"
}
```

#### Delete Event

> DELETE 1270.0.1:8081/event/{id} <br>

Deletes the Event items with the id designated by the address, returns the deleted Event item<br>

##### Output Fields:

>> **"id"** number <br>
>> **"title"** string <br>
>> **"start"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"end"** string *Format: YYYY-MM-DDTHH:MM:SS.MSSZ* <br>
>> **"color"** string *Format: #RRGGBB* <br>
> 
> Style: Raw JSON

###### Example Output:

```json
{
    "id": 21,
    "title": "",
    "start": "",
    "end": "",
    "color": ""
}
```

### User

####  Signup

> <font color="orange">POST</font> 127.0.0.1:8081/signup <br>

If the username does not already exist then creates a new user and logs in, returns whether a new user was successfully created <br>

##### Input Fields:

>> **"username"** string <br>
>> **"password"** string <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "username":"Pomodoro",
    "password":"ILovePomos",
}
```
 
##### Output Fields:

>> boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
true
```

####  Login

> <font color="blue">PUT</font> 127.0.0.1:8081/login <br>

Logs in if a the a user with the given credentials exists, returns whether the login was successful <br>

##### Input Fields:

>> **"username"** string <br>
>> **"password"** string <br>
> 
> Style: Raw JSON

###### Example Input:

```json
{
    "username":"Pomodoro",
    "password":"ILovePomos",
}
```
 
##### Output Fields:

>> boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
false
```

####  Logout

> <font color="red">PUT</font> 127.0.0.1:8081/logout <br>

Logs out, setting the user to "Anonymous"<br>
 
##### Output Fields:

>> boolean <br>
> 
> Style: Raw JSON

###### Example Output:

```json
true
```
####  GetUsername

> <font color="green">GET</font> 127.0.0.1:8081/userdata <br>

Returns the username of the currently logged in user, returns "Anonymous" if not logged in; returns "" if there is a server side error <br>
 
##### Output Fields:

>> string <br>
> 
> Style: Raw JSON

###### Example Output:

```json
"Anonymous"
```
      
