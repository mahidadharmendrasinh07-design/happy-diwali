
<!DOCTYPE html>
<html lang="gu">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diwali Greeting Card 🪔</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    background: linear-gradient(135deg,#360707,#811d13,#350707);
    color: #fff2ce;
    font-family: "Nirmala UI", sans-serif;
    text-align: center;
    padding: 25px 15px;
}

.container {
    max-width: 500px;
    margin: auto;
    padding: 25px 18px;
    border: 2px solid #e9bd56;
    border-radius: 22px;
    background: #4b0b0b;
    box-shadow: 0 0 25px #ffbb4480;
}

h1 {
    color: #ffd76a;
    margin-bottom: 15px;
    font-size: 32px;
}

p {
    line-height: 1.8;
    margin-bottom: 15px;
}

input {
    width: 100%;
    padding: 14px;
    margin: 9px 0;
    border: 2px solid #e9bd56;
    border-radius: 10px;
    font-size: 16px;
}

button {
    width: 100%;
    padding: 14px;
    margin-top: 12px;
    border: none;
    border-radius: 12px;
    background: linear-gradient(90deg,#ffe17b,#ff9e22);
    color: #501000;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
}

button:hover {
    transform: scale(1.02);
}

#cardArea {
    display: none;
    margin-top: 25px;
}

#preview {
    width: 100%;
    border: 3px solid gold;
    border-radius: 12px;
    margin-top: 12px;
}

.share-note {
    font-size: 13px;
    color: #ffe2a1;
    margin-top: 10px;
}

</style>
</head>

<body>

<div class="container">

    <h1>🪔 શુભ દિવાળી 🪔</h1>

    <p>
        પ્રકાશના પર્વની હાર્દિક શુભકામનાઓ!
        <br>
        તમારી પોતાની દિવાળી શુભેચ્છા બનાવો.
    </p>

    <input
        type="text"
        id="sender"
        placeholder="તમારું નામ લખો"
        maxlength="35"
    >

    <input
        type="text"
        id="receiver"
        placeholder="જેને મોકલવું છે તેનું નામ"
        maxlength="35"
    >

    <button onclick="makeCard()">
        🎁 Greeting Card બનાવો
    </button>

    <div id="cardArea">

        <h2>તમારું દિવાળી કાર્ડ તૈયાર છે! 🎉</h2>

        <img id="preview" alt="Diwali Greeting Card">

        <button onclick="shareCard()">
            📲 WhatsApp પર કાર્ડ મોકલો
        </button>

        <button onclick="downloadCard()">
            ⬇️ કાર્ડ Download કરો
        </button>

        <p class="share-note">
            WhatsApp Share વિકલ્પમાં WhatsApp પસંદ કરીને
            તમારા મિત્રને કાર્ડ મોકલો.
        </p>

    </div>

    <canvas id="card" width="1080" height="1350"
    style="display:none"></canvas>

</div>

<script>

let cardBlob = null;

function drawText(ctx, text, x, y, maxWidth, lineHeight) {

    let words = text.split(" ");
    let line = "";

    for (let i = 0; i < words.length; i++) {

        let test = line + words[i] + " ";

        if (ctx.measureText(test).width > maxWidth && line) {
            ctx.fillText(line.trim(), x, y);
            line = words[i] + " ";
            y += lineHeight;
        } else {
            line = test;
        }
    }

    if (line) {
        ctx.fillText(line.trim(), x, y);
    }
}

