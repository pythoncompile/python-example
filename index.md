# Python Compiler Web Application

This web application allows users to write, compile, and execute Python code directly in their browser. Built using HTML, Tailwind CSS, and Brython, it provides a simple and interactive interface for running Python code snippets. Below is a detailed overview of the components and functionality of the application.

## HTML Structure

The HTML structure consists of a `<head>` section for meta information and styles, and a `<body>` section containing the main content of the application.

### Head Section

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Python Compiler</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <style>
    body, button, input, textarea, h1 {
      font-weight: bold;
    }
  </style>
</head>
```

- **Meta Tags:** Define the character set and viewport settings for responsive design.
- **Title:** Sets the title of the webpage.
- **CSS Links:** Imports Tailwind CSS for styling.
- **Inline Styles:** Applies bold font weight to specific elements for emphasis.

### Body Section

```html
<body class="bg-gray-200 p-4">
  <div class="max-w-lg mx-auto bg-white p-6 rounded-md shadow-md">
    <h1 class="text-2xl mb-4">Python Compiler</h1>
    <textarea id="inputCode" class="w-full h-32 p-2 border rounded-md" placeholder="Enter your Python code here..."></textarea>
    <button onclick="compilePython()" class="mt-4 px-4 py-2 bg-blue-500 text-white rounded-md">Compile</button>
    <div id="output" class="mt-4 p-2 border rounded-md"></div>
  </div>
</body>
```

- **Main Container:** A centered, white background container with padding and rounded corners for the main content.
- **Heading:** A prominent heading for the application.
- **Textarea:** A text area for users to input their Python code.
- **Button:** A button to trigger the compilation of the Python code.
- **Output Div:** A container to display the output or error messages.

## JavaScript Functionality

The functionality for running Python code is provided by Brython, a Python 3 implementation for client-side web programming.

### Script Section

```html
<script src="https://cdn.jsdelivr.net/gh/pythonpad/brython-runner/lib/brython-runner.bundle.js"></script>
<script>
  const runner = new BrythonRunner({
    stdout: {
      write(content) {
        document.getElementById('output').innerHTML += content + "<br>";
      },
      flush() {},
    },
    stderr: {
      write(content) {
        document.getElementById('output').innerHTML += '<span class="text-red-500">' + content + "</span><br>";
      },
      flush() {},
    },
    stdin: {
      async readline() {
        var userInput = prompt();
        return userInput;
      },
    }
  });

  function compilePython() {
    var code = document.getElementById('inputCode').value;
    document.getElementById('output').innerHTML = ''; // Clear previous output
    runner.runCode(code); // Run the Python code
  }
</script>
```

- **Brython Runner Initialization:** Sets up BrythonRunner to handle standard output, error output, and input.
  - **stdout.write:** Appends normal output to the output div.
  - **stderr.write:** Appends error messages to the output div with red text.
  - **stdin.readline:** Prompts the user for input if needed.
- **compilePython Function:** Retrieves the code from the textarea, clears any previous output, and runs the code using BrythonRunner.

## Usage

To use this Python Compiler, visit the [Python Compiler Web Application](https://lelbois.nekoweb.org/py.html). This link will take you to the live application where you can enter your Python code, compile it, and see the output immediately.

## Summary

This Python Compiler web application provides an interactive environment for executing Python code in the browser. It leverages Brython to interpret and run the Python code, while Tailwind CSS ensures a clean and responsive user interface. The application is user-friendly, with clear sections for input, compilation, and output, making it a handy tool for quick Python code testing and learning.
