<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PlayVerse</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background-color: #0F0F0F;
    color: white;
    text-align: center;
}

header {
    background: #7B2FFF;
    padding: 20px;
    font-size: 28px;
    font-weight: bold;
}

.container {
    padding: 20px;
}

input {
    padding: 10px;
    width: 60%;
    margin: 10px;
    border-radius: 5px;
    border: none;
}

button {
    padding: 10px 20px;
    background: #00C2FF;
    border: none;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

.video-box {
    margin-top: 20px;
}

iframe {
    width: 80%;
    height: 400px;
    border-radius: 10px;
}

.comment-section {
    margin-top: 20px;
}

.comment {
    background: #1a1a1a;
    padding: 10px;
    margin: 5px auto;
    width: 60%;
    border-radius: 5px;
}
</style>
</head>

<body>

<header>🎮 PlayVerse</header>

<div class="container">
    <h2>Poste seu vídeo (cole o link do YouTube)</h2>
    <input type="text" id="videoLink" placeholder="Cole o link aqui">
    <br>
    <button onclick="addVideo()">Publicar</button>

    <div class="video-box" id="videoBox"></div>

    <div class="comment-section">
        <h3>Comentários</h3>
        <input type="text" id="commentInput" placeholder="Escreva um comentário">
        <button onclick="addComment()">Comentar</button>
        <div id="comments"></div>
    </div>
</div>

<script>
function addVideo() {
    const link = document.getElementById("videoLink").value;
    const videoBox = document.getElementById("videoBox");

    if(link.includes("youtube.com") || link.includes("youtu.be")) {
        let videoID;

        if(link.includes("watch?v=")) {
            videoID = link.split("watch?v=")[1];
        } else if(link.includes("youtu.be/")) {
            videoID = link.split("youtu.be/")[1];
        }

        videoBox.innerHTML = `
            <iframe src="https://www.youtube.com/embed/${videoID}" 
            allowfullscreen></iframe>
            <br><br>
            <button onclick="likeVideo()">❤️ Curtir</button>
            <p id="likeCount">Curtidas: 0</p>
        `;
    }
}

let likes = 0;

function likeVideo() {
    likes++;
    document.getElementById("likeCount").innerText = "Curtidas: " + likes;
}

function addComment() {
    const input = document.getElementById("commentInput");
    const comments = document.getElementById("comments");

    if(input.value !== "") {
        const newComment = document.createElement("div");
        newComment.classList.add("comment");
        newComment.innerText = input.value;
        comments.appendChild(newComment);
        input.value = "";
    }
}
</script>

</body>
</html>
