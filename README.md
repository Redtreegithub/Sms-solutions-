# Sms-solutions-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bulk SMS Sender</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Bulk SMS Sender</h1>
        <textarea id="message" placeholder="Enter your message..."></textarea>
        <button id="sendButton">Send SMS</button>
        <div id="response"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

.container {
    max-width: 600px;
    margin: 50px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

h1 {
    text-align: center;
}

textarea {
    width: 100%;
    height: 100px;
    margin-bottom: 10px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

#response {
    margin-top: 20px;
}
document.getElementById('sendButton').addEventListener('click', function() {
    var message = document.getElementById('message').value;

    // Send the message to the server
    fetch('/send-sms', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ message: message })
    })
    .then(response => response.json())
    .then(data => {
        document.getElementById('response').textContent = data.message;
    })
    .catch(error => {
        console.error('Error:', error);
    });
});
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

app.use(bodyParser.json());

app.post('/send-sms', (req, res) => {
    const message = req.body.message;
    // Replace this with code to send SMS using a bulk SMS service provider
    // For example, using Twilio or Nexmo APIs
    console.log('Sending SMS:', message);
    res.json({ message: 'SMS sent successfully' });
});

app.use(express.static('public'));

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});

