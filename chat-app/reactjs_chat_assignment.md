# React chat app

import React, { useState } from 'react';

const user_list = ["Alan", "Bob", "Carol", "Dean", "Elin"];

const ChatApp = () => {
  const [message, setMessage] = useState('');
  const [chats, setChats] = useState([]);

  const handleSendMessage = () => {
    if (message.trim() !== '') {
      const randomUser = user_list[Math.floor(Math.random() * user_list.length)];
      const newChat = {
        user: randomUser,
        message: message,
        likes: 0
      };

      setChats([...chats, newChat]);
      setMessage('');
    }
  };

  const handleLike = (index) => {
    const updatedChats = [...chats];
    updatedChats[index].likes++;
    setChats(updatedChats);
  };

  return (
    <div>
      <div>
        {chats.map((chat, index) => (
          <div key={index}>
            <span>{chat.user}: {chat.message}</span>
            <button onClick={() => handleLike(index)}>
              Like ({chat.likes})
            </button>
          </div>
        ))}
      </div>
      <div>
        <input
          type="text"
          value={message}
          onChange={(e) => setMessage(e.target.value)}
        />
        <button onClick={handleSendMessage}>Send</button>
      </div>
    </div>
  );
};

export default ChatApp;
