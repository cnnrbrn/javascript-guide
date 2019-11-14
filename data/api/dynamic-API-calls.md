# Using a function for dynamic API calls and DOM manipulation

```js
// the function takes 2 arguments
// itemId will be used in the API call
// elementId will be used to select the HTML element
function getSpecificResult(itemId, elementId) {
    // create the URL string we will use for the API call using the itemId argument
    const url = "path/to/api/" + itemId;

    // either
    // make the fetch call using fat arrow syntax
    fetch(url)
        .then(response => response.json())
        .then(json => createHtml(json))
        .catch(error => console.log(error));

    // or
    // make the fetch call using normal function syntax
    fetch(url)
        .then(function(response) {
            return response.json();
        })
        .then(function(json) {
            createHtml(json);
        })
        .catch(function(error) {
            console.log("An error occured", error);
        });

    function createHtml(result) {
        // the result object holds all the result details
        // we can use . notation to access them
        // console.log(result.someDetail)

        // get the HTML element using the elementId argument
        const element = document.getElementById(elementId);

        // create the HTML using template literals
        element.innerHTML = `<div class="result__details">
                                <h4 class="result__name">${result.name}</h4>
                                <p class="result__age">Age: ${result.age}</p>
                            </div>`;
    }
}

// we can call the function as often we need to

// assuming <div id="someId" class="result"></div> exists
getSpecificResult(1, "someId");

// assuming <div id="someOtherId" class="result"></div> exists
getSpecificResult(83, "someOtherId");
```
