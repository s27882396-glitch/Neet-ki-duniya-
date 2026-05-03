!DOCTYPE html><html>
<head>
    <title>NEET Mock Test Pro</title>
    <style>
        body { font-family: Arial; text-align:center; background:#f5f5f5; }
        .quiz-box {
            background:white;
            width:80%;
            margin:auto;
            padding:20px;
            margin-top:50px;
            border-radius:10px;
            box-shadow:0px 0px 10px gray;
        }
        button {
            display:block;
            width:100%;
            margin:10px 0;
            padding:10px;
            background:green;
            color:white;
            border:none;
            border-radius:5px;
        }
        #timer { color:red; font-size:20px; }
    </style>
</head>
<body><div class="quiz-box">
    <h1>NEET Mock Test Pro</h1>
    <h3 id="timer">Time Left: 30</h3>
    <h2 id="question"></h2>
    <div id="answers"></div>
</div><script>
let username = prompt("Enter your name:");
let isPremiumUser = confirm("Do you have Premium Access? Click OK for Yes / Cancel for Free User");

const quizData = [
    {
        question: "Which organelle is known as powerhouse of the cell?",
        options: ["Ribosome", "Mitochondria", "Nucleus", "Golgi Body"],
        correct: "Mitochondria"
    },
    {
        question: "What is the SI unit of force?",
        options: ["Joule", "Newton", "Pascal", "Watt"],
        correct: "Newton"
    },
    {
        question: "pH of pure water is?",
        options: ["5", "6", "7", "8"],
        correct: "7"
    },
    {
        question: "DNA is found in?",
        options: ["Nucleus", "Blood Plasma", "Skin", "Muscles"],
        correct: "Nucleus"
    }
];

let currentQuestion = 0;
let score = 0;
let timeLeft = 30;

function loadQuestion(){
    const q = quizData[currentQuestion];
    document.getElementById('question').innerText = q.question;

    let optionsHtml = "";
    q.options.forEach(option => {
        optionsHtml += `<button onclick="checkAnswer('${option}')">${option}</button>`;
    });

    document.getElementById('answers').innerHTML = optionsHtml;
}

function checkAnswer(answer){
    if(answer === quizData[currentQuestion].correct){
        score = score + 4;   // NEET correct marks
    } else {
        score = score - 1;   // NEET negative marking
    }

    currentQuestion++;

    if(currentQuestion < quizData.length){
        function aiDoubtSolver(){
    alert("AI Doubt Solver Coming Soon: Upload image/PDF and solve doubts 🤖");
}

if(!isPremiumUser){
   alert("Free users can access only basic mock tests. Premium tests are locked 🔒");
}

loadQuestion();
    } else {
        finishTest();
    }
}

function finishTest(){
    localStorage.setItem(username, score);

    let rank = score === quizData.length ? "Top Rank 🏆" : "Keep Practicing 💪";

    document.querySelector('.quiz-box').innerHTML = `
        <h1>Test Completed ✅</h1>
        <h2>${username}, Your NEET Score: ${score}</h2>
        <h3>Leaderboard Score Saved</h3>
        <h3>Your Rank Status: ${rank}</h3>
        <button onclick="aiDoubtSolver()">Ask AI Doubt Solver</button>
    `;
}

let timer = setInterval(() => {
    timeLeft--;
    document.getElementById('timer').innerText = "Time Left: " + timeLeft;

    if(timeLeft <= 0){
        clearInterval(timer);
        finishTest();
    }
},1000);

loadQuestion();
</script></body>
</html>
