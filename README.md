<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Quiz Builder</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea, #764ba2);
            min-height: 100vh;
            padding: 30px 15px;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }

        header h1 {
            font-size: 40px;
            margin-bottom: 8px;
        }

        header p {
            font-size: 18px;
        }

        .container {
            max-width: 850px;
            margin: auto;
        }

        .quiz-card {
            background: white;
            padding: 30px;
            border-radius: 18px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
        }

        label {
            display: block;
            font-weight: bold;
            margin-bottom: 8px;
            color: #333;
        }

        .title-input {
            margin-bottom: 25px;
        }

        input,
        select {
            width: 100%;
            padding: 13px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 15px;
            outline: none;
            transition: 0.3s;
        }

        input:focus,
        select:focus {
            border-color: #667eea;
        }

        .question {
            background: #f7f8ff;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
            border-left: 5px solid #667eea;
        }

        .question-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .question-header h3 {
            color: #667eea;
        }

        .delete-btn {
            background: #ff4d4d;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 6px;
            cursor: pointer;
        }

        .delete-btn:hover {
            background: #e63939;
        }

        .answers {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin: 15px 0;
        }

        .buttons {
            display: flex;
            gap: 12px;
            margin-top: 20px;
        }

        button {
            border: none;
            padding: 13px 20px;
            border-radius: 8px;
            font-size: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
        }

        .add-btn {
            background: #555;
            color: white;
        }

        .save-btn {
            background: #667eea;
            color: white;
        }

        .preview-btn {
            background: #22c55e;
            color: white;
        }

        .preview {
            display: none;
            margin-top: 25px;
            padding: 25px;
            background: #f0fff4;
            border: 2px solid #22c55e;
            border-radius: 12px;
        }

        .preview h2 {
            color: #166534;
            margin-bottom: 20px;
        }

        .preview-question {
            background: white;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }

        .preview-question h3 {
            margin-bottom: 12px;
        }

        .preview-option {
            display: block;
            margin: 8px 0;
            padding: 10px;
            background: #f5f5f5;
            border-radius: 6px;
        }

        .success {
            display: none;
            background: #dcfce7;
            color: #166534;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
            text-align: center;
            font-weight: bold;
        }

        @media (max-width: 600px) {
            header h1 {
                font-size: 30px;
            }

            .quiz-card {
                padding: 20px;
            }

            .answers {
                grid-template-columns: 1fr;
            }

            .buttons {
                flex-direction: column;
            }

            button {
                width: 100%;
            }
        }
    </style>
</head>

