---
up:
  - "[[HTML]]"
related: 
created: 2024-06-09
---
An HTML form is used to collect user input.
It's a set of controls

## form Element
```html
<form>
.
Elements
.
</form>
```

The `<form>` element is a container for different types of input elements, such as: text fields, checkboxes, radio buttons, submit buttons, etc.

## label Element
The `<label>` element is useful for screen-reader users, because the screen-reader will read out loud the label when the user focuses on the input element.
The `<label>` element also helps users who have difficulty clicking on very small regions (such as radio buttons or checkboxes) - because when the user clicks the text within the `<label>` element, it toggles the radio button/checkbox.

The `for` attribute of the `<label>` tag should be equal to the `id` attribute of the `<input>` element to bind them together.

بنستخدمها عشان مخليش الكلام في الهوا كدا وعشان ال for تخلي اليوزر لو ضغط على الكلام يروح على البوكس

## input Element
The HTML `<input>` element is the most used form element.
An `<input>` element can be displayed in many ways, depending on the `type` attribute.

### text
```html
<form>
	<label for="fname">First name:</label><br>
	<input type="text" id="fname" name="fname"><br>
	<label for="lname">Last name:</label><br>
	<input type="text" id="lname" name="lname">
</form>
```

<form>
	<label for="fname">First name:</label><br>
	<input type="text" id="fname" name="fname"><br>
</form>

### password
```html
<form>  
  <label for="username">Username:</label><br>  
  <input type="text" id="username" name="username"><br>  
  <label for="pwd">Password:</label><br>  
  <input type="password" id="pwd" name="pwd">  
</form>
```
It will be masked.
![[Pasted image 20240609233808.png]]
### submit
a button for **submitting** form data to a **form-handler**
The form-handler is typically a server page with a script for processing input data.
```html
<form action="/action_page.php">
	<label for="fname">First name:</label><br>
	<input type="text" id="fname" name="fname" value="John"><br>
	<label for="lname">Last name:</label><br>
	<input type="text" id="lname" name="lname" value="Doe"><br><br>
	<input type="submit" value="Submit">
</form> 
```
If you omit the submit button's value attribute, the button will get a default text

### Reset
a **reset button** that will reset all form values to their default values

```html
<input type="reset" value="Reset">  
```

### radio
Radio buttons let a user select ONLY ONE of a limited number of choices:
```html
<p>Choose your favorite Web language:</p>  
  
<form>  
  <input type="radio" id="html" name="fav_language" value="HTML">  
  <label for="html">HTML</label><br>  
  <input type="radio" id="css" name="fav_language" value="CSS">  
  <label for="css">CSS</label><br>  
  <input type="radio" id="javascript" name="fav_language" value="JavaScript">  
  <label for="javascript">JavaScript</label>  
</form>
```
خد بالك ان لازم تحط ال attribute اللي اسمه name عشان دا هيحدد البارمتر اللي هيرجع في ال C# واللي هياخده ال input دا (في كل الحالات اللي فاتت)
في حالة ال radio لما بيعرف ان اتنين ليهم نفس القيمة بيعرف انهم تبع بعض فمش هينفع تحدد غير واحدة بس

To make one of them checked we will use `checked`

```html
<input type="radio" id="html" name="fav_language" value="HTML" checked />
```
### Checkbox
Checkboxes let a user select ZERO or MORE options of a limited number of choices.
```html
<form action="#">
	<input type="checkbox" id="bike" value="bike" />
	<label for="bike">I have a bike</label><br />
	<input type="checkbox" id="car" />
	<label for="bike">I have a car</label><br />
	<input type="checkbox" id="bus" />
	<label for="bike">I have a bus</label><br />

</form>
```

To make one of them checked we will use `checked`

```html
<input type="checkbox" id="bike" value="bike" checked />
```

### Button
We talked before about [[Buttons HTML]]
It's a new way to do it and we will use it to make a functions with JS work with it
```html
<input type="button" onclick="alert('Hello World!')" value="Click Me!">
```

### color
input fields that should contain a color.
```html
<form>  
  <label for="favcolor">Select your favorite color:</label>  
  <input type="color" id="favcolor" name="favcolor">  
</form>
```

### date
input fields that should contain a date
```html
<form>  
  <label for="birthday">Birthday:</label>  
  <input type="date" id="birthday" name="birthday">  
</form>
```

You can also use the `min` and `max` attributes to add restrictions to dates:

```html
<form>  
  <label for="datemax">Enter a date before 1980-01-01:</label>  
  <input type="date" id="datemax" name="datemax" max="1979-12-31"><br><br>  
  <label for="datemin">Enter a date after 2000-01-01:</label>  
  <input type="date" id="datemin" name="datemin" min="2000-01-02">  
</form>
```

### email
 input fields that should contain an e-mail address
 Some smartphones recognize the email type, and add ".com" to the keyboard to match email input.
 ```html
<form>  
  <label for="email">Enter your email:</label>  
  <input type="email" id="email" name="email">  
</form>
```

### file
a file-select field and a "Browse" button for file uploads
```html
<form>  
  <label for="myfile">Select a file:</label>  
  <input type="file" id="myfile" name="myfile">  
</form>
```

### range
a control for entering a number whose exact value is not important (like a slider control). Default range is 0 to 100.

```html
<form>  
  <label for="vol">Volume (between 0 and 50):</label>  
  <input type="range" id="vol" name="vol" min="0" max="50">  
</form>
```

### tel
input fields that should contain a telephone number.
```html
<form>  
  <label for="phone">Enter your phone number:</label>  
  <input type="tel" id="phone" name="phone" pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}">  
</form>
```

