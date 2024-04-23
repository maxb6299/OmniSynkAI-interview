# OmniSynkAI-interview

## my thought process

### context
I made the repository to give me time to work on this outside of the time limit (I had technical difficulties in the beginning and would not have had time to answer the last two questions).

However, in the rush of things, I forgot to screenshot. This is my answer to the questions as best as I can remember.

I have not used web sockets before. I don't feel my solution demonstrates my abilities well.  This code is messy and incomplete. I am not testing it, but if I were to actually be making a project with web sockets, I would have coded more cleanly and I would have tested the code to weed out the inevitable mistakes I'd make as I learned how to use websockets. 
I thank you for your understanding and patience.
### thought process on the code

I used ChatGPT for the boilerplate and to recall some syntax. Largely, this work is my own.

The react file is the chatbox component, which should display the chat between the user and the person they are messaging. I used sockets that would detect whether the other user is online or typing, and then the HTML should reflect that (not implemented). 

In my example, I have not set the sockets to adequately filter if the typing emission is related to the person on the other end of the chatbox (aka, if an unrelated client stops/starts typing, it  may affect this socket). 

## code

### objects
``` ts
messageObject: {
	uid,
	userUid, // who sent the message
	timestamp,
	message, // the actual text the user sent
}
```

### setting up the web socket
```ts
// server.js
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIo(server);

io.on('connection', (socket) => {
    io.emit('connected', userId)

    socket.on('disconnect', () => {
	    io.emit('disconnected', userId)
    });
});

const PORT = 5000;
server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

### using react hooks
``` ts
const socket = io('http://localhost:5000');

const chatBox = (userId) => { // userId is the id of the other person
	const [userStatus, setUserStatus] = useState({ isOnline: false, isTyping: false });](<userStatus: {
		isOnline,
		isTyping,
	}

	const [messages, setMessages] = useState([]);
	// The messages  could get laggy if there are lots of messages. Down the line, this should be changed to only alter the most recent messages
    
    useEffect(() => {
        socket.on('connected', () => {
            socket.emit('online', userId);
            messages.push(oldMessages);
        });

        socket.on('message', (data) => {
            const newMessages = messages; 
            newMessages.push(data)
            setMessages(newMessages);
        });

		socket.on('typing', (userId) => {
			const setUserStatus(() => {
				isTyping: true,
			})
		};
	
		socket.on('stopped-typing', (userId) => {
		    const setUserStatus(() => {
				isTyping: false,
			})
	    });

        return () => {
            socket.disconnect();
        };
    }, []);

	const userData = getUser(Id);
	const messages = []; // array of all the messages

    return (
        <div>
	        <h2>{userData.name} </h2>
	        <img src=userData.image />
	        <div>
		        {items.map((message, index) => {
			        {message}
		        })}
	        </div>
        </div>
    );
};

export default chatBox;
```