async function makeCard() {

    let sender = document.getElementById("sender").value.trim();
    let receiver = document.getElementById("receiver").value.trim();

    if (!sender || !receiver) {
        alert("કૃપા કરીને બંને નામ લખો!");
        return;
    }

    await document.fonts.ready;

    let canvas = document.getElementById("card");
    let ctx = canvas.getContext("2d");

    // Background
    let bg = ctx.createLinearGradient(0,0,1080,1350);
    bg.addColorStop(0,"#390606");
    bg.addColorStop(0.5,"#891b10");
    bg.addColorStop(1,"#360606");

    ctx.fillStyle = bg;
    ctx.fillRect(0,0,1080,1350);

    // Golden border
    ctx.strokeStyle = "#ffdb76";
    ctx.lineWidth = 12;
    ctx.strokeRect(35,35,1010,1280);

    ctx.strokeStyle = "#e6a82f";
    ctx.lineWidth = 3;
    ctx.strokeRect(55,55,970,1240);

    // Rangoli circles
    ctx.textAlign = "center";

    ctx.font = "100px sans-serif";
    ctx.fillText("🌸",540,180);

    ctx.font = "95px sans-serif";
    ctx.fillText("🪔",540,330);

    // Heading
    ctx.fillStyle = "#ffe28a";
    ctx.font = "bold 100px sans-serif";
    ctx.fillText("શુભ દિવાળી!",540,490);

    // Greeting
    ctx.fillStyle = "#fff1c6";
    ctx.font = "bold 52px 'Nirmala UI', sans-serif";
    ctx.fillText("પ્રિય " + receiver,540,600);

    ctx.font = "42px 'Nirmala UI', sans-serif";
    drawText(
        ctx,
        "તમને અને તમારા પરિવારને દિવાળીના પાવન પર્વની હાર્દિક શુભકામનાઓ.",
        540,710,850,75
    );

    ctx.fillStyle = "#ffd46b";
    ctx.font = "45px 'Nirmala UI', sans-serif";

    drawText(
        ctx,
        "તમારા જીવનમાં સુખ, શાંતિ, સમૃદ્ધિ અને ખુશીઓનો પ્રકાશ ફેલાય.",
        540,900,850,75
    );

    // Diyas
    ctx.font = "100px sans-serif";
    ctx.fillText("🪔 ✨ 🪔",540,1100);

    // Sender
    ctx.fillStyle = "#fff1c6";
    ctx.font = "bold 48px 'Nirmala UI', sans-serif";
    ctx.fillText("શુભેચ્છક: " + sender,540,1210);

    ctx.fillStyle = "#ffdc7b";
    ctx.font = "35px sans-serif";
    ctx.fillText("HAPPY DIWALI",540,1270);

    // Create image
    cardBlob = await new Promise(resolve =>
        canvas.toBlob(resolve,"image/png")
    );

    if (!cardBlob) {
        alert("કાર્ડ બનાવવામાં મુશ્કેલી આવી. ફરી પ્રયત્ન કરો.");
        return;
    }

    let imageURL = URL.createObjectURL(cardBlob);

    document.getElementById("preview").src = imageURL;

    document.getElementById("cardArea").style.display = "block";

    document.getElementById("cardArea").scrollIntoView({
        behavior: "smooth"
    });

}

async function shareCard() {

    if (!cardBlob) return;

    let file = new File(
        [cardBlob],
        "Happy-Diwali.png",
        {type:"image/png"}
    );

    if (navigator.canShare &&
        navigator.canShare({files:[file]}) &&
        navigator.share) {

        try {
            await navigator.share({
                files:[file],
                title:"Happy Diwali",
                text:"🪔 શુભ દિવાળી! 🪔"
            });
        } catch(error) {
            if (error.name !== "AbortError") {
                alert("Share કરવામાં મુશ્કેલી આવી.");
            }
        }

    } else {

        downloadCard();

        alert(
          "તમારું કાર્ડ Download થયું છે. હવે WhatsApp ખોલો અને આ Image મોકલો."
        );
    }

}

function downloadCard() {

    if (!cardBlob) return;

    let link = document.createElement("a");

    link.href = URL.createObjectURL(cardBlob);
    link.download = "Happy-Diwali.png";

    link.click();

    URL.revokeObjectURL(link.href);
}

</script>

</body>
</html>
