---
up:
  - "[[Py Module]]"
related: 
created: 2024-05-13
tags:
  - note/develop🍃
Link: https://www.geeksforgeeks.org/python-datetime-module/?ref=gcse
---
- `datetime` is a Python module to manipulate date, time etc
- `Date` and `DateTime` are an object in Python, so when you manipulate them, you are manipulating objects and not strings or timestamps.

## Classes
### date
- An idealized naïve date
- The date class is used to instantiate date objects
- It represents a date in the format **YYYY-MM-DD**
- The constructor of this class needs three mandatory arguments year, month, and date

The arguments must be in the following range –  

- MINYEAR <= year <= MAXYEAR
- 1 <= month <= 12
- 1 <= day <= number of days in the given month and year

```python
import datetime

my_date = datetime.date(2002, 10, 1)

print("My birthday is", my_date)
# My birthday is 2002-10-1
```

>[!warning]
>If the argument is not an integer it will raise a TypeError and if it is outside the range a ValueError will be raised.

#### Get the current date
We will use date `today()` function of the date class.
```python
from datetime import date

today = date.today()
print(today) # 2024-05-13
```
#### Get Today’s Year, Month, and Date
We can get the year, month, and date attributes from the date object
```python
from datetime import date

today = date.today()
print(today.year) # 2024
print(today.month) # 5
print(today.day) # 13
```
#### Get Date from Timestamp
- We can create date objects from timestamps using the `fromtimestamp()` method.
- The timestamp is the number of seconds from 1st January 1970 at UTC to a particular date.

```python
from datetime import datetime

date_time = datetime.fromtimestamp(1887639468)
print("Datetime from timestamp:", date_time)
# Datetime from timestamp: 2029-10-25 16:17:48
```

#### Convert Date to String
We can convert date object to a string representation using two functions `isoformat()` and `strftime()`.
```python
from datetime import date

today = date.today()

Str = date.isoformat(today)
print("String Representation", Str) # String Representation 2021-08-19
print(type(Str)) # <class 'str'>
```

#### Date Class methods
| Function Name     | Description                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------- |
| ctime()           | Return a string representing the date                                                               |
| fromisocalendar() | Returns a date corresponding to the ISO calendar                                                    |
| fromisoformat()   | Returns a date object from the string representation of the date                                    |
| fromordinal()     | Returns a date object from the proleptic Gregorian ordinal, where January 1 of year 1 has ordinal 1 |
| fromtimestamp()   | Returns a date object from the POSIX timestamp                                                      |
| isocalendar()     | Returns a tuple year, week, and weekday                                                             |
| isoformat()       | Returns the string representation of the date                                                       |
| isoweekday()      | Returns the day of the week as an integer where Monday is 1 and Sunday is 7                         |
| replace()         | Changes the value of the date object with the given parameter                                       |
| strftime()        | Returns a string representation of the date with the given format                                   |
| timetuple()       | Returns an object of type time.struct_time                                                          |
| today()           | Returns the current local date                                                                      |
| toordinal()       | Return the proleptic Gregorian ordinal of the date, where January 1 of year 1 has ordinal 1         |
| weekday()         | Returns the day of the week as integer where Monday is 0 and Sunday is 6                            |
### time
The time class creates the time object which represents local time, independent of any day.

All the arguments are optional. tzinfo can be None otherwise all the attributes must be integer in the following range – 

- 0 <= hour < 24
- 0 <= minute < 60
- 0 <= second < 60
- 0 <= microsecond < 1000000
- fold in \[0, 1]

```python
from datetime import time

my_time = time(13, 24, 56)
print(my_time) # 13:24:56

my_time = time(minute=12)
print(my_time) # 00:12:00

my_time = time()
print(my_time) # 00:00:00
```
#### Get hours, minutes, seconds, and microseconds
- Its attributes can also be printed separately
```python
from datetime improt time

Time = time (11, 34, 56)

print(Time.hour)
print(Time.minute)
print(Time.second)
print(Time.microsecond)
```

#### Convert Time object to String
We can convert time object to string using the `isoformat()` method.
```python
from datetime import time

Time = time(12, 24, 36, 1212)
Str = Time.isoformat()
print(Str) # 12:24:36.001212
```

