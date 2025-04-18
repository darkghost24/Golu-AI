<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Golu - Your Cute Assistant 💕</title>
  <style>
    :root {
      --primary-color: #FF4081;
      --secondary-color: #FF80AB;
      --background-color: #FFEBEE;
      --text-color: #333;
      --card-color: #FFF3F3;
    }

    body {
      font-family: 'Comic Sans MS', 'Segoe UI', sans-serif;
      background: var(--background-color);
      color: var(--text-color);
      text-align: center;
      margin: 0;
      padding: 20px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    h1 {
      font-size: 2.5em;
      color: var(--primary-color);
      margin-bottom: 20px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
    }

    .container {
      max-width: 800px;
      width: 90%;
      margin: 0 auto;
    }

    button {
      padding: 15px 30px;
      font-size: 18px;
      border: none;
      border-radius: 30px;
      background-color: var(--secondary-color);
      color: white;
      cursor: pointer;
      margin: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      transition: all 0.3s ease;
      font-weight: bold;
    }

    button:hover {
      background-color: var(--primary-color);
      transform: scale(1.05);
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
    }

    button:disabled {
      background-color: #ccc;
      cursor: not-allowed;
      transform: none;
    }

    #output {
      margin-top: 20px;
      font-size: 20px;
      color: var(--primary-color);
      font-weight: bold;
      padding: 20px;
      border-radius: 15px;
      background-color: var(--card-color);
      border: 2px solid var(--secondary-color);
      min-height: 80px;
      width: 90%;
      margin: 20px auto;
      overflow-y: auto;
      white-space: pre-wrap;
      text-align: left;
      box-shadow: inset 0 0 10px rgba(0,0,0,0.05);
    }

    #output a {
      color: #d63384;
      text-decoration: underline;
      font-weight: bold;
    }

    #textInput {
      padding: 12px 15px;
      font-size: 16px;
      width: 70%;
      border: 2px solid var(--secondary-color);
      border-radius: 12px;
      margin: 10px 0;
      background-color: var(--card-color);
      transition: all 0.3s ease;
    }

    #textInput:focus {
      border-color: var(--primary-color);
      outline: none;
      box-shadow: 0 0 5px rgba(255, 64, 129, 0.5);
    }

    .input-group {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 100%;
      margin: 15px 0;
    }

    .button-group {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }

    #golu-avatar {
      margin: 20px auto;
      width: 200px;
      height: 260px;
      position: relative;
      animation: float 3s ease-in-out infinite;
    }

    .head {
      width: 150px;
      height: 150px;
      background: #ffc1e3;
      border-radius: 50%;
      position: relative;
      margin: auto;
      box-shadow: 0 4px 15px rgba(0,0,0,0.15);
    }

    .eye {
      width: 20px;
      height: 20px;
      background: black;
      border-radius: 50%;
      position: absolute;
      top: 45px;
      animation: blink 5s infinite;
    }

    .left-eye { left: 35px; }
    .right-eye { right: 35px; }

    @keyframes blink {
      0%, 95%, 100% { transform: scaleY(1); }
      96%, 97%, 98%, 99% { transform: scaleY(0.1); }
    }

    .mouth {
      width: 40px;
      height: 20px;
      border-bottom: 5px solid #d63384;
      position: absolute;
      bottom: 30px;
      left: 50%;
      transform: translateX(-50%);
      border-radius: 50%;
      transition: all 0.3s ease;
    }

    .body {
      position: relative;
      top: -10px;
      width: 100%;
      height: 100px;
    }

    .hand {
      width: 30px;
      height: 60px;
      background-color: #ffc1e3;
      border-radius: 50%;
      position: absolute;
      top: 0;
    }

    .wave-hand {
      left: -20px;
      transform-origin: top right;
      animation: wave 2.5s infinite ease-in-out;
    }

    .other-hand {
      right: -20px;
    }

    @keyframes wave {
      0%, 100% { transform: rotate(0deg); }
      30% { transform: rotate(-25deg); }
      60% { transform: rotate(10deg); }
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-8px); }
    }

    .listening #golu-avatar .mouth {
      height: 10px;
      width: 60px;
      border-radius: 5px;
      background: #d63384;
      border-bottom: none;
    }

    .typing #golu-avatar .mouth {
      height: 5px;
      width: 30px;
      border-radius: 5px;
      background: #d63384;
      border-bottom: none;
    }

    .status-indicator {
      margin: 10px 0;
      font-size: 14px;
      color: #666;
    }

    .command-history {
      width: 90%;
      margin: 20px auto;
      max-height: 150px;
      overflow-y: auto;
      background: white;
      border-radius: 10px;
      padding: 10px;
      box-shadow: inset 0 0 5px rgba(0,0,0,0.1);
      text-align: left;
    }

    .command-item {
      padding: 5px;
      border-bottom: 1px solid #eee;
      cursor: pointer;
    }

    .command-item:hover {
      background: #f5f5f5;
    }

    @media (max-width: 600px) {
      h1 {
        font-size: 2em;
      }
      
      #textInput {
        width: 90%;
      }
      
      button {
        padding: 12px 20px;
        font-size: 16px;
      }
      
      #output {
        font-size: 18px;
        padding: 15px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Golu - Your Cute Assistant</h1>

    <div id="golu-avatar">
      <div class="head">
        <div class="eye left-eye"></div>
        <div class="eye right-eye"></div>
        <div class="mouth"></div>
      </div>
      <div class="body">
        <div class="hand wave-hand"></div>
        <div class="hand other-hand"></div>
      </div>
    </div>

    <div class="status-indicator" id="status">Ready</div>

    <div class="button-group">
      <button onclick="startListening()" id="micButton">🎤 Speak</button>
      <button onclick="stopListening()" id="stopButton" disabled>✋ Stop</button>
    </div>

    <div class="input-group">
      <input type="text" id="textInput" placeholder="Type your message here... ✍️" 
             onkeypress="handleKeyPress(event)">
      <div class="button-group">
        <button onclick="sendText()">Send 💬</button>
        <button onclick="clearConversation()">Clear 🗑️</button>
      </div>
    </div>

    <div id="output"></div>

    <div class="command-history" id="commandHistory">
      <div>Recent commands will appear here</div>
    </div>
  </div>

  <script>
    // DOM Elements
    const output = document.getElementById('output');
    const textInput = document.getElementById('textInput');
    const statusElement = document.getElementById('status');
    const commandHistory = document.getElementById('commandHistory');
    const micButton = document.getElementById('micButton');
    const stopButton = document.getElementById('stopButton');
    
    // Speech Recognition Setup
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    const recognition = new SpeechRecognition();
    recognition.lang = 'en-US';
    recognition.interimResults = false;
    recognition.continuous = false;

    // App State
    let currentLanguage = "en"; // en, hi, bn
    let availableVoices = [];
    let conversationHistory = [];
    let isListening = false;

    // Initialize the app
    window.onload = () => {
      // Load voices
      speechSynthesis.onvoiceschanged = () => {
        availableVoices = speechSynthesis.getVoices();
      };
      
      // Try to get voices immediately (some browsers don't fire the event)
      availableVoices = speechSynthesis.getVoices();
      
      // Load conversation history from localStorage
      loadHistory();
      
      // Greet the user
      greetUser();
      
      // Add event listeners
      textInput.addEventListener('focus', () => {
        document.body.classList.add('typing');
      });
      
      textInput.addEventListener('blur', () => {
        document.body.classList.remove('typing');
      });
    };

    // Voice Recognition Functions
    function startListening() {
      if (isListening) return;
      
      isListening = true;
      micButton.disabled = true;
      stopButton.disabled = false;
      statusElement.textContent = "Listening...";
      output.textContent = "Listening...";
      document.body.classList.add('listening');
      
      recognition.start();
    }

    function stopListening() {
      if (!isListening) return;
      
      isListening = false;
      recognition.stop();
      micButton.disabled = false;
      stopButton.disabled = true;
      statusElement.textContent = "Ready";
      document.body.classList.remove('listening');
    }

    recognition.onresult = (event) => {
      const transcript = event.results[0][0].transcript;
      addToHistory(transcript);
      outputTextWithTypingEffect("You said: " + transcript);
      respond(transcript);
      stopListening();
    };

    recognition.onerror = (event) => {
      output.textContent = "Error occurred: " + event.error;
      stopListening();
    };

    recognition.onend = () => {
      if (isListening) {
        recognition.start(); // Continue listening if not manually stopped
      }
    };

    // Text Input Functions
    function sendText() {
      const input = textInput.value.trim();
      if (input) {
        addToHistory(input);
        outputTextWithTypingEffect("You typed: " + input);
        respond(input);
        textInput.value = "";
      }
    }

    function handleKeyPress(event) {
      if (event.key === 'Enter') {
        sendText();
      }
    }

    // Conversation Functions
    function greetUser() {
      const hour = new Date().getHours();
      let greeting = "Hello! I'm Golu, your assistant. How can I help you today?";
      if (hour >= 5 && hour < 12) greeting = "Good morning! I'm Golu, your assistant. What can I do for you today?";
      else if (hour >= 12 && hour < 17) greeting = "Good afternoon! I'm Golu, your assistant. How can I assist you?";
      else if (hour >= 17 && hour < 21) greeting = "Good evening! I'm Golu, your assistant. What do you need help with?";
      else greeting = "Hello night owl! I'm Golu, your assistant. What brings you here so late?";
      
      outputTextWithTypingEffect(greeting);
      speak(greeting);
    }

    function respond(message) {
      let response = getResponseForMessage(message.toLowerCase());
      
      // If we have a response, use it
      if (response) {
        if (response.action) {
          response.action();
        }
        if (response.text) {
          outputTextWithTypingEffect(response.text);
          speak(response.text);
        }
        return;
      }
      
      // Default response if no match found
      const defaultResponse = currentLanguage === "hi" ? 
        "माफ कीजिए, मैं समझ नहीं पाया। क्या आप दोबारा कह सकते हैं?" :
        currentLanguage === "bn" ? 
        "দুঃখিত, আমি বুঝতে পারিনি। আপনি আবার বলতে পারেন?" :
        "Sorry, I didn't understand that. Could you try again?";
      
      outputTextWithTypingEffect(defaultResponse);
      speak(defaultResponse);
    }

    function getResponseForMessage(message) {
      // Website opening
      const websites = {
        "youtube": {url: "https://www.youtube.com", name: "YouTube"},
        "facebook": {url: "https://www.facebook.com", name: "Facebook"},
        "instagram": {url: "https://www.instagram.com", name: "Instagram"},
        "whatsapp": {url: "https://web.whatsapp.com", name: "WhatsApp"},
        "gmail": {url: "https://mail.google.com", name: "Gmail"},
        "google": {url: "https://www.google.com", name: "Google"},
        "twitter": {url: "https://twitter.com", name: "Twitter"},
        "netflix": {url: "https://www.netflix.com", name: "Netflix"},
        "amazon": {url: "https://www.amazon.com", name: "Amazon"},
        "wikipedia": {url: "https://www.wikipedia.org", name: "Wikipedia"}
      };

      for (let site in websites) {
        if (message.includes("open " + site)) {
          const siteInfo = websites[site];
          return {
            text: currentLanguage === "hi" ? `${siteInfo.name} खोल रहा हूँ...` :
                  currentLanguage === "bn" ? `${siteInfo.name} খুলছি...` :
                  `Opening ${siteInfo.name}...`,
            action: () => window.open(siteInfo.url, "_blank")
          };
        }
      }

      // Wikipedia lookup
      if (message.startsWith("who is") || message.startsWith("what is") || 
          message.startsWith("tell me about")) {
        const topic = message.replace("who is", "")
                            .replace("what is", "")
                            .replace("tell me about", "")
                            .trim();
        return {
          text: currentLanguage === "hi" ? `मैं ${topic} के बारे में जानकारी ढूंढ रहा हूँ...` :
                currentLanguage === "bn" ? `আমি ${topic} সম্পর্কে তথ্য খুঁজছি...` :
                `Looking up information about ${topic}...`,
          action: () => fetchWikipedia(topic)
        };
      }

      // Google search
      if (message.includes("search") || message.includes("google")) {
        let query = message.replace("search", "")
                           .replace("in google", "")
                           .replace("google", "")
                           .trim();
        if (query) {
          return {
            text: currentLanguage === "hi" ? `"${query}" को Google पर खोज रहा हूँ...` :
                  currentLanguage === "bn" ? `"${query}" গুগলে খুঁজছি...` :
                  `Searching for "${query}" on Google...`,
            action: () => window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`, "_blank")
          };
        }
      }

      // Play music/video
      if (message.includes("play")) {
        const query = message.replace("play", "")
                             .replace("song", "")
                             .replace("music", "")
                             .replace("video", "")
                             .trim();
        if (query) {
          return {
            text: currentLanguage === "hi" ? `"${query}" चला रहा हूँ YouTube पर...` :
                  currentLanguage === "bn" ? `"${query}" ইউটিউবে চালাচ্ছি...` :
                  `Playing "${query}" on YouTube...`,
            action: () => window.open(`https://www.youtube.com/results?search_query=${encodeURIComponent(query)}`, "_blank")
          };
        }
      }

      // Language switching
      if (message.includes("speak in bengali") || message.includes("speak bengali") || 
          message.includes("বাংলা")) {
        currentLanguage = "bn";
        return {
          text: "ভাষা বাংলা করা হয়েছে। এখন আমি বাংলায় কথা বলব।",
          action: () => speak("ভাষা বাংলা করা হয়েছে। এখন আমি বাংলায় কথা বলব।")
        };
      }
      
      if (message.includes("speak in hindi") || message.includes("speak hindi") || 
          message.includes("हिंदी")) {
        currentLanguage = "hi";
        return {
          text: "अब मैं हिंदी में बोलूंगा।",
          action: () => speak("अब मैं हिंदी में बोलूंगा।")
        };
      }
      
      if (message.includes("speak in english") || message.includes("speak english")) {
        currentLanguage = "en";
        return {
          text: "Language changed to English.",
          action: () => speak("Language changed to English.")
        };
      }

      // Math calculations
      if (/(\d+|\w+)\s?(plus|minus|times|multiplied by|divided by|over)\s?(\d+|\w+)/.test(message)) {
        const result = solveMath(message);
        if (result !== null) {
          return {
            text: currentLanguage === "bn" ? `উত্তর হল ${result}।` :
                  currentLanguage === "hi" ? `उत्तर है ${result}।` :
                  `The answer is ${result}.`
          };
        } else {
          return {
            text: currentLanguage === "bn" ? "এই অঙ্কটা একটু কঠিন। আবার বলো।" :
                  currentLanguage === "hi" ? "यह गणित थोड़ा कठिन है। कृपया फिर से पूछें।" :
                  "Hmm, that math looks tricky. Can you try again?"
          };
        }
      }

      // Time/date
      if (message.includes("time") || message.includes("date") || message.includes("today")) {
        const now = new Date();
        const time = now.toLocaleTimeString();
        const date = now.toLocaleDateString();
        return {
          text: currentLanguage === "hi" ? `आज की तारीख ${date} है और समय ${time} है।` :
                currentLanguage === "bn" ? `আজকের তারিখ ${date} এবং সময় ${time}।` :
                `Today is ${date}, and the current time is ${time}.`
        };
      }

      // Greetings
      if (message.includes("hello") || message.includes("hi") || message.includes("hey")) {
        return {
          text: currentLanguage === "hi" ? "हैलो! मैं गोलू हूँ। आपकी क्या मदद कर सकता हूँ?" :
                currentLanguage === "bn" ? "হ্যালো! আমি গোলু। আমি আপনাকে কিভাবে সাহায্য করতে পারি?" :
                "Hello! I'm Golu. How can I help you today?"
        };
      }

      // Self introduction
      if (message.includes("who are you") || message.includes("your name") || 
          message.includes("introduce yourself") || message.includes("about you")) {
        return {
          text: currentLanguage === "hi" ? "मेरा नाम गोलू है। मैं आपकी मदद के लिए यहाँ हूँ!" :
                currentLanguage === "bn" ? "আমার নাম গোলু। আমি তোমার সাহায্য করতে এখানে আছি!" :
                "My name is Golu. I'm here to help you with anything you need!"
        };
      }

      // Goodbye
      if (message.includes("good night") || message.includes("bye") || message.includes("goodbye")) {
        return {
          text: currentLanguage === "hi" ? "अलविदा! अपना ख्याल रखना!" :
                currentLanguage === "bn" ? "বিদায়! ভালো থেকো!" :
                "Goodbye! Have a wonderful day!",
          action: () => {
            speak(currentLanguage === "hi" ? "अलविदा! अपना ख्याल रखना!" :
                  currentLanguage === "bn" ? "বিদায়! ভালো থেকো!" :
                  "Goodbye! Have a wonderful day!");
            recognition.stop();
          }
        };
      }

      // Say hello to someone
      if (message.includes("say hello to")) {
        let name = "";
        if (message.includes("say hello to my friend")) {
          name = message.split("say hello to my friend")[1]?.trim();
        } else if (message.includes("say hello to mr")) {
          name = "Mr. " + message.split("say hello to mr")[1]?.trim();
        } else if (message.includes("say hello to ms")) {
          name = "Ms. " + message.split("say hello to ms")[1]?.trim();
        } else if (message.includes("say hello to mrs")) {
          name = "Mrs. " + message.split("say hello to mrs")[1]?.trim();
        } else {
          name = message.split("say hello to")[1]?.trim();
        }

        if (!name && (message.includes("all my friends") || message.includes("everyone"))) {
          return {
            text: currentLanguage === "hi" ? "नमस्ते दोस्तों! 😊" :
                  currentLanguage === "bn" ? "হ্যালো বন্ধুরা! 😊" :
                  "Hello everyone! 👋"
          };
        }

        if (name) {
          return {
            text: currentLanguage === "hi" ? `नमस्ते ${name} जी! 😊` :
                  currentLanguage === "bn" ? `হ্যালো ${name}! 😊` :
                  `Hello ${name}! 👋`
          };
        }
      }

      return null; // No response found
    }

    function fetchWikipedia(topic) {
      const url = `https://en.wikipedia.org/wiki/${encodeURIComponent(topic)}`;
      fetch(`https://en.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(topic)}`)
        .then(res => res.json())
        .then(data => {
          if (data.extract) {
            const maxLength = 400;
            const shortText = data.extract.length > maxLength
              ? data.extract.substring(0, maxLength) + "..."
              : data.extract;
            const response = `${shortText}\n\n👉 <a href="${url}" target="_blank">Click here to read more</a>`;
            output.innerHTML = response.replace(/\n/g, "<br>");
            speak(shortText);
          } else {
            const response = currentLanguage === "hi" ? 
              "माफ कीजिए, मैं इस विषय पर जानकारी नहीं ढूंढ पाया।" :
              currentLanguage === "bn" ? 
              "দুঃখিত, আমি এই বিষয়ে তথ্য খুঁজে পাইনি।" :
              "Sorry, I couldn't find information about that.";
            outputTextWithTypingEffect(response);
            speak(response);
          }
        })
        .catch(() => {
          const response = currentLanguage === "hi" ? 
            "जानकारी प्राप्त करते समय कोई समस्या आई।" :
            currentLanguage === "bn" ? 
            "তথ্য পাওয়ার সময় একটি সমস্যা হয়েছে।" :
            "Something went wrong while fetching the information.";
          outputTextWithTypingEffect(response);
          speak(response);
        });
    }

    function solveMath(message) {
      message = message.replace("what is", "")
                      .replace("calculate", "")
                      .replace("solve", "")
                      .trim();
      const numberWords = {
        "plus": "+", "add": "+", "and": "+", "sum": "+",
        "minus": "-", "subtract": "-", "remove": "-",
        "times": "*", "multiplied by": "*", "multiply": "*", "product": "*",
        "divided by": "/", "over": "/", "divide": "/", "quotient": "/",
        "one": 1, "two": 2, "three": 3, "four": 4, "five": 5,
        "six": 6, "seven": 7, "eight": 8, "nine": 9, "zero": 0,
        "ten": 10, "twenty": 20, "thirty": 30, "forty": 40, "fifty": 50,
        "sixty": 60, "seventy": 70, "eighty": 80, "ninety": 90,
        "hundred": 100, "thousand": 1000
      };
      
      Object.keys(numberWords).forEach(word => {
        const regex = new RegExp("\\b" + word + "\\b", "gi");
        message = message.replace(regex, numberWords[word]);
      });
      
      try {
        // Safety check - only allow basic math operations
        if (/^[\d+\-*/. ]+$/.test(message)) {
          return eval(message);
        }
        return null;
      } catch {
        return null;
      }
    }

    // UI Functions
    function outputTextWithTypingEffect(text) {
      output.innerHTML = "";
      let i = 0;
      document.body.classList.add('typing');
      
      const interval = setInterval(() => {
        if (i < text.length) {
          output.innerHTML += text.charAt(i);
          i++;
        } else {
          clearInterval(interval);
          document.body.classList.remove('typing');
        }
      }, 30);
    }

    // Speech Functions
    function speak(text) {
      const synth = window.speechSynthesis;
      
      // Cancel any ongoing speech
      synth.cancel();
      
      const utter = new SpeechSynthesisUtterance(text.replace(/[\u{1F600}-\u{1F6FF}]/gu, ""));
      
      // Set language based on current setting
      if (currentLanguage === "hi") {
        utter.lang = "hi-IN";
        utter.rate = 1.0;
      } else if (currentLanguage === "bn") {
        utter.lang = "bn-IN";
        utter.rate = 1.0;
      } else {
        utter.lang = "en-US";
        utter.rate = 1.1;
      }
      
      utter.pitch = 1.5;
      
      // Try to find a suitable voice
      const voice = availableVoices.find(v => 
        v.lang.toLowerCase().includes(utter.lang.toLowerCase()) && 
        (v.name.toLowerCase().includes("child") || v.name.toLowerCase().includes("female"))
      ) || availableVoices.find(v => v.lang.toLowerCase().includes(utter.lang.toLowerCase()));
      
      if (voice) {
        utter.voice = voice;
      }
      
      synth.speak(utter);
    }

    // History Functions
    function addToHistory(command) {
      conversationHistory.unshift({
        command: command,
        timestamp: new Date().toLocaleString()
      });
      
      // Keep only the last 10 commands
      if (conversationHistory.length > 10) {
        conversationHistory.pop();
      }
      
      updateHistoryDisplay();
      saveHistory();
    }

    function updateHistoryDisplay() {
      if (conversationHistory.length === 0) {
        commandHistory.innerHTML = "<div>No commands yet</div>";
        return;
      }
      
      commandHistory.innerHTML = conversationHistory
        .map(item => `<div class="command-item" onclick="useHistoryItem('${escapeHtml(item.command)}')">
          <strong>${escapeHtml(item.command)}</strong>
          <small>${item.timestamp}</small>
        </div>`)
        .join("");
    }

    function useHistoryItem(command) {
      textInput.value = command;
      textInput.focus();
    }

    function clearConversation() {
      output.textContent = "";
      conversationHistory = [];
      updateHistoryDisplay();
      saveHistory();
    }

    function saveHistory() {
      localStorage.setItem('goluHistory', JSON.stringify(conversationHistory));
    }

    function loadHistory() {
      const saved = localStorage.getItem('goluHistory');
      if (saved) {
        conversationHistory = JSON.parse(saved);
        updateHistoryDisplay();
      }
    }

    // Utility function to escape HTML
    function escapeHtml(unsafe) {
      return unsafe
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
    }
  </script>
</body>
</html>
