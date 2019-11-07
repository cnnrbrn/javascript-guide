# Form validation

Here is a simple form.

```html
<form id="contactForm">
    <fieldset>
        <legend>Contact form</legend>
        <div>
            <label for="firstName">Name</label>
            <input type="text" name="firstName" id="firstName" placeholder="At least 1 character">
            <div class="error firstname" style="display:none">Please enter your first name</div>
        </div>
        <div>
            <input type="submit" />
        </div>
    </fieldset>
</form>
```

We'll add the following validation code to an external file.

First we must find the form, the first name input and the first name error.

```js
// find the form and assign it to a variable
const contactForm = document.querySelector("#contactForm");
// or 
// const contactForm = document.getElementById("contactForm");

// find the first name input and assign it to a variable
const firstNameInput = document.querySelector("#firstName");

// find the first name error element and assign it to a variable
const firstNameError = document.querySelector(".error.firstname");
```

Our `validateName` function will make sure the length of a string passed into the function is greater than 0, after we have removed any spaces before or after the string.

```js
// this function will check whether the argument passed in has a length greater than 0
function validateName(name) {
    // use the trim function to remove spaces
    const trimmedName = name.trim();

    if(trimmedName.length > 0) {
        // name is valid
        // function will exit and return true
        return true;
    }
    // name is not valid
    // function will exit and return false
    return false;
}
```

Now we need to listen for the form's `submit` event using `addEventListener`:

```js
contactForm.addEventListener("submit", function(event) {})
```

When the submit event happens, the function will run. This function receives an `event` argument from the HTML form. We can use this argument to stop the default action of a form which is to submit the page.

The following blocks of code all happen inside the function:

```js

// if you console log the event you will see it has a lot of properties
// if you expand it's prototype property (__proto__ in Chrome), you will see all the properties it inherits
// one of those is the function preventDefault()
console.log(event);

// prevent the form performing it's default action of submitting the page
// if the page gets submitted, it will be reloaded and the validation won't run
event.preventDefault();

```

Now we need to get the value from the name input:

```js
// we need to get the value of the input(s) using the "value" property
const nameValue = firstNameInput.value;
```

Then we use the function we created above to validate the name:

```js
const nameIsValid = validateName(nameValue);
```

If the name is valid, we hide the error. (If we don't do this, the error won't clear if it's ever displayed because the validation failed).

If the name is not valid, the error is displayed.

```js
// if the name is valid, we hide the error message
if(nameIsValid) {
    firstNameError.style.display = "none";        
}
// if the name is not valid, show the error
else {
    firstNameError.style.display = "block";   
}
```

Here it is all together:

```js
// find the form and assign it to a variable
const contactForm = document.querySelector("#contactForm");
// or 
// const contactForm = document.getElementById("contactForm");

// find the first name input and assign it to a variable
const firstNameInput = document.querySelector("#firstName");

// find the first name error element and assign it to a variable
const firstNameError = document.querySelector(".error.firstname");

// this function will check whether the argument passed in has a length greater than 0
function validateName(name) {
    // use the trim function to remove spaces
    const trimmedName = name.trim();

    if(trimmedName.length > 0) {
        // name is valid
        // function will exit and return true
        return true;
    }
    // name is not valid
    // function will exit and return false
    return false;
}

// add an event listener to the form
// this will listen for a submit event
// when the submit event happens, the function will run
// it receives an "event" argument from the HTML form
contactForm.addEventListener("submit", function(event) {

    // if you console log the event you will see it has a lot of properties
    // if you expand it's prototype property (__proto__ in Chrome), you will see all the properties it inherits
    // one of those is the function preventDefault()
    console.log(event);
    
    // prevent the form performing it's default action of submitting the page
    // if the page gets submitted, it will be reloaded and the validation won't run
    event.preventDefault();

    // we need to get the value of the input(s) using the "value" property
    const nameValue = firstNameInput.value;

    // now we can use the validateName function to check if the name is valid
    const nameIsValid = validateName(nameValue);
    
    // if the name is valid, we hide the error message
    if(nameIsValid) {
        firstNameError.style.display = "none";        
    }
    // if the name is not valid, show the error
    else {
        firstNameError.style.display = "block";   
    }
    
})

```

Note: if an input field needs to pass the same validation as another, you can reuse the validation function. The name of the argument passed into the function doesn't matter outside of the function.


