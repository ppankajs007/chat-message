## connect with socket io on live server
   # Server file
      const express = require('express');
      const fs = require('fs');
      const https = require('https');
      const socketIo = require('socket.io');
      const app = express();
      
      const options = {
        key: fs.readFileSync('private_key.txt'),
        cert: fs.readFileSync('CRT_key.txt')
      };
      
      const server = https.createServer(options, app);
      
      //const server = https.createServer(app);
      
      const io = socketIo(server);
      
      io.on('connection', (socket) => {
       
        socket.on('chat message', (message) => {
            console.log( message )
            io.emit('chat message', message); // Broadcast the message to all connected clients
        });
        socket.on('disconnect', () => {
          console.log('User disconnected');
        });
      });
      
      server.listen(3000, () => {
        console.log('Server listening on port 3000');
      });

# javascript messagfe append

    let audio = new Audio(`<?= base_url('public/chat-tone.mp3') ?>`);
    audio.muted = true;

    let socketFooter = io.connect( `<?= WS_HOST ?>`,{ transports: ['websocket']  } );
    let receiver_id = `<?= $this->session->userdata('id'); ?>`

    socketFooter.on('chat message', function (msg) { 
        let jsonMessage = JSON.parse(msg);
        if( typeof jsonMessage.msg !== 'undefined' && receiver_id == jsonMessage.receiver_id ){
            Notification.requestPermission().then(function(permission) {
                new Notification(jsonMessage.name, { body: jsonMessage.msg });
            });
            
            setTimeout(function(){
                let countMsg = `<?= getUnredMessage() ?>`;
                console.log('countMsg', countMsg  )
                $('.headerMessages').children('.icon-button').remove('icon-button__badge');
                let count = `<span class='icon-button__badge'>${countMsg}</span>`;
                $('.headerMessages').children('.icon-button').append(count);
            },2000);
            audio.play()
            .then(() => { audio.muted = false; })
            .catch(error => { console.error('Failed to play audio:', error); });
        }
    })

    (ii)
       const messanger_url = `<?= base_url('messanger') ?>`
       let socket = io.connect( `<?= WS_HOST ?>`,{ transports: ['websocket']  } );
       
       socket.on('connect', () => {
           //console.log('socket => ', socket );   
       })
      

    