#### Time class Methods
|Function Name|Description|
|---|---|
|dst()|Returns tzinfo.dst() is tzinfo is not None|
|fromisoformat()|Returns a time object from the string representation of the time|
|isoformat()|Returns the string representation of time from the time object|
|replace()|Changes the value of the time object with the given parameter|
|strftime()|Returns a string representation of the time with the given format|
|tzname()|Returns tzinfo.tzname() is tzinfo is not None|
|utcoffset()|Returns tzinfo.utcffsets() is tzinfo is not None|
### datetime
- It contains information on both date and time.

The year, month, and day arguments are mandatory. tzinfo can be None, rest all the attributes must be an integer in the following range –  

- MINYEAR <= year <= MAXYEAR
- 1 <= month <= 12
- 1 <= day <= number of days in the given month and year
- 0 <= hour < 24
- 0 <= minute < 60
- 0 <= second < 60
- 0 <= microsecond < 1000000
- fold in [0, 1]

```python
from datetime import datetime

# Initializing constructor
a = datetime(1999, 12, 12)
print(a) # 1999-12-12 00:00:00

# Initializing constructor
# with time parameters as well
a = datetime(1999, 12, 12, 12, 12, 12, 342380)
print(a) # 1999-12-12 12:12:12.342380
```
#### Get year, month, hour, minute, and timestamp
```python
from datetime import datetime

a = datetime(1999, 12, 12, 12, 12, 12)

print("year =", a.year)
print("month =", a.month)
print("hour =", a.hour)
print("minute =", a.minute)
print("timestamp =", a.timestamp())
```
#### Current date and time
```python
from datetime import datetime

# Calling now() function
today = datetime.now()

print("Current date and time is", today)
# Current date and time is 2019-10-25 11:12:11.289834
```

#### Convert Python Datetime to String
We can convert Datetime to string in Python using the `datetime.strftime` and `datetime.isoformat` methods. 

```python
from datetime import datetime as dt

# Getting current date and time
now = dt.now()

string = dt.isoformat(now)
print(string) # 2021-08-19T18:13:25.346259
print(type(string))
```

#### Datetime class Methods
|Function Name|Description|
|---|---|
|astimezone()|Returns the DateTime object containing timezone information.|
|combine()|Combines the date and time objects and return a DateTime object|
|ctime()|Returns a string representation of date and time|
|date()|Return the Date class object|
|fromisoformat()|Returns a datetime object from the string representation of the date and time|
|fromordinal()|Returns a date object from the proleptic Gregorian ordinal, where January 1 of year 1 has ordinal 1. The hour, minute, second, and microsecond are 0|
|fromtimestamp()|Return date and time from POSIX timestamp|
|isocalendar()|Returns a tuple year, week, and weekday|
|isoformat()|Return the string representation of date and time|
|isoweekday()|Returns the day of the week as integer where Monday is 1 and Sunday is 7|
|now()|Returns current local date and time with tz parameter|
|replace()|Changes the specific attributes of the DateTime object|
|strftime()|Returns a string representation of the DateTime object with the given format|
|strptime()|Returns a DateTime object corresponding to the date string|
|time()|Return the Time class object|
|timetuple()|Returns an object of type time.struct_time|
|timetz()|Return the Time class object|
|today()|Return local DateTime with tzinfo as None|
|toordinal()|Return the proleptic Gregorian ordinal of the date, where January 1 of year 1 has ordinal 1|
|tzname()|Returns the name of the timezone|
|utcfromtimestamp()|Return UTC from POSIX timestamp|
|utcoffset()|Returns the UTC offset|
|utcnow()|Return current UTC date and time|
|weekday()|Returns the day of the week as integer where Monday is 0 and Sunday is 6|
### Timedelta
### strftime
- String format time
- We use it to make the date or time string formated
- تقدر تنسقهم عادي زيهم زي أي string
```python
myBirthDay = datetime.datetime(1982, 10, 25)

print(myBirthDay.strftime("%a")) # Mon
print(myBirthDay.strftime("%A")) # Monday
print(myBirthDay.strftime("%b")) # Oct
print(myBirthDay.strftime("%a")) # October

print(myBirthDay.sytftime("%d/%B/%Y")) # 25/October/1982
```
### tzinfo()
### Timezone
