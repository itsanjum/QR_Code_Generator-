# QR Code Generator

This project is a simple Node.js application that:
1. Uses the `inquirer` package to take user input (a URL).
2. Converts the user-provided URL into a QR code image using the `qr-image` package.
3. Saves the provided URL into a text file using Node.js's native `fs` module.

---

## Prerequisites

Before running this application, make sure you have the following installed:

- [Node.js](https://nodejs.org) (LTS version recommended)
- npm (comes with Node.js installation)

---

## Installation

1. Clone the repository or copy the code into a directory.
2. Navigate to the project directory:
   ```bash
   cd <your-project-directory>
   ```
3. Install the required npm packages:
   ```bash
   npm install inquirer qr-image
   ```

---

## Usage

1. Run the application:
   ```bash
   node <your-file-name>.js
   ```
2. Enter a URL when prompted.
3. The application will:
   - Generate a QR code image (`qr_img.png`) in the project directory.
   - Save the entered URL to a text file (`URL.txt`) in the project directory.

---

## Code Overview

```javascript
import inquirer from 'inquirer';
import qr from 'qr-image';
import fs from 'fs';

// Prompt the user for a URL
inquirer
  .prompt([
    {
      message: "Type in your URL: ",
      name: "URL",
    },
  ])
  .then((answers) => {
    const url = answers.URL;

    // Generate QR code image
    const qr_svg = qr.image(url);
    qr_svg.pipe(fs.createWriteStream('qr_img.png'));

    // Save the URL to a text file
    fs.writeFile('URL.txt', url, (err) => {
      if (err) throw err;
      console.log('The file has been saved!');
    });
  })
  .catch((error) => {
    if (error.isTtyError) {
      console.error('Prompt could not be rendered in the current environment.');
    } else {
      console.error('An error occurred:', error);
    }
  });
```

---

## Files Generated

1. `qr_img.png`: Contains the generated QR code image for the provided URL.
2. `URL.txt`: Stores the user-provided URL as plain text.

---

## Notes

- Ensure that the project directory has write permissions to save the generated files.
- If the application fails, check the versions of the installed npm packages to ensure compatibility.

---

## Dependencies

- [inquirer](https://www.npmjs.com/package/inquirer): For prompting the user for input.
- [qr-image](https://www.npmjs.com/package/qr-image): For generating QR code images.

---

