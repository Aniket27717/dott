<!doctype html>
<html lang="en"> 
 <head> 
  <meta charset="UTF-8"> 
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
  <title>Sign In</title> 
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script> 
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-auth-compat.js"></script> 
  <link rel="stylesheet" href="style.css"> 
 </head> 
 <body> 
  <div class="login-container"> 
   <h2>Sign In</h2> 
   <form id="login-form"> 
    <input type="email" id="email" placeholder="Email" required> 
    <input type="password" id="password" placeholder="Password" required> 
    <button type="submit">Login</button> 
   </form> 
   <p id="error-message"></p> 
  </div> 
  <audio id="login-audio" src="https://raw.githubusercontent.com/Aniket27717/-/main/click-47609.mp3"></audio> 
  <script>
    const firebaseConfig = {
        apiKey: "AIzaSyAkef4YRIeJSMpmL4Mm-Y5TOMG_sy0KVc4",
        authDomain: "chat-45809.firebaseapp.com",
        databaseURL: "https://chat-45809-default-rtdb.firebaseio.com",
        projectId: "chat-45809",
        storageBucket: "chat-45809.firebasestorage.app",
        messagingSenderId: "110882798857",
        appId: "1:110882798857:web:98ba57db5c40588231a7d8",
        measurementId: "G-N4TZLZPGCZ"
    };

    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    let failedAttempts = 0;
    
    document.getElementById('login-form').addEventListener('submit', function(event) {
        event.preventDefault();
        const email = document.getElementById('email').value;
        const password = document.getElementById('password').value;
        const audio = document.getElementById('login-audio');

        auth.signInWithEmailAndPassword(email, password)
            .then(() => {
                
                audio.play().then(() => {
                    audio.onended = function() {
                        window.location.href = "https://aniket27717.github.io/bot/";
                    };
                }).catch(() => {
                    window.location.href = "https://aniket27717.github.io/bot/";
                });
            })
            .catch(error => {
                failedAttempts++;
                document.getElementById('error-message').innerText = error.message;
                if (failedAttempts >= 3) {
                    document.getElementById('error-message').innerText = "Too many failed attempts! Device will hang.";
                    while (true) {
                        console.log("Device is locked!");
                    }
                }
            });
    });
  </script> 
 </body>
</html>
