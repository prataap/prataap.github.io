### An example of a React based UI for a custom chat interface to interact with a bot.

This code adds logic to the React component to handle form submissions and send messages to the Telegram bot. 
It uses the fetch API to send a POST request to the /api/send-message endpoint, with the user's message as the request body. 
The bot's response is then added to the messages array, which is used to render the chat messages on the screen.


```javascript
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  // Use state to store the user's messages and the bot's responses
  const [messages, setMessages] = useState([]);

  // Create a ref for the messages container
  const messagesRef = React.createRef();

  // Handle form submission
  const handleSubmit = event => {
    event.preventDefault();

    // Get the user's message from the input field
    const message = event.target.elements.message.value;

    // Send the message to the Telegram bot
    sendMessage(message);

    // Clear the input field
    event.target.elements.message.value = "";
  };

  // Send a message to the Telegram bot and update the messages array
  const sendMessage = message => {
    // Add the user's message to the messages array
    setMessages(messages.concat({
      type: "user",
      text: message
    }));

    // Send the user's message to the Telegram bot and get the response
    fetch("/api/send-message", {
      method: "POST",
      body: JSON.stringify({
        message
      })
    })
    .then(response => response.json())
    .then(data => {
      // Add the bot's response to the messages array
      setMessages(messages.concat({
        type: "bot",
        text: data.response
      }));
    });
  };

  // Scroll the messages container to the bottom
  const scrollToBottom = () => {
    messagesRef.current.scrollTo(0, messagesRef.current.scrollHeight);
  };

  // Use the useEffect hook to scroll the messages container to the bottom
  // whenever the messages array is updated
  useEffect(scrollToBottom, [messages]);

  return (
    <div className="app">
      <header>
        <h1>Bookstore Bot</h1>
      </header>
      <main>
        <div className="messages" ref={messagesRef}>
          {messages.map((message, index) => (
            <div className={`message ${message.type}`} key={index}>
              {message.text}
            </div>
          ))}
        </div>
        <form className="input-form" onSubmit={handleSubmit}>
          <input
            type="text"
            placeholder="Enter your message..."
            name="message"
            onKeyDown={event => {
              if (event.key === "Enter") {
                sendMessage(event.target.value);
                event.target.value = "";
              }
            }}
          />
          <button>Send</button>
        </form>
      </main>
    </div>
```

- Create a file called App.css to customize the look and feel of the chat interface, such as the font, colors, and layout. For example:

```css
.app {
  font-family: sans-serif;
  text-align: center;
  width: 400px;
  margin: 0 auto;
}

.app header {
  background-color: #333;
  color: white;
  padding: 20px;
}

.app main {
  background-color: #f5f5f5;
  padding: 20px;
}

.app .messages {
  height: 200px;
  overflow-y: scroll;
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 20px;
}

.app .input-form {
  display: flex;
  align-items: center;
}

.app .input-form input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  margin-right: 10px;
}

.app .input-form button {
  padding: 10px;
  background-color: #333;
  color: white;
  border: none;
  cursor: pointer;
}

.app .message {
  margin-bottom: 10px;
  padding: 10px;
  background-color: #fff;
  border-radius: 5px;
}

.app .message.bot {
  background-color: #f0f0f0;
  text-align: left;
}

.app .message.user {
  background-color: #333;
  color: white;
  text-align: right;
}
```


