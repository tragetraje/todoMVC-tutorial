# NOTES

##  1. Requirements v1

  1.  It should have a place to store todo

     We can store our items(todos) in a list (called array in JS) and give our array a nickname for easy referencing, var todo:  
     `var todos = ['item1', 'item2', 'item3'];`

  2. It should have a way to display todo  
     To fulfill the requirement of v1 we can just:

     `console.log('My todos: ', todos);`

  3. It should have a way to add new todos

     We can just do: `todos.push('item 4');`  
     Now our todos looks like:  

     `var todos = ['item1', 'item2', 'item3', 'item 4'];`

  4. It should have a way to change a todo(update it)

     Grab the item you want to update and assign it a new value like so, for example the first item:

     `todos[0] = 'item 1 updated';`  

     Our updated array:

     `todos = ["item 1 updated", "item 2", "item3"];`

  5. It should have a way to delete a todo

     `todos.splice(item's index, how many items we want to delete);`   
     `todos.splice(0, 1);`

     So our todos now:  
     `todos = ["item 2", "item3"]];`

##  2. Requirements v2

  1.  Skip to 2. as the items are stored in the same todos variable
  2.  Let's write a function to display todos:  
  ```javascript
  function displayTodos() {  
          console.log('My todos:', todos);
  }
  ```
  and then invoke it: `displayTodos();`  

  3.  How would we add a new todo? Writing a function:  
  ```javascript
  function addTodos() {
          todos.push('new todo'); // add todo
          displayTodos(); // display our todos array
  }
  ```
  `addTodos(); // adds 'new todo' at the end of the todos array`
  But what if we don't want to add 'new todo' every time?
  ```javascript
  function addTodos(todo) {
          todos.push(todo); // add todo
          displayTodos(); // display our todos array
  }
  ```
  4.  How we would change our todo?

     In the previous version we were just updating the value like so:  
  `todos[0] = 'changed value';`  

    How to do it with a function and be able to change any item with any value?  
  ```javascript
  function changeTodo(position, newValue) {
          todos[position] = newValue;
          displayTodos(); // display the new updated list
  }
  ```  
  Then call the function and see what happens!! Yay!!  
  `changeTodo(0, 'new changed value');`

  5. How do we write a delete function?  

    In our previous version we just did:  
    `todos.splice(position, numberOfItems);` or  
    `todos.splice(0, 1);`  

    How we'll rewrite it in a function:
  ```javascript
  function deleteTodo(position) {
    	todos.splice(position, 1);
      displayTodos();
  }
  ```
  And call this function `deleteTodo(0);`

##  3. Requirements v3

  Let's try to understand what an object is, actually it's a way to store different types of data in one place. Real world examples like computer or myself can be described with an object like so:

  ```javascript
  var zina = {
    name: "Zina",
    sayName: function() {
      console.log(this.name); // to reference an object inside which our method operates we use 'this' keyword
    }
  };
  ```

  Storing our data in an object will help to organise our code as well, everything related to todos will be inside one object  

  Follow along app.js file


