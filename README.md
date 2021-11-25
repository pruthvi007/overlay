<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" class="no-js">

<head>
    <title>PHH</title>
    <style>
        body {
            background-image: url(phh.PNG);
            background-size: cover;
            /* <------ */
        }
        
        .chat-overlay {
            position: fixed;
            width: 376px;
            height: 500px;
            bottom: 24px;
            right: 24px;
            z-index: 90;
        }
        
        .chat-overlay-open {
            height: 512px;
        }
        
        .chat-overlay-closed {
            height: 78px;
        }
        
        .chat-overlay-wrapper {
            width: 376px;
            height: 448px;
        }
        
        .chat-overlay-header-mobile {
            display: none;
        }
        
        .chat-overlay-header {
            position: relative;
            height: 56px;
            width: 56px;
            margin-left: auto;
            border-radius: 50%;
            box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
        }
        
        #receiver {
            transition: opacity 1s ease-in-out;
            opacity: 1;
            background: rgba(0, 0, 0, 0.5);
            box-shadow: 1rem 1rem 5rem rgba(0, 0, 0, 0.5);
            /* border-radius: 0.5rem; */
        }
        
        #receiver.close {
            height: 0;
            opacity: 0;
            overflow: hidden;
        }
        
        #receiver.open {
            height: 100%;
            opacity: 1;
            overflow: hidden;
        }
        
        .chat-overlay-header-img {
            position: absolute;
            max-width: 56px;
            max-height: 56px;
            transition: opacity 1s ease-in-out;
            opacity: 1;
            right: 0px;
            left: 0px;
            top: 0px;
            bottom: 0px;
            margin: auto;
        }
        
        .chat-overlay-header-img.open {
            opacity: 0;
        }
        
        .absolute-cart-box {
            display: none;
        }
        
        @media only screen and (max-width: 768px) {
            .chat-overlay {
                width: 100%;
                position: fixed;
                height: 100%;
            }
            .chat-overlay-header-mobile {
                display: flex;
                width: inherit;
                height: 9%;
                background: #4d5aff;
            }
            .chat-overlay-header-mobile img {
                height: 30%;
                padding: 1rem;
                margin-left: auto;
            }
            .chat-overlay-header-mobile.close {
                display: none;
            }
            #receiver {
                border-radius: 0;
            }
            #receiver.close {
                height: 0;
                opacity: 0;
                overflow: hidden;
            }
            #receiver.open {
                height: 91%;
                opacity: 1;
                overflow: hidden;
            }
            .chat-overlay-open {
                height: 100%;
                bottom: 0px;
                right: 0px;
            }
            .chat-overlay-closed {
                height: 70px;
                bottom: 24px;
                right: 24px;
            }
            .chat-overlay-wrapper {
                width: 100%;
                height: 100%;
            }
        }
    </style>
</head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<link href='https://fonts.googleapis.com/css?family=Droid+Sans:400,700|Droid+Serif' rel='stylesheet'>
<link href="https://fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">

<body>
    <div class="chat-overlay">
        <div class="chat-overlay-wrapper">
            <div class="chat-overlay-header-mobile">
                <img class="close" src="./amelia-close.png" alt="toggle chat overlay" />
            </div>
            <iframe id="receiver" src="https://ocwen.dev.amelia.com/Amelia/ui/ocwen/chat?embed=iframe&domainCode=owcenfinancial" frameborder="0" width="100%" height="100%" allow="geolocation; microphone; camera">
        <p>Your browser does not support iframes.</p>
      </iframe>
            <div class="chat-overlay-header">
                <img class="chat-overlay-header-img close" src="./amelia-close.png" alt="toggle chat overlay" />
                <img class="chat-overlay-header-img open" src="./amelia-icon.png" alt="toggle chat overlay" />
            </div>
        </div>
    </div>


    <script>
        function openChatOverlay(receiverElem, imgElemOpen, imgElemClose) {
            document.getElementById('receiver').classList.add("open");
            document.getElementById('receiver').classList.remove("close");
            document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-open");
            document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-closed");
            document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.remove('close');
            imgElemClose.style.opacity = 1;
            imgElemOpen.style.opacity = 0;
            localStorage.setItem('chatOverlayOpen', true);
        }

        function closeChatOverlay(receiverElem, imgElemOpen, imgElemClose) {
            document.getElementById('receiver').classList.add("close");
            document.getElementById('receiver').classList.remove("open");
            document.getElementsByClassName('chat-overlay')[0].classList.add("chat-overlay-closed");
            document.getElementsByClassName('chat-overlay')[0].classList.remove("chat-overlay-open");
            document.getElementsByClassName('chat-overlay-header-mobile')[0].classList.add('close');
            imgElemOpen.style.opacity = 1;
            imgElemClose.style.opacity = 0;
            localStorage.setItem('chatOverlayOpen', false);
        }

        function toggleChatOverlay() {
            /**
             * Toggles opening and closing of the chatOverlay
             * @returns - no return
             */
            var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
            var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
            var receiverElem = document.getElementById('receiver');
            if (receiverElem.classList.contains('close')) {
                openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
            } else {
                closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
            }
        }

        var chatOverlayHeaderElem = document.getElementsByClassName('chat-overlay-header')[0];
        chatOverlayHeaderElem.addEventListener('click', toggleChatOverlay);
        var chatOverlayHeaderElemMobile = document.getElementsByClassName('chat-overlay-header-mobile')[0];
        chatOverlayHeaderElemMobile.addEventListener('click', toggleChatOverlay);


        if (typeof(Storage) !== "undefined") {
            var chatOverlayOpen = localStorage.getItem('chatOverlayOpen');
            var chatOverlayHeaderImgElemOpen = document.getElementsByClassName('chat-overlay-header-img open')[0];
            var chatOverlayHeaderImgElemClose = document.getElementsByClassName('chat-overlay-header-img close')[0];
            var receiverElem = document.getElementById('receiver');
            if (chatOverlayOpen && localStorage.getItem('chatOverlayOpen') !== "true") {
                closeChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
            } else {
                openChatOverlay(receiverElem, chatOverlayHeaderImgElemOpen, chatOverlayHeaderImgElemClose);
            }
        } else {
            // Sorry! No Web Storage support..
            console.log('No localStorage support')
        }
    </script>

</body>

</html>
