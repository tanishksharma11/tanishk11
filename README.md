# tanishk11
<!DOCTYPE html>
<html>
<head>
    <style>

        body
         {
          font-family: 'Poppins', sans-serif;
          background-image: url("https://blog.examin.co.in/wp-content/uploads/2017/11/02081.jpeg");
          background-repeat:no-repeat;
          background-size: cover;
          display: flex;
          justify-content: center;
        }
        
        .container 
        {
          width: 450px;
          padding: 20px;
          margin-top: 80px;
          background-image:url("https://www.leadquizzes.com/wp-content/uploads/2019/02/New-blog-graphic.jpg");
          background-repeat:no-repeat;
          background-size: cover;
          box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
          border-radius: 20px;
        }
        
        h1 
        {
          text-align: center;
        }
        
        .question
         {
          font-weight: bold;
          font-size: 35px;
          margin-bottom: 10px;
        }
        
        .options 
        {
          margin-bottom: 20px;
        }
        
        .option 
        {
          display: block;
          margin-bottom: 10px;
        }
        
        .button 
        {
          display: inline-block;
          padding: 10px 20px;
          background-color: #428bca;
          color: #fff;
          border: none;
          cursor: pointer;
          font-size: 16px;
          border-radius: 4px;
          transition: background-color 0.3s;
          margin-right: 10px;
        }
        
        .button:hover 
        {
          background-color: #3071a9;
        }
        
        .result 
        {
          text-align: center;
          margin-top: 20px;
          font-weight: bold;
        }
        
        .hide
        {
          display: none;
        }</style>
  <title>JavaScript Quiz App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>Quizzone</h1>
    <div id="quiz"></div>
    <div id="result" class="result"></div>
    <button id="submit" class="button">Submit</button>
    <button id="retry" class="button hide">Retry</button>
    <button id="showAnswer" class="button hide">Show Answer</button>
  </div>
  <script>const quizData = [
    {
      question: 'What is the currency of Myanmar?',
      options: ['Rupee', 'Burma', 'Dollar', 'Euro'],
      answer: 'Paris',
    },
    {
      question: 'What is the largest planet in our solar system?',
      options: ['Mars', 'Saturn', 'Jupiter', 'Neptune'],
      answer: 'Jupiter',
    },
    {
      question: 'Which country won the FIFA World Cup in 2018?',
      options: ['Brazil', 'Germany', 'France', 'Argentina'],
      answer: 'France',
    },
    {
      question: 'What is the tallest mountain in the world?',
      options: ['Mount Everest', 'K2', 'Kangchenjunga', 'Makalu'],
      answer: 'Mount Everest',
    },
    {
      question: 'Which is the largest ocean on Earth?',
      options: [
        'Pacific Ocean',
        'Indian Ocean',
        'Atlantic Ocean',
        'Arctic Ocean',
      ],
      answer: 'Pacific Ocean',
    },
    {
      question: 'What is the chemical symbol for gold?',
      options: ['Au', 'Ag', 'Cu', 'Fe'],
      answer: 'Au',
    },
    {
      question: 'Who painted the Mona Lisa?',
      options: [
        'Pablo Picasso',
        'Vincent van Gogh',
        'Leonardo da Vinci',
        'Michelangelo',
      ],
      answer: 'Leonardo da Vinci',
    },
    {
      question: 'Which planet is known as the Red Planet?',
      options: ['Mars', 'Venus', 'Mercury', 'Uranus'],
      answer: 'Mars',
    },
    {
      question: 'What is the largest species of shark?',
      options: [
        'Great White Shark',
        'Whale Shark',
        'Tiger Shark',
        'Hammerhead Shark',
      ],
      answer: 'Whale Shark',
    },
    {
      question: 'Which animal is known as the King of the Jungle?',
      options: ['Lion', 'Tiger', 'Elephant', 'Giraffe'],
      answer: 'Lion',
    },
  ];
  
  const quizContainer = document.getElementById('quiz');
  const resultContainer = document.getElementById('result');
  const submitButton = document.getElementById('submit');
  const retryButton = document.getElementById('retry');
  const showAnswerButton = document.getElementById('showAnswer');
  
  let currentQuestion = 0;
  let score = 0;
  let incorrectAnswers = [];
  
  function shuffleArray(array) 
  {
    for (let i = array.length - 1; i > 0; i--) 
    {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }
  
  function displayQuestion() {
    const questionData = quizData[currentQuestion];
  
    const questionElement = document.createElement('div');
    questionElement.className = 'question';
    questionElement.innerHTML = questionData.question;
  
    const optionsElement = document.createElement('div');
    optionsElement.className = 'options';
  
    const shuffledOptions = [...questionData.options];
    shuffleArray(shuffledOptions);
  
    for (let i = 0; i < shuffledOptions.length; i++) 
    {
      const option = document.createElement('label');
      option.className = 'option';
  
      const radio = document.createElement('input');
      radio.type = 'radio';
      radio.name = 'quiz';
      radio.value = shuffledOptions[i];
  
      const optionText = document.createTextNode(shuffledOptions[i]);
  
      option.appendChild(radio);
      option.appendChild(optionText);
      optionsElement.appendChild(option);
    }
  
    quizContainer.innerHTML = '';
    quizContainer.appendChild(questionElement);
    quizContainer.appendChild(optionsElement);
  }
  
  function checkAnswer() 
  {
    const selectedOption = document.querySelector('input[name="quiz"]:checked');
    if (selectedOption) 
    {
      const answer = selectedOption.value;
      if (answer === quizData[currentQuestion].answer)
       {
        score++;
      } else 
      {
        incorrectAnswers.push(
          {
          question: quizData[currentQuestion].question,
          incorrectAnswer: answer,
          correctAnswer: quizData[currentQuestion].answer,
        });
      }
      currentQuestion++;
      selectedOption.checked = false;
      if (currentQuestion < quizData.length) 
      {
        displayQuestion();
      } else 
      {
        displayResult();
      }
    }
  }
  
  function displayResult() 
  {
    quizContainer.style.display = 'none';
    submitButton.style.display = 'none';
    retryButton.style.display = 'inline-block';
    showAnswerButton.style.display = 'inline-block';
    resultContainer.innerHTML = You scored ${score} out of ${quizData.length}!;
  }
  
  function retryQuiz()
  {
    currentQuestion = 0;
    score = 0;
    incorrectAnswers = [];
    quizContainer.style.display = 'block';
    submitButton.style.display = 'inline-block';
    retryButton.style.display = 'none';
    showAnswerButton.style.display = 'none';
    resultContainer.innerHTML = '';
    displayQuestion();
  }
  
  function showAnswer() 
  {
    quizContainer.style.display = 'none';
    submitButton.style.display = 'none';
    retryButton.style.display = 'inline-block';
    showAnswerButton.style.display = 'none';
  
    let incorrectAnswersHtml = '';
    for (let i = 0; i < incorrectAnswers.length; i++) 
    {
      incorrectAnswersHtml += `
        <p>
          <strong>Question:</strong> ${incorrectAnswers[i].question}<br>
          <strong>Your Answer:</strong> ${incorrectAnswers[i].incorrectAnswer}<br>
          <strong>Correct Answer:</strong> ${incorrectAnswers[i].correctAnswer}
        </p>
      `;
    }
  
    resultContainer.innerHTML = `
      <p>You scored ${score} out of ${quizData.length}!</p>
      <p>Incorrect Answers:</p>
      ${incorrectAnswersHtml}
    `;
  }
  
  submitButton.addEventListener('click', checkAnswer);
  retryButton.addEventListener('click', retryQuiz);
  showAnswerButton.addEventListener('click', showAnswer);
  
  displayQuestion();</script>
</body>
</html>