### time
allows the user to select a time (no time zone)
```html
<form>  
  <label for="appt">Select a time:</label>  
  <input type="time" id="appt" name="appt">  
</form>
```
### url
input fields that should contain a URL address
Some smartphones recognize the url type, and adds ".com" to the keyboard to match url input.
```html
<form>  
  <label for="homepage">Add your homepage:</label>  
  <input type="url" id="homepage" name="homepage">  
</form>
```

### hidden
defines a hidden input field (not visible to a user).
داتا مش هتظهر للعميل زي مثلًا انك تعمله id وتقدر تخزنها في ال DB
```html
<form>
	<label for="fname"> First name:</label>
	<input type="text" id="fname" name="fname"> <br><br>
	<input type="hidded" id="custID" name="custId" value="3487">
	<input type="submit" value="Submit">
</form>
```

**Note:** While the value is not displayed to the user in the page's content, it is visible (and can be edited) using any browser's developer tools or "View Source" functionality. Do not use hidden inputs as a form of security!
## Form and Input attributes
### Form
#### action
It have an important attribute called `action`
دا اللي بيحدد لما أضغط على زرار ال submit يعمل ايه بالظبط أو يروح فين
Usually, the form data is sent to a file on the server when the user clicks on the submit button.

In the example below, the form data is sent to a file called "action_page.php". This file contains a server-side script that handles the form data:

```html
<form action="/action_page.php">
	<input type="submit" value="Save">
</form>
```

لازم نوع ال input يبقا من النوع submit وهو لما بيضغط على الزرار دا بيعمل اللي في ال action
**Tip:** If the `action` attribute is omitted, the action is set to the current page.
#### Autocomplete
The `autocomplete` attribute specifies whether a form should have autocomplete on or off.
لو مفتوحة بياخد من الليوزر دخلها قبل كدا

The `autocomplete` attribute works with `<form>` and the following `<input>` types: text, search, url, tel, email, password, datepickers, range, and color.
```html
<form action="#" autocomplete="on">

<input type="email" id="email" name="email" autocomplete="off"><br><br>
```
### Input
#### name
Notice that each input field must have a `name` attribute to be submitted.
If the `name` attribute is omitted تم حذفه, the value of the input field will not be sent at all.

#### value
The input `value` attribute specifies an initial value for an input field:

```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname" value="John"><br>  
  <label for="lname">Last name:</label><br>  
  <input type="text" id="lname" name="lname" value="Doe">  
</form>
```

#### readonly
specifies that an input field is read-only.
A read-only input field cannot be modified (however, a user can tab to it, highlight it, and copy the text from it).
The value of a read-only input field will be sent when submitting the form!
```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname" value="John" readonly><br>  
  <label for="lname">Last name:</label><br>  
  <input type="text" id="lname" name="lname" value="Doe">  
</form>
```

#### disabled
specifies that an input field should be disabled.

A disabled input field is unusable and un-clickable.

The value of a disabled input field will not be sent when submitting the form!

```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname" value="John" disabled><br>  
  <label for="lname">Last name:</label><br>  
  <input type="text" id="lname" name="lname" value="Doe">  
</form>
```

#### min and max
The input `min` and `max` attributes specify the minimum and maximum values for an input field.

The `min` and `max` attributes work with the following input types: number, range, date, datetime-local, month, time and week.

**Tip:** Use the max and min attributes together to create a range of legal values.

```html
<form>  
  <label for="datemax">Enter a date before 1980-01-01:</label>  
  <input type="date" id="datemax" name="datemax" max="1979-12-31"><br><br>  
  
  <label for="datemin">Enter a date after 2000-01-01:</label>  
  <input type="date" id="datemin" name="datemin" min="2000-01-02"><br><br>  
  
  <label for="quantity">Quantity (between 1 and 5):</label>  
  <input type="number" id="quantity" name="quantity" min="1" max="5">  
</form>
```

#### placeholder
The input `placeholder` attribute specifies a short hint that describes the expected value of an input field (a sample value or a short description of the expected format).

The short hint is displayed in the input field before the user enters a value.

The `placeholder` attribute works with the following input types: text, search, url, number, tel, email, and password.

```html
<form>  
  <label for="phone">Enter a phone number:</label>  
  <input type="tel" id="phone" name="phone"  
  placeholder="123-45-678"  
  pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}">  
</form>
```

#### autofocus
The input `autofocus` attribute specifies that an input field should automatically get focus when the page loads.

```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname" autofocus><br>  
  <label for="lname">Last name:</label><br>  
  <input type="text" id="lname" name="lname">  
</form>
```

___
tabindex


#### required
بتقول ان ال filed لازم يبقا فيه داتا وميبقاش فاضي
```html
<input type="email" required>
```
![[Pasted image 20240623144546.png]]
## select Element
Defines a drop-down list.
```html
<label for="cars">Choose a car:</label>
<select name="cars" id="cars">
	<option value="0">Volvo</option>
	<option value="1">fiat</option>
	<option>lambo</option>
	<option>mpw</option>
</select>
```

The `<option>` element defines an option that can be selected.
The `value` will be send to DB
By default, the first item in the drop-down list is selected.
To define a pre-selected option, add the `selected` attribute to the option:
```html
<option value="fiat" selected>Fiat</option>
```
### Visible Values
Use the `size` attribute to specify the number of visible values
```html
<select id="cars" name="cars" size="3">
```

![[Pasted image 20240610123423.png]]

### Allow Multiple Selections
Use the `multiple` attribute to allow the user to select more than one value
```html
<select id="cars" name="cars" size="4" multiple>
```

## text area Element
The `<textarea>` element defines a multi-line input field (a text area)
```html
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
```
The `rows` attribute specifies the visible number of lines in a text area.
The `cols` attribute specifies the visible width of a text area.
You can also define the size of the text area by using CSS.