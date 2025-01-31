<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Password Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #8a6479;
        }
        .container {
            background: rgb(255, 255, 255);
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        input[type="number"] {
            width: 50px;
        }
        button {
            margin-top: 10px;
            padding: 8px 16px;
            cursor: pointer;
            background: #007BFF;
            color: white;
            border: none;
            border-radius: 4px;
        }
        button:hover {
            background: #0056b3;
        }
        #password {
            margin-top: 10px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Random Password Generator</h2>
        <label for="length">Length:</label>
        <input type="number" id="length" min="4" max="20" value="12">
        <br>
        <input type="checkbox" id="lowercase" checked> Lowercase
        <input type="checkbox" id="uppercase" checked> Uppercase
        <input type="checkbox" id="numbers" checked> Numbers
        <input type="checkbox" id="symbols" checked> Symbols
        <br>
        <button onclick="generatePassword()">Generate Password</button>
        <p id="password"></p>
        <button onclick="copyPassword()">Copy to Clipboard</button>
    </div>

    <script>
        function generatePassword() {
            const length = document.getElementById("length").value;
            const includeLower = document.getElementById("lowercase").checked;
            const includeUpper = document.getElementById("uppercase").checked;
            const includeNumbers = document.getElementById("numbers").checked;
            const includeSymbols = document.getElementById("symbols").checked;
            
            const lowerChars = "abcdefghijklmnopqrstuvwxyz";
            const upperChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
            const numberChars = "0123456789";
            const symbolChars = "!@#$%^&*()_+[]{}|;:,.<>?";
            
            let allChars = "";
            if (includeLower) allChars += lowerChars;
            if (includeUpper) allChars += upperChars;
            if (includeNumbers) allChars += numberChars;
            if (includeSymbols) allChars += symbolChars;
            
            if (allChars === "") {
                document.getElementById("password").textContent = "Select at least one option";
                return;
            }
            
            let password = "";
            for (let i = 0; i < length; i++) {
                const randomIndex = Math.floor(Math.random() * allChars.length);
                password += allChars[randomIndex];
            }
            
            document.getElementById("password").textContent = password;
        }
        
        function copyPassword() {
            const password = document.getElementById("password").textContent;
            if (password) {
                navigator.clipboard.writeText(password);
                alert("Password copied to clipboard!");
            }
        }
    </script>
</body>
</html>