##  4. Requirements v4 and introduction to booleans

  We'll get rid of that initial todos array, leave it blank since now we don't want to store that simple todos strings but an object with different types of data. Such as an item itself (we called it todoText) and a boolean value if this todo is completed (by default it's not)

  Let's work on our second requirement, by changingTodo we should just change our todoText property only

  So we'll just rename newValue parameter to todoText as it sounds more descriptive and we want to grab just todoText property of todo object that we pushed so to target it we do:  
  `this.todos[position].todoText`

  In a new toggleCompleted method we grab the completed property of our newly added item `todoList.todos[position].completed` (or simply `this.todos[position].completed`) and flip its original value with the bang operator `!`:

  `this.todos[position].completed = !this.todos[position].completed;`

##  5. Requirements v5

  For loops trivia...

  To refactor our displayTodos method to loop through our todos array we use a for loop like so:
  ```javascript
  for (var i = 0; i < this.todos.length; i++) {
    // and we access every item like so
    console.log(this.todos[i].todoText);
  }
  ```
  To comply with the second requirement we should use an if statement:
  ```javascript
  if (this.todos.length === 0) {
    console.log('Your todo list is empty');
  } else {
    for (var i = 0; i < this.todos.length; i++) {
        // and we access every item like so
        console.log(this.todos[i].todoText);
      }
    }
  ```
  We want to be able to show the completed tasks in our displayTodos function, we can do this with an if statement like so:
  ```javascript
  if (this.todos[i].completed === true) {
    console.log('(x)', this.todos[i].todoText);
  } else {
        console.log('( )', this.todos[i].todoText);
  }
  ```

##  6. Requirements v6

  In version 6 we are going to work solely on one feature which consists of two parts:  
  1.  How to toggle all the tasks to false when all of them are true or otherwise make them all true:  

  Start with case 1, but how can we get totalTodos (that's this.todos.length) and completedTodos?
  ```javascript
  toggleAll: function() {
        var totalTodos = this.todos.length;
        var completedTodos = 0; // a counter for completed tasks, we assume it's 0 in the beginning
        // Get number of completed todos
        for (var i = 0; i < totalTodos; i++) {
          if (this.todos[i].completed === true) {
            completedTodos++;
          }
        }
        // Case 1: if everything is true, make everything false
        if (completedTodos === totalTodos) {
          for (var i = 0; i < totalTodos; i++) {
            this.todos[i].completed = false;
          }
        }
      }  
  ```  
  2. In the second case we just need to add an if statement.

  ```javascript
  toggleAll: function() {
        var totalTodos = this.todos.length;
        var completedTodos = 0; // a counter for completed tasks, we assume it's 0 in the beginning
        // Get number of completed todos
        for (var i = 0; i < totalTodos; i++) {
          if (this.todos[i].completed === true) {
            completedTodos++;
          }
        }
        // Case 1: if everything is true, make everything false
          if (completedTodos === totalTodos) {
            for (var i = 0; i < totalTodos; i++) {
              this.todos[i].completed = false;
            }
          } else {
          // Case 2: otherwise, make everything true
            for (var i = 0; i < totalTodos; i++) {
              this.todos[i].completed = true;
            }
          }
        this.displayTodos();
      }
  ```

##  Data types. Primitives vs objects

  Primitives: strings, numbers, booleans, undefined and null

  When comparing them, its' actual value is compared:
  ```
  1 === 1 // true
  1 === 2 // false
  true === true // true
  true === false // false
  ```
  Objects: objects, arrays and any data type made with them
  when comparing their actual memory addresses (references) are compared and not the actual values:

  ```
  {} === {} // false
  [1, 2] === [1, 2] // false
  ```

  But, if you compare their references:
  ```
  var houseA = {};
  houseA === houseA // true;
  ```

##  7. Requirements v7

  Get access to `document` object from the console and see the methods defined on it.

  Let's create two button elements in our HTML "Display Todos" and "Toggle All", now we want to get access to the buttons from our js. We want to run `todoList.displayTodos()` method when someone clicks a button.

  To get an access to the button we create a variable:

  `var displayTodosButton = document.getElementById("displayTodosButton");`

  And then an event listener to run the method:

  ```javascript
  displayTodosButton.addEventListener('click', function(){
    todoList.displayTodos();
  });
  ```
  Repeat for `toggleAll()`.


##  Learning how to use Chrome's built-in debugger

  With debugger we pause the program when it's running to be able to inspect the code step by step;
  ```javascript
  displayTodos: function() {
      debugger; // write this line in your code to enable debugger
      if (this.todos.length === 0) {
        console.log('Your todo list is empty!');
      } else {
        console.log('My todos:');
        for (var i = 0; i < this.todos.length; i++) { // Let's loop over an array and access todoText property of each added item
          //console.log(this.todos[i].todoText);

          if (this.todos[i].completed === true) {
            console.log('(x)', this.todos[i].todoText);
          } else {
            console.log('( )', this.todos[i].todoText);
          }
        }
      }
    }
  ```
  To debug a piece of code you actually need to run it first, so we go to console and do:

  `todoList.displayTodos();` (or use our new Display Todos button)

  A sources tab with debugger menu will open up as the code reaches the debugger statement in my code, the program will stop at this line (paused in debugger line appears on the screen):

  Then click "step over to next function call", the program will stop at the if statement, hovering over the condition `this.todos.length === 0` you can see that the length = 0 and todos is an array. Press the arrow button again and the script will run to the end of the method avoiding else statement (as there are no todos).

  To exit the debugger just press "Resume script execution", remove "debugger;" line from your code.

  It's possible to step into an internal function like so:
  ```
  todoList.addTodo(todoText) {
  //...
  //...
  this.displayTodos(); // to step into this method use arrow down symbol, step into the function to inspect this function too.
  }
  ```

##  8. Requirements v8

  Let's first refactor our code a bit, instead of using ids on our html button elements and then attaching event listeners to each of them we could just create a new handlers object, get rid of button ids and use button attribute onclick to run the methods:

  With new requirements we'll have to take user's input into account, introduce `<input>` since it's the way to write the todos in our simple UI.

  Let's organise our html first:
  ```
  <div>
  <button onclick="handlers.displayTodos()">Display Todos</button>
  <button onclick="handlers.toggleAll()">Toggle All</button>
  </div>

  <div>
    <button onclick="handlers.addTodo()">Add</button>
    <input id="addTodoTextInput" type="text">
  </div>
  ```
  Working on changeTodo button and input of position and todo, add this to our html:
  ```
  <div>
      <button onclick="handlers.changeTodo()">Change Todo</button>
      <input id="changeTodoPositionInput" type="number">
      <input id="changeTodoTextInput" type="text">
  </div>
  ```
  then define `handlers.changeTodo();`

  `handlers.deleteTodo()` and `handlers.toggleCompleted()` will look similar to the previous methods

##  9. Requirements v9

  We're going to escape from the console in this version, all our todos will be displayed in the current window and not the console

  We're going to insert dynamically with JS the items of the todo list

  First, create static empty `<ul></ul>` element in our html, we can do it this way since it's the only unordered list on the page now.

  The `<li>` element will be created dynamically within <ul> with JS like so:
  `
  var todoLi = document.createElement('li');
  var todosUl = document.querySelector('ul');

  `  
  Then, we just append a child element into the `<ul>` we've found on the page:

  `todosUl.appendChild(todoLi);`

  Working on the first requirement to add an li element for each new todo, we create a new view object, and a new displayTodos function which will replace later our original `todoList.displayTodos()` like so:
  ```javascript
  var view = {
    displayTodos: function(){
      var todosUl = document.querySelector('ul');
      // this line makes sure <ul> is empty before adding any new li elements, //otherwise each time you call view.displayTodos() after adding the //elements new bullet points will be added
      todosUl.innerHTML = '';
      for (var i = 0; i < todoList.todos.length; i++){
        var todoLi = document.createElement('li');
        todosUl.appendChild(todoLi);
      }
    }
  };
  ```  
  Now, to add .todoText to each li, we should do this inside the for loop of `view.displayTodos()`:

  `todoLi.textContent = todoList.todos[i].todoText;`

  Let's do the logic to show whether the task was completed or not:

  Create a couple of new variables:
  `
        var todo = todoList.todos[i];
        var todoTextWithCompletion = '';

  `  
  If statement:
  `
        if (todo.completed === true) {
          todoTextWithCompletion = '(x) ' + todo.todoText;
        } else {
          todoTextWithCompletion = '( ) ' + todo.todoText;
        }
  `
  And then update the content like so:

  `todoLi.textContent = todoTextWithCompletion;`

  To finish this part of the course and completely escape from the console, we should clean up our code a bit, and get rid of our old `todoList.displayTodos()` method and its instances. Instead, we'll place our new `view.displayTodos()` method at the end of methods defined on handler object

##  Functions inside of functions

  Let's create a function that logs 10 numbers:

  ```javascript
  function logNumbers() {
    for (var i = 0; i < 10; i++) {
      console.log(i);
    }
  }
  ```

  But what if we want to debug the function with the debugger? We'd run:

  ```javascript
  debugger;
  logNumbers();
  ```

  Instead of doing that we could create a function which would run a debugger for us:

  ```javascript
  function runWithDebugger(ourFunction){
    debugger;
    ourFunction();
  }
  ```

  So next time when we want to debug our function we'd do:

  ```javascript
  runWithDebugger(function logNumbers() {
    for (var i = 0; i < 10; i++) {
      console.log(i);
    }
  });
  ```
  We've simplified the task of debugging for us. The ability to run functions inside functions is very powerful, it enhances the behaviour of other functions.

  E.g.: built-in `setTimeout();` function which acts as an alarm, it'll run the function we'll pass in 5000ms(5s) period of time:

  ```javascript
  setTimeout(function(){
    console.log("Wake up!");
  }, 5000);
  ```

  So it enhances the behaviour of passed in function by turning it in a timer or alarm clock.

  Another example of enhanced function is `forEach()` which acts on all arrays and basically executes the function we pass in to `forEach()` on every element of array:

  ```javascript
  var students = ['anne', 'pete', 'bruno'];

  function logName(name){
    console.log(name);
  }

  logName(students[0]); // anne
  logName(students[1]); // pete

  for (var i = 0; i < students.length; i++){
    logName(students[i]);
  }
  ```

  But we can automate that like so:

  ```javascript
  students.forEach(logName);

  // or

  students.forEach(function logName(name){
    console.log(name);
  });

  // or

  students.forEach(function(name){
    console.log(name);
  });  
  ```

  Actually, we can write a similar function to built in `forEach()` ourselves:

  ```javascript
  function forEach(myArray, myFunction){
    for (var i = 0; i < myArray.length; i++){
      myFunction(myArray[i]);
    }
  }

  forEach(students, logName); // logName will serve as it takes a student's name as a parameter
  ```

  You'll notice similar patterns with built-in `addEventListener`:

  ```javascript
  var currentElement = $0; // to reference a highlighted element in Chrome
  currentElement.addEventListener('click', function(){
    alert('Click!'); // it'll alert when the element is clicked
  });

  // or

  currentElement.addEventListener('click', function(event){
    console.log(event); // it'll log event-object to the console if you choose to
    alert('Click!');
  })
  ```

  In the code examples above, `forEach()`, `setTimeout()` and `addEventListener()` are called higher order functions, they accept other functions as arguments and enhance their behaviour.

  The functions we pass in to higher order functions as parameters are callback functions.

##  10. Requirements v10

  We're working on creating a new delete button, to simplify our code we'll write a new method to do that which finally should return a button:

  ```javascript
  var view = {
    displayTodos: function() {
      // method
    },
    createDeleteButton: function() {
      var deleteButton = document.createElement('button');
      deleteButton.textContent = 'Delete';
      deleteButton.className = 'deleteButton';
      return deleteButton;
    }
  };
  ```

  To add a delete button to each todo we should just grab a reference to each li element and insert created button element inside `view.displayTodos()` like so: `todoLi.appendChild(this.createDeleteButton());`

  Working on assigning each li element its unique id we should just do that:
  `todoLi.id = i;` inside the for loop.

  To get an access to todo's is from delete button we'll use `addEventListener()` function. Thinking about which element should have an event listener attached it's probably logical to think about li elements, since that's where we created the delete buttons. But, attaching an event listener to each li we'll finish with a lot of them working with the app and it could lead to performance problems. So it's smarter to attach it to unordered list since it's the parentNode of li. How we can do that? With event object we pass in to `addEventListener()` function.

  Let's grab the reference to ul:

  `var todosUl = document.querySelector('ul');`

  and then explore event object clicking triggering an event from delete button:

  ```javascript
  todosUl.addEventListener('click', function(event) {
      console.log(event.target.parentNode.id); // logs li's id
    });
  ```

  Clever!

  Let's make our delete button actually delete the created todo and update the DOM:

  ```javascript
  var view = {
    displayTodos: function() {
      // code
    },
    createDeleteButton: function() {
      // code
    },
    setUpEventListeners: function() {
      var todosUl = document.querySelector('ul');

      todosUl.addEventListener('click', function(event) {
        var elementClicked = event.target;

        if (elementClicked.className === 'deleteButton') {
          handlers.deleteTodo(parseInt(elementClicked.parentNode.id));
        }
      });
    }
  };
  ```

  Don't forget to get rid of old deleteTodo functionality in `handlers.deleteTodo()` and pass in a position `handlers.deleteTodo(position)`
   and call our function:

  `view.setUpEventListeners();`

  Cleaning up the code we can completely get rid of Delete button div in our index.html

  And wrapping up, we've used event delegation pattern by making our ul element respond to click events of child delete button

##  Requirements v11

  We're going to re-write our for loops and replace them with `forEach()` method, it makes them easier to read and less error prone. Our new todoList.toggleAll() method will look like so:

  ```javascript
  toggleAll: function() {
    var totalTodos = this.todos.length;
    var completedTodos = 0;

    // Get number of completed todos.
    this.todos.forEach(function(todo) {
      if (todo.completed === true) {
        completedTodos++;
      }
    });

    this.todos.forEach(function(todo) {
      // Case 1: If everything’s true, make everything false.
      if (completedTodos === totalTodos) {
        todo.completed = false;
      // Case 2: Otherwise, make everything true.
      } else {
          todo.completed = true;
      }
    });
  }
  ```

  and `view.displayTodos()`:

  ```javascript
  displayTodos: function() {
    var todosUl = document.querySelector('ul');
    todosUl.innerHTML = '';

    todoList.todos.forEach(function(todo, position) {
      var todoLi = document.createElement('li');
      var todoTextWithCompletion = '';

      if (todo.completed === true) {
        todoTextWithCompletion = '(x) ' + todo.todoText;
      } else {
        todoTextWithCompletion = '( ) ' + todo.todoText;
      }

      todoLi.id = position;
      todoLi.textContent = todoTextWithCompletion;
      todoLi.appendChild(this.createDeleteButton());
      todosUl.appendChild(todoLi);

    }, this);
  }
  ```

  Here there are a couple of nuances:

  We actually are able to pass two arguments to our callback function of `forEach()` method, a todo on which it operates and its index in an array, e.g position. Because of that we can do `todoLi.id = position;`

  Besides that, to access our view object from within `todoLi.appendChild(this.createDeleteButton());` function we should pass `this` as a second argument to `forEach(callback, this);`
