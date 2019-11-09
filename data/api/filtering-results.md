# Filtering results

```js

// empty array for results
let dogArray = [];
const resultsContainer = document.querySelector(".results");
const searchInput = document.querySelector(".search-input");
const searchButton = document.querySelector(".search-button");

// the API call will be made on page load when the browser gets here
fetch("path/to/api")
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        loopThroughDogs(json);
    });


function loopThroughDogs(dogObject) {

    // store the dog array in the variable we created at the top of the page
    dogArray = dogObject.cards;

    // loop through the dog objects in the array
    dogArray.forEach(function(dog) {

        resultsContainer.innerHTML += `<div class="dog">
                                            <h1>${dog.name}</h1>
                                            <img src="${dog.imageSrc}">
                                            <a href="path/to/more/details/${dog.id}">More details</a>
                                        </div>`;
    });

}

// listen for the click event on the search button
// when the event happens, the filterDogs function will run
searchButton.addEventListener("click", filterDogs);


function filterDogs() {

    // get what the user typed into the search input
    const searchValue = searchInput.value;
    // the search value and the name in each dog object must be the same case for the comparison to work
    const lowerCaseSearchValue = searchValue.toLowerCase();

    const filteredDogs = dogArray.filter(function(dog) {

        // make each name property lowercase
        const lowerCaseDogName = dog.name.toLowerCase();

        if(lowerCaseDogName.startsWith(lowerCaseSearchValue)) {
            return true
        }
    });

    // clear the current HTML
    resultsContainer.innerHTML = "";

    filteredDogs.forEach(function(dog) {

        resultsContainer.innerHTML += `<div class="dog">
                                            <h1>${dog.name}</h1>
                                            <img src="${dog.imageSrc}">
                                            <a href="path/to/more/details/${dog.id}">More details</a>
                                        </div>`;
    });

}


```
