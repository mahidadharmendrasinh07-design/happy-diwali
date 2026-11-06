
<!DOCTYPE html>
<html lang="gu">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gujarati Festival Wishes 🪔</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    background: #4b1009;
    color: #fff1ce;
    font-family: "Nirmala UI", sans-serif;
    text-align: center;
    padding: 25px 12px;
}

.container {
    max-width: 500px;
    margin: auto;
    padding: 25px 18px;
    background: #fff3d5;
    color: #6c220e;
    border: 4px solid #dba83e;
    border-radius: 20px;
}

h1 {
    color: #9d350c;
    margin-bottom: 15px;
}

p {
    line-height: 1.8;
    margin: 12px 0;
}

select, input {
    width: 100%;
    padding: 14px;
    margin: 9px 0;
    border: 2px solid #dba83e;
    border-radius: 10px;
    font-size: 16px;
    background: white;
}

button {
    width: 100%;
    padding: 15px;
    margin-top: 12px;
    border: none;
    border-radius: 10px;
    background: linear-gradient(90deg,#ffdc78,#eaa32d);
    color: #581b08;
    font-size: 17px;
    font-weight: bold;
    cursor: pointer;
}

#cardArea {
    display: none;
    margin-top: 25px;
}

#preview {
    width: 100%;
    border: 3px solid #dba83e;
    border-radius: 10px;
    margin-top: 15px;
}

.note {
    font-size: 13px;
    color: #6c220e;
}
</style>
</head>

<body>

<div class="container">

<h1>🪔 તહેવારની શુભકામનાઓ 🪔</h1>

<p>તમારા નામથી સુંદર શુભેચ્છા કાર્ડ બનાવો અને મોકલો!</p>

<select id="festival">
    <option value="diwali">શુભ દિવાળી</option>
    <option value="dhanteras">શુભ ધનતેરસ</option>
    <option value="newyear">નવું વર્ષ</option>
</select>

<input
    type="text"
    id="sender"
    placeholder="તમારું નામ લખો"
    maxlength="35"
>

<input
    type="text"
    id="receiver"
    placeholder="સામેની વ્યક્તિનું નામ"
    maxlength="35"
>

<button onclick="makeCard()">
🎁 મારું શુભેચ્છા કાર્ડ બનાવો
</button>

<div id="cardArea">

<h2>તમારું કાર્ડ તૈયાર છે! 🎉</h2>

<img id="preview" alt="તમારું શુભેચ્છા કાર્ડ">

<button onclick="shareCard()">
📲 WhatsApp પર કાર્ડ મોકલો
</button>

<button onclick="downloadCard()">
⬇️ કાર્ડ Download કરો
</button>

<p class="note">
WhatsApp Share Menu માં WhatsApp પસંદ કરો.
</p>

</div>

<canvas id="card" width="900" height="1200"
style="display:none"></canvas>

</div>

<script>

let cardBlob = null;
let cardURL = null;

function centerText(ctx,text,y,font,color) {
    ctx.font = font;
    ctx.fillStyle = color;
    ctx.textAlign = "center";
    ctx.fillText(text,450,y);
}

function wrapText(ctx,text,y,maxWidth,lineHeight,font,color) {

    ctx.font = font;
    ctx.fillStyle = color;
    ctx.textAlign = "center";

    let words = text.split(" ");
    let line = "";

    for(let word of words) {

        let test = line + word + " ";

        if(ctx.measureText(test).width > maxWidth && line) {
            ctx.fillText(line.trim(),450,y);
            line = word + " ";
            y += lineHeight;
        } else {
            line = test;
        }
    }

    if(line) {
        ctx.fillText(line.trim(),450,y);
    }
}