<body>

    <header>
        <h1>🧠 Quiz Builder</h1>
        <p>Create your own quiz easily</p>
    </header>

    <div class="container">

        <div class="quiz-card">

            <label for="quizTitle">Quiz Title</label>
            <input
                type="text"
                id="quizTitle"
                class="title-input"
                placeholder="Enter quiz title..."
            >

            <div id="questions"></div>

            <div class="buttons">
                <button class="add-btn" onclick="addQuestion()">
                    + Add Question
                </button>

                <button class="preview-btn" onclick="previewQuiz()">
                    👀 Preview
                </button>

                <button class="save-btn" onclick="saveQuiz()">
                    💾 Save Quiz
                </button>
            </div>

            <div class="success" id="successMessage">
                ✅ Quiz saved successfully!
            </div>

            <div class="preview" id="preview">
                <h2>Quiz Preview</h2>
                <div id="previewContent"></div>
            </div>

        </div>

    </div>


    <script>

        let questionNumber = 0;

        // Add first question automatically
        addQuestion();


        function addQuestion() {

            questionNumber++;

            const questionsContainer =
                document.getElementById("questions");

            const question = document.createElement("div");

            question.className = "question";

            question.innerHTML = `

                <div class="question-header">

                    <h3>
                        Question ${questionNumber}
                    </h3>

                    <button
                        class="delete-btn"
                        onclick="deleteQuestion(this)"
                    >
                        🗑 Delete
                    </button>

                </div>

                <label>Question</label>

                <input
                    type="text"
                    class="question-text"
                    placeholder="Enter your question..."
                >

                <div class="answers">

                    <input
                        type="text"
                        class="answer"
                        placeholder="Answer A"
                    >

                    <input
                        type="text"
                        class="answer"
                        placeholder="Answer B"
                    >

                    <input
                        type="text"
                        class="answer"
                        placeholder="Answer C"
                    >

                    <input
                        type="text"
                        class="answer"
                        placeholder="Answer D"
                    >

                </div>

                <label>Correct Answer</label>

                <select class="correct-answer">

                    <option value="A">
                        Answer A
                    </option>

                    <option value="B">
                        Answer B
                    </option>

                    <option value="C">
                        Answer C
                    </option>

                    <option value="D">
                        Answer D
                    </option>

                </select>
            `;

            questionsContainer.appendChild(question);

        }


        function deleteQuestion(button) {

            const question = button.closest(".question");

            question.remove();

            updateQuestionNumbers();

        }


        function updateQuestionNumbers() {

            const questions =
                document.querySelectorAll(".question");

            questions.forEach((question, index) => {

                question.querySelector("h3").textContent =
                    `Question ${index + 1}`;

            });

            questionNumber = questions.length;

        }


        function previewQuiz() {

            const title =
                document.getElementById("quizTitle").value;

            const questions =
                document.querySelectorAll(".question");

            const preview =
                document.getElementById("preview");

            const previewContent =
                document.getElementById("previewContent");

            if (!title.trim()) {

                alert("Please enter a quiz title.");

                return;

            }

            if (questions.length === 0) {

                alert("Please add at least one question.");

                return;

            }

            let html = `
                <h3>${escapeHTML(title)}</h3>
                <br>
            `;

            questions.forEach((question, index) => {

                const questionText =
                    question.querySelector(".question-text").value;

                const answers =
                    question.querySelectorAll(".answer");

                html += `
                    <div class="preview-question">

                        <h3>
                            ${index + 1}. 
                            ${escapeHTML(questionText)}
                        </h3>
                `;

                answers.forEach((answer, answerIndex) => {

                    const letter =
                        String.fromCharCode(65 + answerIndex);

                    html += `
                        <div class="preview-option">
                            <strong>${letter}.</strong>
                            ${escapeHTML(answer.value)}
                        </div>
                    `;

                });

                html += `</div>`;

            });

            previewContent.innerHTML = html;

            preview.style.display = "block";

            preview.scrollIntoView({
                behavior: "smooth"
            });

        }


        function saveQuiz() {

            const title =
                document.getElementById("quizTitle").value;

            const questions =
                document.querySelectorAll(".question");

            if (!title.trim()) {

                alert("Please enter a quiz title.");

                return;

            }

            if (questions.length === 0) {

                alert("Please add at least one question.");

                return;

            }

            const quiz = {

                title: title,

                questions: []

            };


            questions.forEach(question => {

                const questionText =
                    question.querySelector(".question-text").value;

                const answers =
                    question.querySelectorAll(".answer");

                const correct =
                    question.querySelector(".correct-answer").value;

                quiz.questions.push({

                    question: questionText,

                    answers: [

                        answers[0].value,
                        answers[1].value,
                        answers[2].value,
                        answers[3].value

                    ],

                    correctAnswer: correct

                });

            });


            localStorage.setItem(
                "myQuiz",
                JSON.stringify(quiz)
            );


            const success =
                document.getElementById("successMessage");

            success.style.display = "block";

            setTimeout(() => {

                success.style.display = "none";

            }, 3000);

        }


        function escapeHTML(text) {

            const div = document.createElement("div");

            div.textContent = text;

            return div.innerHTML;

        }

    </script>

</body>
</html>
