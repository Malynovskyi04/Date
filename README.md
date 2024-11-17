<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Приглашение на свидание</title>
  <style>
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      font-family: Arial, sans-serif;
      margin: 0;
      background: radial-gradient(circle, #2a3a58, #1e2a3a);
      color: #ffffff;
      overflow: hidden;
    }

    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      z-index: 1;
    }

    .container {
      width: 550px;
      height: 550px;
      text-align: center;
      padding: 30px;
      border: 3px solid #fff;
      border-radius: 15px;
      background-color: rgba(0, 0, 0, 0.7);
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 10;
    }

    .button {
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      border: 1px solid #333;
      border-radius: 5px;
      background-color: #ffffff;
      color: #333;
    }

    .hidden {
      display: none;
    }

    .heart {
      position: fixed;
      top: -50px;
      color: #9b59b6;
      font-size: 24px;
      animation-name: fallHearts;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
      opacity: 0.8;
      z-index: 2;
    }

    @keyframes fallHearts {
      to {
        transform: translateY(100vh);
      }
    }

    .snowflake {
      position: fixed;
      top: -50px;
      color: #FFF;
      font-size: 24px;
      animation-name: fallSnow;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
      opacity: 0.8;
      z-index: 1;
    }

    @keyframes fallSnow {
      to {
        transform: translateY(100vh);
      }
    }
  </style>
</head>
<body>

  <div class="overlay"></div>

  <div class="container" id="inviteBox">
    <p>Мы идем на свидание?</p>
    <button class="button" id="yesButton">Да</button>
    <button class="button" id="noButton">Нет</button>
    <button class="button" id="sickButton">Я заболела</button>
    <button class="button" id="examButton">У меня экзамены</button>
    <button class="button" id="busyButton">Я занята</button>
    <button class="button" id="pelmeniButton">Кушаю пельмени</button>
    <button class="button" id="holostyakButton">Смотрю холостяка</button>
    <button class="button" id="SvoyButton">Свой вариант</button>

  </div>

  <div class="container hidden" id="formBox">
    <p>Выбирай дату и время:</p>
    <label for="date">Дата:</label>
    <input type="date" id="date"><br><br>
    <label for="time">Время:</label>
    <input type="time" id="time"><br><br>
    <button class="button" id="sendButton">Отправить</button>
  </div>

  <script>
    const inviteBox = document.getElementById("inviteBox");
    const formBox = document.getElementById("formBox");

    const yesButton = document.getElementById("yesButton");
    const noButton = document.getElementById("noButton");
    const sickButton = document.getElementById("sickButton");
    const examButton = document.getElementById("examButton");
    const busyButton = document.getElementById("busyButton");
    const pelmeniButton = document.getElementById("pelmeniButton");
    const holostyakButton = document.getElementById("holostyakButton");
    const sendButton = document.getElementById("sendButton");
    const SvoyButton = document.getElementById("SvoyButton");

  
    const maxSnowflakes = 100;
    const maxHearts = 100;

    // Массивы для отслеживания текущих снежинок и сердечек
    let snowflakes = [];
    let hearts = [];

    // Функция для добавления падающих сердечек
    function startHearts() {
      const heartSymbol = "💜";  // Используем только фиолетовое сердечко
      setInterval(() => {
        if (hearts.length >= maxHearts) {
          // Удаляем первое сердечко, если их слишком много
          const firstHeart = hearts.shift();
          firstHeart.remove();
        }

        const heart = document.createElement("div");
        heart.classList.add("heart");
        heart.textContent = heartSymbol;
        heart.style.left = `${Math.random() * 100}vw`; // Случайная позиция по горизонтали
        heart.style.animationDuration = `5s`; // Увеличиваем время анимации
        heart.style.fontSize = `${Math.random() * 10 + 20}px`; // Разнообразие в размере сердечек
        heart.style.opacity = Math.random() * 0.5 + 0.3; // Разная прозрачность
        document.body.appendChild(heart);

        hearts.push(heart); // Добавляем в массив

        // Удаляем сердечко после анимации
        heart.addEventListener("animationend", () => {
          heart.remove();
        });
      }, 50); // Интервал создания сердечек
    }  

    function startSnowflakes() {
      const snowflakeSymbols = ["❄", "❅", "❆"];
      setInterval(() => {
        if (snowflakes.length >= maxSnowflakes) {
          // Удаляем первую снежинку, если их слишком много
          const firstSnowflake = snowflakes.shift();
          firstSnowflake.remove();
        }


        const snowflake = document.createElement("div");
        snowflake.classList.add("snowflake");
        snowflake.textContent = snowflakeSymbols[Math.floor(Math.random() * snowflakeSymbols.length)];
        snowflake.style.left = `${Math.random() * 100}vw`; // Случайная позиция по горизонтали
        snowflake.style.animationDuration = `5s`; // Увеличиваем время анимации
        snowflake.style.fontSize = `${Math.random() * 10 + 20}px`; // Разнообразие в размере снежинок
        snowflake.style.opacity = Math.random() * 0.5 + 0.3; // Разная прозрачность
        document.body.appendChild(snowflake);

        snowflakes.push(snowflake); // Добавляем в массив

        // Удаляем снежинку после анимации
        snowflake.addEventListener("animationend", () => {
          snowflake.remove();
        });
      }, 50); // Интервал создания снежинок
    }



    const makeButtonMove = (button) => {
      button.addEventListener("mouseover", () => {
        const boxRect = inviteBox.getBoundingClientRect();
        const x = Math.random() * (boxRect.width - button.clientWidth);
        const y = Math.random() * (boxRect.height - button.clientHeight);
        button.style.position = "absolute";
        button.style.left = `${x}px`;
        button.style.top = `${y}px`;
      });
    };

    [noButton, sickButton, examButton, busyButton, pelmeniButton, holostyakButton].forEach(makeButtonMove)
    //
    makeButtonMove(noButton);
    makeButtonMove(sickButton);
    makeButtonMove(examButton);

    makeButtonMove(busyButton);
    makeButtonMove(pelmeniButton);
    pelmeniButton(holostyakButton);


    noButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("Жаль, но я понял.");
    });

    sickButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("Выздоравливай");
    });

    examButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("Удачи на экзаменах!");
    });

// 
    busyButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("До следушего раза!");
    });

    pelmeniButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("Приятного аппетита!");
    });

    holostyakButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      alert("Приятного просмотра!");
    });




//
SvoyButton.addEventListener("click", () => {
  inviteBox.classList.add("hidden");
  formBox.classList.remove("hidden");
  startHearts();
  startSnowflakes();
  const email = "kiril20112004@gmail.com";
  const subject = "Прости, я не могу";
  const body = "Я не могу и вот почему: ";
  const mailtoLink = `https://mail.google.com/mail/?view=cm&fs=1&to=${email}&su=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
  window.location.href = mailtoLink;
});

 

    yesButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      formBox.classList.remove("hidden");
      startHearts();
      startSnowflakes();
    });

    sendButton.addEventListener("click", () => {
      const date = document.getElementById("date").value;
      const time = document.getElementById("time").value;

      if (!date || !time) {
        alert("Пожалуйста, выберите дату и время.");
        return;
      }

      const email = "kiril20112004@gmail.com";
      const subject = "Запрос на свидание";
      const body = `Выбрана дата свидания: ${date}, время: ${time}`;
      const mailtoLink = `https://mail.google.com/mail/?view=cm&fs=1&to=${email}&su=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
      window.location.href = mailtoLink;
    });
  </script>
</body>
</html>