async function makeCard() {

    const sender = document.getElementById("sender").value.trim();
    const receiver = document.getElementById("receiver").value.trim();
    const festival = document.getElementById("festival").value;

    if(!sender || !receiver) {
        alert("બંને નામ લખો!");
        return;
    }

    const canvas = document.getElementById("card");
    const ctx = canvas.getContext("2d");

    await document.fonts.ready;

    // Background
    let bg = ctx.createLinearGradient(0,0,900,1200);

    bg.addColorStop(0,"#fff9e8");
    bg.addColorStop(0.5,"#ffeac0");
    bg.addColorStop(1,"#fff5d9");

    ctx.fillStyle = bg;
    ctx.fillRect(0,0,900,1200);

    // Golden border
    ctx.strokeStyle = "#c68a24";
    ctx.lineWidth = 12;
    ctx.strokeRect(22,22,856,1156);

    ctx.strokeStyle = "#e6b65c";
    ctx.lineWidth = 3;
    ctx.strokeRect(40,40,820,1120);

    // Decorations
    centerText(ctx,"🌼 🌺 🌼 🌺 🌼",115,"55px sans-serif","#a44b0b");

    centerText(ctx,"🪔",245,"110px sans-serif","#a44b0b");

    // Festival heading
    let heading = festival === "diwali"
        ? "શુભ દિવાળી"
        : festival === "newyear"
          ? "નુતન વર્ષ"
          : festival === "dhanteras"
            ? "શુભ ધનતેરસ"
            : "શુભ ધનતેરસ";


    centerText(
        ctx,
        heading,
        365,
        "bold 78px 'Nirmala UI', sans-serif",
        "#a5270d"
    );

    centerText(
        ctx,
        "ની હાર્દિક શુભકામનાઓ",
        440,
        "bold 38px 'Nirmala UI', sans-serif",
        "#61200c"
    );

    centerText(
        ctx,
        "પ્રિય " + receiver,
        545,
        "bold 48px 'Nirmala UI', sans-serif",
        "#a5270d"
    );

    let message = festival === "diwali"
        ? "તમને અને તમારા પરિવારને દિવાળીના પાવન પર્વની હાર્દિક શુભકામનાઓ."
        : festival === "newyear"
          ? "તમને અને તમારા પરિવારને નુતન વર્ષની હાર્દિક શુભકામનાઓ."
          : "આ ધનતેરસ તમારા જીવનમાં સુખ, સમૃદ્ધિ અને ખુશીઓ લઈને આવે તેવી શુભેચ્છાઓ.";

    wrapText(
        ctx,
        message,
        650,
        730,
        65,
        "36px 'Nirmala UI', sans-serif",
        "#57220e"
    );

    let secondMessage = festival === "diwali"
        ? "તમારા જીવનમાં સુખ, શાંતિ અને સમૃદ્ધિનો પ્રકાશ ફેલાય."
        : festival === "newyear"
          ? "નુતન વર્ષ નવી સફળતા અને ખુશીઓ લઈને આવે."
          : "ધન, આરોગ્ય અને સફળતા હંમેશા તમારી સાથે રહે.";

    wrapText(
        ctx,
        secondMessage,
        810,
        730,
        65,
        "34px 'Nirmala UI', sans-serif",
        "#7b3514"
    );

    // Festival artwork
    if(festival === "diwali") {

        centerText(ctx,"🌸 🪔 ✨ 🪔 🌸",990,"85px sans-serif","#a44b0b");

    } else if(festival === "newyear") {

        centerText(ctx,"🪷 ✨ 🌹 ✨ 🪷",990,"85px sans-serif","#a44b0b");

    } else if(festival === "dhanteras") {

        centerText(ctx,"🪷 🪙 🏺 🪙 🪷",990,"85px sans-serif","#a44b0b");

    }

    // Sender
    centerText(
        ctx,
        "શુભેચ્છક :",
        1080,
        "30px 'Nirmala UI', sans-serif",
        "#7b3514"
    );

    centerText(
        ctx,
        sender,
        1130,
        "bold 40px 'Nirmala UI', sans-serif",
        "#a5270d"
    );

    cardBlob = await new Promise(resolve =>
        canvas.toBlob(resolve,"image/png")
    );

    if(!cardBlob) {
        alert("કાર્ડ બનાવવામાં સમસ્યા આવી.");
        return;
    }

    if(cardURL) URL.revokeObjectURL(cardURL);

    cardURL = URL.createObjectURL(cardBlob);

    document.getElementById("preview").src = cardURL;

    document.getElementById("cardArea").style.display = "block";

    document.getElementById("cardArea").scrollIntoView({
        behavior:"smooth"
    });
}

async function shareCard() {

    if(!cardBlob) return;

    const file = new File(
        [cardBlob],
        "Festival-Wishes.png",
        {type:"image/png"}
    );

    if(
        navigator.share &&
        navigator.canShare &&
        navigator.canShare({files:[file]})
    ) {

        try {

            await navigator.share({
                title:"તહેવારની શુભકામનાઓ",
                text:"🪔 હાર્દિક શુભકામનાઓ!",
                files:[file]
            });

        } catch(error) {

            if(error.name !== "AbortError") {
                alert("કાર્ડ શેર થઈ શક્યું નથી.");
            }

        }

    } else {

        downloadCard();

        alert("કાર્ડ Download થઈ ગયું છે. હવે WhatsAppમાં Image મોકલો.");

    }
}

function downloadCard() {

    if(!cardBlob) return;

    const link = document.createElement("a");

    link.href = cardURL;
    link.download = "Festival-Wishes.png";

    link.click();
}

</script>

</body>
</html>
