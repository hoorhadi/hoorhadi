<!---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Problem Solver</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<style>
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #000;
    color: #c0c0c0;
}

#container {
    max-width: 800px;
    margin: 20px auto;
    padding: 20px;
    background-color: #111;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
}

h1 {
    text-align: center;
    color: #ffd700;
}

#welcomeMessage {
    margin-bottom: 20px;
    padding: 15px;
    background-color: #ffd700;
    color: #000000;
    border-radius: 5px;
    text-align: center;
}

#questionList {
    list-style-type: none;
    padding: 0;
    margin: 0;
}

#questionList li {
    cursor: pointer;
    margin: 10px 0;
    padding: 15px;
    border-radius: 5px;
    background-color: #ffd700; 
    color: #000000;
    transition: background-color 0.3s;
}

#questionList li:hover {
    background-color: #ffd900b6;
}

#solutionOutput {
    margin-top: 20px;
    padding: 20px;
    background-color: #111;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(255, 187, 0, 0.64);
    color: #ffffff;
}
</style>
    <div id="container">
        <h1>Problem Solver</h1>
        <div id="welcomeMessage"></div>
        <ul id="questionList"></ul>
        <div id="solutionOutput"></div>
    </div>
        
    <script>
    var data = [
    // JavaScript Questions (30)
    { question: "What is JavaScript?", answer: "JavaScript is a scripting language that enables you to create dynamically updating content, control multimedia, animate images, and much more within web browsers." },
    { question: "Explain the difference between 'let', 'const', and 'var' in JavaScript.", answer: "'let' and 'const' are block-scoped, while 'var' is function-scoped. 'let' allows reassignment, 'const' is for constants, and 'var' is an older way of declaring variables." },
    { question: "What is a closure in JavaScript?", answer: "A closure is a function bundled together with references to its surrounding state. It allows the function to access variables from its outer function even after the outer function has finished execution." },
    { question: "What is the 'this' keyword in JavaScript?", answer: "The 'this' keyword refers to the current execution context or the object to which the function belongs. Its value is determined by how a function is called." },
    { question: "Explain the concept of prototypal inheritance in JavaScript.", answer: "JavaScript uses prototypal inheritance, where objects can inherit properties and methods from other objects through a prototype chain. Each object has a prototype object, and properties/methods are inherited from it." },
    { question: "What is event delegation in JavaScript?", answer: "Event delegation is a technique where a single event listener is attached to a common ancestor rather than individual elements. It helps in handling events for multiple elements efficiently." },
    { question: "How does asynchronous programming work in JavaScript?", answer: "Asynchronous programming in JavaScript involves using functions like callbacks, promises, and async/await. These mechanisms allow non-blocking execution, enabling the program to perform tasks concurrently." },
    { question: "What is the difference between 'null' and 'undefined'?", answer: "'null' is an assignment value that represents the intentional absence of any object value, while 'undefined' is a variable that has been declared but has not yet been assigned a value." },
    { question: "Explain the purpose of the 'use strict' directive in JavaScript.", answer: "The 'use strict' directive is used to enable strict mode in JavaScript, catching common coding mistakes and preventing the use of certain error-prone features. It promotes safer and more maintainable code." },
    { question: "What is a callback function in JavaScript?", answer: "A callback function is a function passed as an argument to another function. It is executed after the completion of some operation, such as an asynchronous task or an event." },
    { question: "How do you handle errors in JavaScript?", answer: "Errors in JavaScript can be handled using try-catch blocks. The 'try' block contains the code that may throw an exception, and the 'catch' block handles the exception, allowing you to take appropriate actions." },
    { question: "What is the purpose of the 'bind' method in JavaScript?", answer: "The 'bind' method in JavaScript is used to create a new function that, when called, has its 'this' keyword set to a specific value. It is often used to bind a function to a particular context." },
    { question: "Explain the event loop in JavaScript.", answer: "The event loop is a mechanism in JavaScript that allows for non-blocking execution. It continuously checks the call stack and the message queue, pushing callbacks to the call stack when the stack is empty." },
    { question: "How do you create and manipulate arrays in JavaScript?", answer: "Arrays in JavaScript can be created using array literals ([]), and various methods are available for manipulation, including adding/removing elements, iterating, and using higher-order functions like 'map' and 'filter'." },
    { question: "What is the purpose of the 'async' and 'await' keywords in JavaScript?", answer: "'async' and 'await' are used for asynchronous programming in JavaScript. The 'async' keyword is used to define an asynchronous function, and 'await' is used to pause execution until a Promise is resolved or rejected." },
    { question: "What are arrow functions in JavaScript?", answer: "Arrow functions are a concise way to write functions in JavaScript. They have a shorter syntax and automatically bind to the surrounding context ('this'). Arrow functions are especially useful for short, one-line functions and callbacks." },
    { question: "Explain the concept of hoisting in JavaScript.", answer: "Hoisting in JavaScript refers to the behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase. However, only the declarations are hoisted, not the initializations." },
    { question: "How do you handle asynchronous operations in JavaScript without using async/await?", answer: "Asynchronous operations in JavaScript can be handled using callbacks and promises. Callbacks involve passing a function as an argument to another function, while promises provide a cleaner way to work with asynchronous code using 'then' and 'catch'." },
    { question: "What is the purpose of the 'map' function in JavaScript?", answer: "The 'map' function in JavaScript is used to create a new array by applying a provided function to each element of an existing array. It returns a new array without modifying the original array." },
    { question: "Explain the concept of debouncing in JavaScript.", answer: "Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, making it more efficient. It involves delaying the execution of a function until after a certain amount of time has passed since the last invocation." },
    { question: "How does the 'localStorage' object work in JavaScript?", answer: "The 'localStorage' object in JavaScript allows you to store key-value pairs in a web browser with no expiration time. The stored data persists even after the browser is closed, providing a simple way to save and retrieve information." },
    { question: "What is the difference between '== and '===' in JavaScript?", answer: "In JavaScript, '==' is the equality operator that performs type coercion, while '===' is the strict equality operator that compares both value and type without type coercion. It is recommended to use '===' for precise equality checks." },
    { question: "Explain the concept of the 'Promise' object in JavaScript.", answer: "A 'Promise' in JavaScript represents the eventual completion or failure of an asynchronous operation and its resulting value. It has three states: pending, resolved (fulfilled), and rejected. Promises simplify handling asynchronous code and allow chaining of asynchronous operations." },
    { question: "How does the 'apply' method work in JavaScript?", answer: "The 'apply' method in JavaScript is used to invoke a function with a given 'this' value and an array or array-like object of arguments. It allows you to set the context (value of 'this') and pass an array of arguments to a function." },
    { question: "Explain the concept of event bubbling in JavaScript.", answer: "Event bubbling in JavaScript is a phase in the event propagation model where an event starts from the target element and bubbles up through its ancestors in the DOM tree. It allows you to handle events at a higher level, simplifying event delegation." },
    { question: "What is the purpose of the 'defer' attribute in script tags?", answer: "The 'defer' attribute in script tags is used to defer the execution of the script until the HTML parsing is complete. It ensures that the script is executed in order after the HTML document is fully parsed, improving page load performance." },
    { question: "Explain the concept of the 'spread' operator in JavaScript.", answer: "The 'spread' operator in JavaScript is used to expand elements of an array or properties of an object. It allows you to copy array elements or object properties into a new array or object, making it useful for creating shallow copies." },

    // HTML Questions (10)
    { question: "What is HTML?", answer: "HTML (HyperText Markup Language) is the standard markup language used to create the structure of web pages. It consists of elements represented by tags, and each tag describes different document content or structure." },
    { question: "What is the purpose of the 'DOCTYPE' declaration in HTML?", answer: "The 'DOCTYPE' declaration in HTML specifies the document type and version being used. It helps browsers render web pages correctly by triggering the browser to use specific rendering modes, such as standards mode or quirks mode." },
    { question: "Explain the difference between 'block-level' and 'inline' elements in HTML.", answer: "Block-level elements in HTML create a new block or box and typically start on a new line, while inline elements do not start on a new line and only take up as much width as necessary. Examples of block-level elements include <div> and <p>, while <span> is an inline element." },
    { question: "What is the 'alt' attribute in the 'img' tag used for?", answer: "The 'alt' attribute in the 'img' tag is used to provide alternative text for an image. This text is displayed if the image cannot be loaded and is also used by screen readers for accessibility." },
    { question: "How do you create a hyperlink in HTML?", answer: "A hyperlink in HTML is created using the 'a' (anchor) tag. The 'href' attribute is used to specify the URL of the destination. For example: <a href='https://example.com'>Click here</a>." },
    { question: "What is the purpose of the 'meta' tag in HTML?", answer: "The 'meta' tag in HTML is used to provide metadata about the document, such as character set, viewport settings, and description. Common 'meta' tags include 'charset', 'viewport', and 'description'." },
    { question: "How do you create a numbered list in HTML?", answer: "A numbered list in HTML is created using the 'ol' (ordered list) tag. Each list item is represented by the 'li' (list item) tag. For example: <ol><li>Item 1</li><li>Item 2</li></ol>." },
    { question: "What is the purpose of the 'form' element in HTML?", answer: "The 'form' element in HTML is used to create an interactive form that allows users to input data. It can contain various form elements such as text fields, checkboxes, radio buttons, and buttons for form submission." },
    { question: "How do you create a table in HTML?", answer: "A table in HTML is created using the 'table' tag. It contains rows represented by the 'tr' (table row) tag and cells represented by the 'td' (table data) tag. The 'th' (table header) tag is used for header cells. For example: <table><tr><th>Header 1</th><th>Header 2</th></tr><tr><td>Data 1</td><td>Data 2</td></tr></table>." },
    { question: "What is the purpose of the 'span' tag in HTML?", answer: "The 'span' tag in HTML is an inline container used to group and apply styles to inline elements. It does not add any specific visual formatting but can be styled using CSS or used for JavaScript operations." },

    // CSS Questions (10)
    { question: "What is CSS?", answer: "CSS (Cascading Style Sheets) is a style sheet language used for describing the presentation of a document written in HTML or XML. It defines how elements should be displayed, including layout, colors, fonts, and spacing." },
    { question: "Explain the difference between 'margin' and 'padding' in CSS.", answer: "In CSS, 'margin' is the space outside an element, creating space between the element and its surrounding elements, while 'padding' is the space inside an element, creating space between the element's content and its border." },
    { question: "How do you center an element horizontally and vertically in CSS?", answer: "To center an element horizontally, use 'margin: 0 auto;' for block-level elements. To center vertically, use 'display: flex; align-items: center; justify-content: center;' for the container, or 'position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);' for the element." },
    { question: "What is the 'box model' in CSS?", answer: "The 'box model' in CSS describes the layout of elements on a web page. It consists of content, padding, border, and margin. Understanding the box model is essential for controlling the dimensions and spacing of elements." },
    { question: "How can you hide an element in CSS?", answer: "To hide an element in CSS, you can use the 'display: none;' property. This property removes the element from the normal flow of the document, making it invisible and taking up no space." },
    { question: "What is the purpose of the 'float' property in CSS?", answer: "The 'float' property in CSS is used to specify whether an element should be placed to the left or right of its container, allowing text and inline elements to wrap around it. However, it is often better to use modern layout techniques like flexbox or grid." },
    { question: "Explain the concept of CSS selectors.", answer: "CSS selectors are patterns used to select and style HTML elements. They can target elements based on their type, class, ID, attributes, and relationships with other elements. CSS selectors play a crucial role in styling specific elements or groups of elements." },
    { question: "How do you create a responsive design in CSS?", answer: "To create a responsive design in CSS, use media queries to apply different styles based on the device's characteristics, such as screen width. Implement flexible layouts, fluid grids, and relative units to ensure proper scaling on various devices." },
    { question: "What is the 'position' property in CSS used for?", answer: "The 'position' property in CSS is used to control the positioning of an element within its containing element. Common values include 'static' (default), 'relative', 'absolute', 'fixed', and 'sticky'. Each value provides different ways to position an element on the page." },
    { question: "How can you include external stylesheets in an HTML document?", answer: "External stylesheets in CSS can be included in an HTML document using the 'link' element with the 'rel' attribute set to 'stylesheet' and the 'href' attribute pointing to the external CSS file. For example: <link rel='stylesheet' href='styles.css'>." }
];

document.addEventListener("DOMContentLoaded", function () {
    // Display a welcome message
    var welcomeMessage = document.getElementById("welcomeMessage");
    welcomeMessage.innerHTML = "Welcome! Click on a question to view the answer.";

    // Display the list of questions
    var questionList = document.getElementById("questionList");
    data.forEach(function (item, index) {
        var listItem = document.createElement("li");
        listItem.textContent = item.question;
        listItem.addEventListener("click", function () {
            showAnswer(index);
        });
        questionList.appendChild(listItem);
    });
});

function showAnswer(index) {
    // Display the answer corresponding to the selected question
    var solutionOutput = document.getElementById("solutionOutput");
    solutionOutput.innerHTML = "<strong>Answer:</strong> " + data[index].answer;
}

    </script>
</body>
</html>
--->
