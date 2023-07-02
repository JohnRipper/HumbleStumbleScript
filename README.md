The ᕼᑌᗰᗷᒪEᔕTᑌᗰᗷᔕᑕᖇIᑭT is a UserScript written in JavaScript that aims to enhance the user experience of StumbleChat, a web-based chat platform. by providing additional functionality for handling specific chat messages and enabling media playback within the chat room.

The script modifies the behavior of WebSocket communication to intercept and manipulate messages. It establishes a WebSocket connection with the chat server and overrides the send method to intercept outgoing messages..

Temporary data structure within the execution context of the script, stored in memory within the JavaScript runtime environment only while the script is running.

// ==UserScript==
// @name         ᕼᑌᗰᗷᒪEᔕTᑌᗰᗷᔕᑕᖇIᑭT
// @namespace    http://tampermonkey.net/
// @version      4.2.0
// @description  Just For Fun - Script to enhance StumbleChat experience
// @author       Valhalla Team
// @match        https://stumblechat.com/room/*
// @grant        GM_xmlhttpRequest
// ==/UserScript==

(function () {
    const users = new Map(); // Store usernames using their ID numbers

    // Add your Imgur API credentials here
    const clientId = '0fb72170f80258d';
    const clientSecret = '5b46ee3f974c629ce47bacf7d021632105715883';

    WebSocket.prototype._send = WebSocket.prototype.send;
    WebSocket.prototype.send = function (data) {
        this._send(data);

        this.addEventListener('message', handleMessage.bind(this), false);

        this.send = function (data) {
            console.log('send:', data);
            const sendData = safeJSONParse(data);

            if (sendData && sendData['stumble'] === 'subscribe') {
                console.log('subscribe caught');
            } else {
                this._send(data);
            }
        };
    };

    function handleMessage(msg) {
        console.log('<<', msg.data);
        const wsmsg = safeJSONParse(msg.data);
        console.log(wsmsg);


        // Generate a random number between 1 and 100.

        if (wsmsg['text'] ==="number")
        {
            setTimeout(() => { this._send('{"stumble":"msg","text":"Generating random number between 1 and 100..."}'); }, 1000);
            setTimeout(() => {
                var randomNum = Math.floor(Math.random() * 100) + 1;
                this._send('{"stumble":"msg","text":"The random number is: ' + randomNum + '"}');
            }, 3000);
        }
        // Random links, images, messages
        if (wsmsg['text'] === "munch1es") // Post different MUNCH1ES logos randomly with each prompt.
        {
            var linkss = ["https://i.imgur.com/tE4Wjtx.png",
                          "https://i.imgur.com/8bhoJ6L.png",
                          "https://i.imgur.com/ngkXq7G.png",
                          "https://i.imgur.com/ZLPlKB8.png",
                          "https://i.imgur.com/T5dUnLS.png",
                          "https://i.imgur.com/E7qTtBE.png",
                          "https://i.imgur.com/D0EKZAK.png",
                          "https://i.imgur.com/sblamo8.gif",
                          "https://i.imgur.com/KoXl3OB.gif"
                         ];
            var randomslink = linkss[Math.floor(Math.random() * linkss.length)];

            this._send('{"stumble":"msg","text":"' + randomslink + '"}')
        }

        if (wsmsg['text'] === 'cheers') { // Celebrate with others when they say "cheers" you will to using randomized messages to keep it fresh.
            var links = [
                '̷🅒🅗🅔🅔🅡🅢',
                '🇨‌🇭‌🇪‌🇪‌🇷‌🇸‌',
                'ᶜᴴᴱᴱᴿˢ',
                '𝒞𝐻𝐸𝐸𝑅𝒮',
                'ℭℌ𝔈𝔈ℜ𝔖',
                'C҉H҉E҉E҉R҉S҉',
                'ꏳꃬꏂꏂꋪꑄ',
                'ᥴꫝꫀꫀ᥅ᦓ',
                'ςђєєгร',
                'ɔɥǝǝɹs',
                '⊂Ꮒ∈∈ᖇ⟆',
                '𝕔𝕙𝕖𝕖𝕣𝕤',
                '❰ █▬█ █☰ █☰ 🆁 ▟▛ ',
                'ｃ∙ｈ∙ｅ∙ｅ∙ｒ∙ｓ',

            ];
            var randomlink = links[Math.floor(Math.random() * links.length)];
            this._send('{"stumble":"msg","text":"' + randomlink + '"}')
        }

        //Send multiple messages, one after another quicker than you can in chat.
        if (wsmsg['text'] === "watch free movies")
        {
            setTimeout(() => { this._send('{"stumble":"msg","text":"These are 100% legal free streaming movie services."}'); }, 1000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"https://tubi.com"}'); }, 2000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"https://crackle.com/"}'); }, 3000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"https://www.vudu.com/"}'); }, 5000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"https://www.youtube.com/playlist?list=PLHPTxTxtC0ibVZrT2_WKWUl2SAxsKuKwx"}'); }, 6000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"https://www.imdb.com/tv/"}'); }, 7000);
        }

        if (wsmsg['text'] === "ding")
        {
            setTimeout(() => { this._send('{"stumble":"msg","text":"DONG"}'); }, 1000);
        }

        // Post a list of smiley emojis.

        if (wsmsg['text'] === "smiley emojis")
        {
            this._send('{"stumble":"msg","text": "🤣 🥲 🥹 ☺️ 😊 😇 🙂 🙃 😉 😌 😍 🥰 😘 😗 😙 😚 😋 😛 😝 😜 🤪 🤨 🧐 🤓 😎 🥸 🤩 🥳 😏 😒 😞 😔 😟 😕 🙁 ☹️ 😣 😖 😫 😩 🥺 😢 😭 😮‍💨 😤 😠 😡 🤬 🤯 😳 🥵 🥶 😱 😨 😰 😥 😓 🫣 🤗 🫡 🤔 🫢 🤭 🤫 🤥 😶 😶‍🌫️ 😐 😑 😬 🫨 🫠 🙄 😯 😦 😧 😮 😲 🥱 😴 🤤 😪 😵 😵‍💫 🫥 🤐 🥴 🤢 🤮 🤧 😷 🤒 🤕 🤑 🤠 😈 👿 👹 👺 🤡 💩 👻 💀 ☠️ 👽 👾 🤖 🎃 😺 😸 😹 😻 😼 😽 🙀 😿 😾"}')
        }
        if (wsmsg['text'] === "nature emojis") // Posts a list of emojis all nature related.
        {
            this._send('{"stumble":"msg","text": " 🌵 🎄 🌲 🌳 🌴 🪹 🪺 🪵 🌱 🌿 ☘️ 🍀 🎍 🪴 🎋 🍃 🍂 🍁 🍄 🐚 🪨 🌾 💐 🌷 🪷 🌹 🥀 🌺 🌸 🪻 🌼 🌻 🌞 🌝 🌛 🌜 🌚 🌕 🌖 🌗 🌘 🌑 🌒 🌓 🌔 🌙 🌎 🌍 🌏 🪐 💫 ⭐️ 🌟 ✨ ⚡️ ☄️ 💥 🔥 🌪 🌈 ☀️ 🌤 ⛅️ 🌥 ☁️ 🌦 🌧 ⛈ 🌩 🌨 ❄️ ☃️ ⛄️ 🌬 💨 💧 💦 🫧 ☔️ ☂️ 🌊 🌫"}')
        }
        if (wsmsg['text'] === "animal emojis") // Post a list of emojis all animal related.
        {
            this._send('{"stumble":"msg","text": "🐶 🐱 🐭 🐹 🐰 🦊 🐻 🐼 🐻‍❄️ 🐨 🐯 🦁 🐮 🐷 🐽 🐸 🐵 🙈 🙉 🙊 🐒 🐔 🐧 🐦 🐦‍⬛ 🐤 🐣 🐥 🦆 🦅 🦉 🦇 🐺 🐗 🐴 🦄 🐝 🪱 🐛 🦋 🐌 🐞 🐜 🪰 🪲 🪳 🦟 🦗 🕷 🕸 🦂 🐢 🐍 🦎 🦖 🦕 🐙 🦑 🦐 🦞 🦀 🪼 🪸 🐡 🐠 🐟 🐬 🐳 🐋 🦈 🐊 🐅 🐆 🦓 🫏 🦍 🦧 🦣 🐘 🦛 🦏 🐪 🐫 🦒 🦘 🦬 🐃 🐂 🐄 🐎 🐖 🐏 🐑 🦙 🐐 🦌 🫎 🐕 🐩 🦮 🐕‍🦺 🐈 🐈‍⬛ 🪽 🪶 🐓 🦃 🦤 🦚 🦜 🦢 🪿 🦩 🕊 🐇 🦝 🦨 🦡 🦫 🦦 🦥 🐁 🐀 🐿 🦔 🐾 🐉 🐲 "}')
        }
        if (wsmsg['text'] === "new emojis") // Post a list of new emojis.
        {
            this._send('{"stumble":"msg","text": "🫨 🩷 🩵 🩶 🫸 🫸🏻 🫸🏼 🫸🏽 🫸🏾 🫸🏿 🫷 🫷🏻 🫷🏼 🫷🏽 🫷🏾 🫷🏿 🫏 🫎 🪿 🐦‍⬛ 🪽 🪼 🪻 🫛 🫚 🪭 🪮 🪈 🪇​ 🫠 🫢 🫣 🫡 🫥 🫤 🥹 🫱 🫰🫵 🫶 🧌 🪸 🪷 🪹 🪺 🫘 🫗 🫙 🛝 🛞 🛟 🪬 🪩 🪫 🩼 🩻 🫧 🪪 🧔‍♂️ 🧔‍♀️ 🟰 🫃 😮‍💨 😵‍💫 😶‍🌫️ "}')
        }
        if (wsmsg['text'] === "object emojis") // Post a list of object emojis.
        {
            setTimeout(() => { this._send('{"stumble":"msg","text":"⌚️ 📱 📲 💻 ⌨️ 🖥 🖨 🖱 🖲 🕹 🗜 💽 💾 💿 📀 📼 📷 📸 📹 🎥 📽 🎞 📞 ☎️ 📟 📠 📺 📻 🎙 🎚 🎛 🧭 ⏱ ⏲ ⏰ 🕰 ⌛️ ⏳ 📡 🔋 🪫 🔌 💡 🔦 🕯 🪔 🧯 🛢 🛍️ 💸 💵 💴 💶 💷 🪙 💰 💳 "}'); }, 1000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"💎 ⚖️ 🪮 🪜 🧰 🪛 🔧 🔨 ⚒ 🛠 ⛏ 🪚 🔩 ⚙️ 🪤 🧱 ⛓ 🧲 🔫 💣 🧨 🪓 🔪 🗡 ⚔️ 🛡 🚬 ⚰️ 🪦 ⚱️ 🏺 🔮 📿 🧿 🪬 💈 ⚗️ 🔭 🔬 🕳 🩹 🩺 🩻 🩼 💊 💉 🩸 🧬 🦠 🧫 🧪 🌡 🧹 🪠 🧺 🧻 🚽 🚰 🚿 🛁 🛀 🧼"}'); }, 2000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"🪥 🪒 🧽 🪣 🧴 🛎 🔑 🗝 🚪 🪑 🛋 🛏 🛌 🧸 🪆 🖼 🪞 🪟 🛍 🛒 🎁 🎈 🎏 🎀 🪄 🪅 🎊 🎉 🪩 🎎 🏮 🎐 🧧 ✉️ 📩 📨 📧 💌 📥 📤 📦 🏷 🪧 📪 📫 📬 📭 📮 📯 📜 📃 📄 📑 🧾 📊 📈 📉 🗒 🗓 📆 📅 🗑 🪪 📇 🗃 🗳 🗄 📋 📁 📂 🗂 🗞 📰 📓 📔 📒 📕 📗 📘 📙 📚 📖 🔖 🧷 🔗 📎 🖇 📐 📏 🧮 📌 📍 ✂️ 🖊 🖋 ✒️ 🖌 🖍 📝 ✏️ 🔍 🔎 🔏 🔐 🔒 🔓"}'); }, 3000);
        }
        if (wsmsg['text'] === "symbol emojis")  // Post a list of symbol emojis.
        {
            setTimeout(() => { this._send('{"stumble":"msg","text":" 🚸 🔱 ⚜️ 🔰 ♻️ ✅ 🈯️ 💹 ❇️ ✳️ ❎ 🌐 💠 Ⓜ️ 🌀 💤 🏧 🚾 ♿️ 🅿️ 🛗 🈳 🈂️ 🛂 🛃 🛄 🛅 🚹 🚺 🚼 ⚧ 🚻 🚮 🎦 🛜 📶 🈁 🔣 ℹ️ 🔤 🔡 🔠 🆖 🆗 🆙 🆒 🆕 🆓 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟 🔢 #️⃣ *️⃣ ⏏️ ▶️ ⏸ ⏯ ⏹ ⏺ ⏭ ⏮ ⏩ ⏪ ⏫ ⏬ ◀️ 🔼 🔽 ➡️ ⬅️ ⬆️ ⬇️ ↗️ ↘️ ↙️ ↖️ ↕️ ↔️ ↪️ ↩️ ⤴️ ⤵️ 🔀 🔁 🔂 🔄 🔃 🎵 🎶 ➕ ➖ ➗ ✖️ 🟰 ♾ 💲 💱 ™️ ©️ ®️ 〰️ ➰ ➿ 🔚 🔙 🔛 🔝 🔜 ✔️ ☑️ 🔘  🔈 🔇 🔉 🔊 🔔 🔕 📣 📢 👁‍🗨 💬 💭 🗯 ♠️ ♣️ ♥️ ♦️ 🃏 🎴 🀄️"}'); }, 1000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"❤️ 🩷 🧡 💛 💚 💙 🩵 💜 🖤 🩶 🤍 🤎 ❤️‍🔥 ❤️‍🩹 💔 ❣️ 💕 💞 💓 💗 💖 💘 💝 💟 ☮️ ✝️ ☪️ 🪯 🕉 ☸️ ✡️ 🔯 🕎 ☯️ ☦️ 🛐 ⛎ ♈️ ♉️ ♊️ ♋️ ♌️ ♍️ ♎️ ♏️ ♐️ ♑️ ♒️ ♓️ 🆔 ⚛️"}'); }, 2000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"🉑 ☢️ ☣️ 📴 📳 🈶 🈚️ 🈸 🈺 🈷️ ✴️ 🆚 💮 🉐 ㊙️ ㊗️ 🈴 🈵 🈹 🈲 🅰️ 🅱️ 🆎 🆑 🅾️ 🆘 ❌ ⭕️ 🛑 ⛔️ 📛 🚫 💯 💢 ♨️ 🚷 🚯 🚳 🚱 🔞 📵 🚭 ❗️ ❕ ❓ ❔ ‼️ ⁉️ 🔅 🔆 〽️ ⚠️"}'); }, 3000);
        }
        if (wsmsg['text'] === "food emojis") // Post a list of food emojis.
        {
            this._send('{"stumble":"msg","text": "🍏 🍎 🍐 🍊 🍋 🍌 🍉 🍇 🍓 🫐 🍈 🍒 🍑 🥭 🍍 🥥 🥝 🍅 🍆 🥑 🥦 🫛 🥬 🥒 🌶 🫑 🌽 🥕 🫒 🧄 🧅 🫚 🥔 🍠 🫘 🥐 🥯 🍞 🥖 🥨 🧀 🥚 🍳 🧈 🥞 🧇 🥓 🥩 🍗 🍖 🦴 🌭 🍔 🍟 🍕 🫓 🥪 🥙 🧆 🌮 🌯 🫔 🥗 🥘 🫕 🥫 🍝 🍜 🍲 🍛 🍣 🍱 🥟 🦪 🍤 🍙 🍚 🍘 🍥 🥠 🥮 🍢 🍡 🍧 🍨 🍦 🥧 🧁 🍰 🎂 🍮 🍭 🍬 🍫 🍿 🍩 🍪 🌰 🥜 🍯 🥛 🍼 🫖 ☕️ 🍵 🧃 🥤 🧋 🫙 🍶 🍺 🍻 🥂 🍷 🫗 🥃 🍸 🍹 🧉 🍾 🧊 🥄 🍴 🍽 🥣 🥡 🥢 🧂"}')
        }
        if (wsmsg['text'] === "non emojis")// Post a list of non emojis.
        {
            this._send('{"stumble":"msg","text": "🔴 🟠 🟡 🟢 🔵 🟣 ⚫️ ⚪️ 🟤 🔺 🔻 🔸 🔹 🔶 🔷 🔳 🔲 ▪️ ▫️ ◾️ ◽️ ◼️ ◻️ 🟥 🟧 🟨 🟩 🟦 🟪 ⬛️ ⬜️ 🟫 ✢ ✣ ✤ ✥ ✦ ✧ ★ ☆ ✯ ✡︎ ✩ ✪ ✫ ✬ ✭ ✮ ✶ ✷ ✵ ✸ ✹ → ⇒ ⟹ ⇨ ⇾ ➾ ⇢ ☛ ☞ ➔ ➜ ➙ ➛ ➝ ➞ ♠︎ ♣︎ ♥︎ ♦︎ ♤ ♧ ♡ ♢ ♚ ♛ ♜ ♝ ♞ ♟ ♔ ♕ ♖ ♗ ♘ ♙ ⚀ ⚁ ⚂ ⚃ ⚄ ⚅ 🂠 ⚈ ⚉ ⚆ ⚇ 𓀀 𓀁 𓀂 𓀃 𓀄 𓀅 𓀆 𓀇 𓀈 𓀉 𓀊 𓀋 𓀌 𓀍 𓀎 𓀏 𓀐 𓀑 𓀒 𓀓 𓀔 𓀕 𓀖 𓀗 𓀘 𓀙 𓀚 𓀛 𓀜 𓀝"}')
        }
        if (wsmsg['text'] === "hes gonna pop") // That moment when you break down from being plugged in to long.
        {
            this._send('{"stumble":"msg","text": "https://i.imgur.com/vqTjZIA.gif"}')
        }
        if (wsmsg['text'] === "this guy gets it") // For when this guy gets it..
        {
            this._send('{"stumble":"msg","text": "https://i.imgur.com/1ZH30a8.gif"}')
        }
        if (wsmsg['text'] === "clever girl") // When she does something clever..
        {
            this._send('{"stumble":"msg","text": "https://i.imgur.com/7oDDdog.gif"}')
        }
        if (wsmsg['text'] === 'spaceshuttle') { // Its a, spaceshuttle, obviously..
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⠀⠀⣠⣶⣿⣿⣿⣷⣤⡀⠀⠀⠀⠀⠀⠀⠀"}'); }, 1000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⢀⣾⡿⠋⠀⠿⠇⠉⠻⣿⣄⠀⠀⠀⠀⠀⠀"}'); }, 2000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⢠⣿⠏⠀⠀⠀⠀⠀⠀⠀⠙⣿⣆⠀⠀⠀⠀⠀"}'); }, 3000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⢠⣿⡏⠀⠀⠀⠀⠀⠀⠀⠀⠀⠸⣿⣆⠀⠀⠀⠀"}'); }, 4000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⢸⣿⡄⠀⠀⠀⢀⣤⣀⠀⠀⠀⠀⣿⡿⠀⠀⠀⠀"}'); }, 5000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠻⣿⣶⣶⣾⡿⠟⢿⣷⣶⣶⣿⡟⠁⠀⠀⠀⠀"}'); }, 6000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡏⠉⠁⠀⠀⠀⠀⠉⠉⣿⡇⠀⠀⠀⠀⠀"}'); }, 7000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 8000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 9000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 10000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 13000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 14000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 14000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀⠀⠀⠀⣿⡗⠀⠀⠀⠀⠀"}'); }, 15000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⠀⢸⣿⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 16600);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⠀⠀⠀⣿⡇⠀⣴⣿⠇⠀⠀⠀⠀⣿⡇⠀⠀⠀⠀⠀"}'); }, 16600);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠀⢀⣠⣴⣿⣷⣿⠟⠁⠀⠀⠀⠀⠀⣿⣧⣄⡀⠀⠀⠀"}'); }, 19000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⢀⣴⡿⠛⠉⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠉⠙⢿⣷⣄⠀"}'); }, 20000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⢠⣿⠏⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠙⣿⣆"}'); }, 21000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⣿⡟⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢹⣿"}'); }, 22000);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⣿⣇⠀⠀⠀⠀⠀⠀⢸⣿⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿"}'); }, 23500);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⢹⣿⡄⠀⠀⠀⠀⠀⠀⢿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣾⡿"}'); }, 24500);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠻⣿⣦⣀⠀⠀⠀⠀⠈⣿⣷⣄⡀⠀⠀⠀⠀⣀⣤⣾⡟⠁"}'); }, 25500);
            setTimeout(() => { this._send('{"stumble":"msg","text":"⠀⠀⠈⠛⠿⣿⣷⣶⣾⡿⠿⠛⠻⢿⣿⣶⣾⣿⠿⠛⠉⠀⠀"}'); }, 26500);
        }

        if (wsmsg['text'].startsWith("play random song")) { // Random songs from the list
            var ball_list = ["You broke it, I am fixing it for you. Please try it again..",
                             "youtube blues brothers cant turn you loose",
                             "youtube boom shack a lack",
                             "youtube miley cyrus flowers",
                             "youtube rick and morty moonman music video",
                             "youtube Alex Gaudino feat. Crystal Waters ",
                             "youtube Little Stranger - 'Brain Fog' with Del the Funky Homosapien",
                             "youtube Terry fold - Chaos Chaos ft. Justin Roiland ",
                             "youtube Get Schwifty Music Video | Rick and Morty",
                             "youtube Tom MacDonald - Dirty Money",
                             "youtube The White Stripes - Seven Nation Army",
                             "youtube Little Stranger Sing it high",
                             "youtube Dirtbag Dan - 211 - DBDLP",
                             "youtube OFFICIAL Somewhere over the Rainbow - Israel IZ Kamakawiwoʻole",
                             "youtube Weird Al Yankovic - Foil",
                             "youtube Rob Dougan - Clubbed To Death",
                             "youtube INZO - Overthinker",
                             "youtube DJ Shadow - Nobody Speak feat. Run The Jewels",
                             "youtube Lit- Over My Head",
                             "youtube The Urge - It's My Time To Fly",
                             "youtube Come Together (Remastered 2009)",
                             "youtube Little Stranger - Brain Fog (Live Acoustic) | Sugarshack Sessions",
                             "youtube Do You Feel It? rick and morty",
                             "youtube Little Stranger - Cool Kids w/ JARV & Damn Skippy ",
                             "youtube DJ Cummerbund - Play That Funky Music Rammstein",
                             "youtube PROF - Pack A Lunch feat. Redman ",
                             "youtube DEATH DEALERS ANONYMOUS ICE T",
                             "youtube M.I.A. - Paper Planes",
                             "youtube Dr. Greenthumb",
                             "youtube Electric Avenue",
                             "youtube brother noland Coconut Girl",
                             /* ... */];

            // Randomly selects an item from the ball_list array and assigns it to the ball_pick variable. The selection is based on generating a random index using Math.random() and multiplying it by the length of the ball_list array.
            var ball_pick = ball_list[Math.floor(Math.random() * ball_list.length)];

            // Sends a message using the _send method, passing a JSON-formatted string as the parameter. The JSON string contains a "stumble" property with a value of "msg" and a "text" property with the value of the randomly selected ball_pick. It sends the randomly selected item as a message.
            this._send('{"stumble":"msg","text":"' + ball_pick + '"}');
        }
        if (wsmsg['text'].startsWith('youtube')) { // Checks if the value of the "text" property in the wsmsg object starts with the string "youtube". It evaluates whether the received message is related to a YouTube query.

            // Extracts the query from the wsmsg['text'] property by creating a substring starting from the 3rd character (index 2) of the string. It removes the first two characters from the received message.
            var query = wsmsg['text'].substring(2);
            this._send('{"stumble": "youtube","type": "add","id": "' + query + '","time": 0}'); // Sends a message using the _send method, passing a JSON-formatted string as the parameter.
        }

        // Checks if wsmsg is falsy (e.g., null, undefined, etc.). If wsmsg is falsy, it indicates that the JSON parsing failed. The code block inside the if statement is executed, logging an error message to the console and then returning from the function.
        if (!wsmsg) {
            console.error('Invalid JSON message received:', msg.data);
            return;
        }
        if (wsmsg['stumble'] === 'msg') { // check the value of the stumble property in the wsmsg object. If the value is 'msg', it calls the handleChatMessage function with wsmsg as the parameter.
            handleChatMessage.call(this, wsmsg);
        } else if (wsmsg['stumble'] === 'join') { //  If the value is 'join', it calls the handleJoinMessage function with wsmsg as the parameter.
            handleJoinMessage.call(this, wsmsg); // The appropriate function is executed based on the value of wsmsg['stumble'].
        }
    }

    function handleChatMessage(wsmsg) {
        const { text } = wsmsg;

        if (text.startsWith('imgur ')) {

            // For a GIF based on the keyword
            const keyword = text.substring(4);

            //  calls the searchGif function, passing the extracted keyword as an argument. It initiates a search for a GIF based on the provided keyword.
            searchGif(keyword)

            // Sets up a callback function to be executed when the searchGif function successfully resolves with a GIF URL. The resolved URL is passed as the gifUrl parameter.
                .then(gifUrl => {
                if (gifUrl) {

                    // If it exists, the respondWithMessage function is called, passing the GIF URL as a parameter.
                    respondWithMessage.call(this, gifUrl);
                } else {

                    // If it exists, the respondWithMessage function is called, passing the GIF URL as a parameter.
                    respondWithMessage.call(this, 'No GIF found for the keyword.');
                }
            })

            // The error is passed as the error parameter.
                .catch(error => {
                console.error('Error searching GIF:', error);
                respondWithMessage.call(this, 'Error occurred while searching for GIF.');
            });
        } else if (text.startsWith('upload ')) {
            const gifLink = text.substring(10);
            uploadGifToImgur(gifLink)
                .then(repostedLink => {

                //  If no valid gifUrl is found, the respondWithMessage function is called with the message "No GIF found for the keyword."
                respondWithMessage.call(this, repostedLink);
            })
            // Code sets up a callback function to be executed if an error occurs during the execution of the searchGif function.
                .catch(error => { // The error is passed as the error parameter.

                // Logs an error message with the specific error
                console.error('Error uploading GIF:', error);
                respondWithMessage.call(this, 'Error occurred while uploading GIF.');
            });
        } else if (text.startsWith('join ')) {
            const username = text.substring(5);

            // Declares a constant variable welcomeMessage and assigns it the result of calling the generateWelcomeMessage function with the handle parameter. It generates a welcome message using the handle value.
            const welcomeMessage = generateWelcomeMessage(username);

            //  Invokes the respondWithMessage function and sets its this value to the current object instance. It passes the welcomeMessage as the text parameter. The respondWithMessage function sends a response message to the server.
            respondWithMessage.call(this, welcomeMessage);
        }
    }

    // Handle join messages received from the server
    function handleJoinMessage(wsmsg) {

        // Retrieve ID and username from the message
        const { id, handle } = wsmsg;

        if (!users.has(id)) {

            // Store the username using the ID number
            users.set(id, handle);

            // Generate a welcome message using the username
            const welcomeMessage = generateWelcomeMessage(handle);
            respondWithMessage.call(this, welcomeMessage);
        }
    }

    // Defines the generateWelcomeMessage function, which takes a username parameter. It generates a random welcome message using the provided username.
    function generateWelcomeMessage(username) {
        const messages = [

            // Randomized welcome messages
            `Welcome, ${username}! Enjoy your stay.`,
            `Hello, ${username}! Have a great time in the chat.`,
            `Welcome aboard, ${username}! Let's chat and have fun.`,
            `Howdy, ${username}! Get ready to stumble upon interesting conversations.`,
            `Hey there, ${username}! Hope you brought pizza!`,
        ];

        //  declares a constant variable randomIndex and assigns it a random integer value between 0 (inclusive) and the length of the messages array (exclusive). It is used to select a random index from the messages array.
        const randomIndex = Math.floor(Math.random() * messages.length);

        // Returns a randomly selected welcome message from the messages array based on the randomIndex value. It is the generated welcome message.
        return messages[randomIndex];
    }

    // This code defines the respondWithMessage function, which takes a text parameter. It sends a response message to the server. The text parameter represents the content of the message.
    function respondWithMessage(text) {

        // Invokes the _send method/function of the current object instance. It sends a JSON stringified object as the payload. The object has a stumble property set to 'msg' and a text property set to the text parameter value.
        this._send(JSON.stringify({ stumble: 'msg', text }));
    }

    // Safely parses a JSON string.
    function safeJSONParse(jsonString) {

        // Starts a block of code that will be executed. It is used in conjunction with the catch keyword to handle potential errors that may occur during the execution of the code within the try block.
        try {

            // Attempts to parse the jsonString variable as a JSON string and convert it into a JavaScript object. The JSON.parse() method is used for this purpose. If the parsing is successful, the parsed JavaScript object is returned.
            return JSON.parse(jsonString);

            // If an error occurs during the execution of the code within the try block, the program flow will be redirected to this catch block. The error parameter captures the error object that was thrown.
        } catch (error) {

            // This line logs an error message to the console, indicating that an error occurred while parsing the JSON. The specific error message is passed as the second argument to console.error(). The error object contains information about the error that occurred.
            console.error('Error parsing JSON:', error);

            // In the event of an error during the parsing process, this line is executed, and null is returned. It serves as a default return value when the JSON parsing fails.
            return null;
        }
        // This closing curly brace marks the end of the catch block. It signifies the end of the error handling code.
    }

    // Searches for a GIF based on a keyword.
    function searchGif(keyword) {

        // The Promise takes two parameters: resolve and reject, which are functions used to indicate the successful fulfillment or failure of the Promise.
        return new Promise((resolve, reject) => {

            //  constructs the API URL by combining the base URL for the Imgur gallery search with the keyword parameter.
            const apiUrl = `https://api.imgur.com/3/gallery/search?q_type=anigif&q=${encodeURIComponent(keyword)}`;

            // It is part of the Greasemonkey (GM) API and allows the user script to make HTTP requests.
            GM_xmlhttpRequest({
                method: 'GET',
                url: apiUrl,

                //  Sets the headers of the HTTP request.
                headers: {
                    Authorization: `Client-ID ${clientId}`,
                },

                // defines an event handler function that is executed when the HTTP request successfully returns a response.
                onload: function (response) {

                    // This line starts a try block, indicating that any code inside the block should be executed and any potential errors should be caught and handled.
                    try {

                        // This line parses the response text from the HTTP request as JSON, converting it into a JavaScript object and assigning it to the data variable.
                        const data = JSON.parse(response.responseText);

                        // This line calls a function named selectRandomGif with the data object as an argument. It assumes that the function is defined elsewhere and is responsible for selecting a random GIF from the response data. The selected GIF is assigned to the gif variable.
                        const gif = selectRandomGif(data);

                        if (gif) { // Checks if a GIF was successfully selected (i.e., gif is truthy).
                            resolve(gif.link); //  If a GIF is present, the Promise is resolved with the link of the GIF using resolve(gif.link).
                        } else {
                            resolve(null); // Otherwise, if no GIF is found, the Promise is still resolved, but with a value of null using resolve(null)
                        }
                    } catch (error) { // catches any potential errors that occur during JSON parsing or GIF selection within the try block.
                        reject(error); // If an error is caught, it is passed to the reject function, indicating that the Promise should be rejected with the error.
                    }
                },
                // Defines an event handler function that is executed when there is an error during the HTTP request. The error parameter contains information about the error.
                onerror: function (error) {

                    // If an error occurs, it is passed to the reject function, indicating that the Promise should be rejected with the error.
                    reject(error);
                },
            }); // closes the GM_xmlhttpRequest call and the Promise object, indicating the end of the code block.
        }); // This line closes the uploadGifToImgur function.
    }


    //  The function, uploadGifToImgur, takes the gifLink parameter. This function is responsible for uploading a GIF to Imgur.
    function uploadGifToImgur(gifLink) {

        // Creates a new Promise object within the uploadGifToImgur function, indicating the eventual completion or failure of an asynchronous operation. It takes two parameters: resolve and reject, which are functions used to indicate the successful fulfillment or failure of the Promise.
        return new Promise((resolve, reject) => {

            //  Assigns the URL of the Imgur API endpoint for uploading images to the apiUrl variable.
            const apiUrl = 'https://api.imgur.com/3/image';

            GM_xmlhttpRequest({
                method: 'POST',
                url: apiUrl,
                headers: {

                    //  Sets the headers of the HTTP request.
                    Authorization: `Client-ID ${clientId}`,
                    'Content-Type': 'application/x-www-form-urlencoded',
                },
                data: `image=${encodeURIComponent(gifLink)}`,

                // defines an event handler function that is executed when the HTTP request successfully returns a response.
                onload: function (response) {

                    // This line starts a try block, indicating that any code inside the block should be executed and any potential errors should be caught and handled.
                    try {
                        const data = JSON.parse(response.responseText);
                        if (data.success) {
                            const repostedLink = data.data.link;
                            resolve(repostedLink);
                        } else {
                            reject('Error uploading GIF to Imgur');
                        }

                        //  catches any potential errors that occur during JSON parsing or checking the response data within the try block.
                    } catch (error) {
                        reject(error);
                    }
                },

                // If an error is caught, it is passed to the reject function, indicating that the Promise should be rejected with the error.
                onerror: function (error) {
                    reject(error);
                },
            });
        }); // closes the GM_xmlhttpRequest call.
    } // This line closes the uploadGifToImgur function.

    // Defines a function named selectRandomGif that takes the data parameter. This function is responsible for selecting a random GIF from the response data.
    function selectRandomGif(data) {
        const gifs = data.data.filter(item => item.type === 'image/gif');

        // This line checks if the data parameter and its nested data property exist, and if the length of the data.data array is greater than 0. It ensures that there is available GIF data to select from.
        if (gifs.length > 0) {

            //  Filters the data.data array to create a new array named gifs that only contains items with a type property equal to 'image/gif'. It selects only the GIF images from the response data.
            const randomIndex = Math.floor(Math.random() * gifs.length);

            // Returns the GIF object at the randomly selected index from the gifs array.
            return gifs[randomIndex];
        }

        // Returns null if there is no valid GIF data available in the response.
        return null;
    }

})();
