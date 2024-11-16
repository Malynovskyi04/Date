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
      width: 350px;
      height: 350px;
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

    const startHearts = () => {
      setInterval(() => {
        const heart = document.createElement("div");
        heart.classList.add("heart");
        heart.textContent = "💜";
        heart.style.left = `${Math.random() * 100}vw`;
        heart.style.animationDuration = `${Math.random() * 3 + 2}s`;
        document.body.appendChild(heart);
        heart.addEventListener("animationend", () => heart.remove());
      }, 100);
    };

    const startSnowflakes = () => {
      setInterval(() => {
        const snowflake = document.createElement("div");
        snowflake.classList.add("snowflake");
        snowflake.textContent = ["❄", "❅", "❆"][Math.floor(Math.random() * 3)];
        snowflake.style.left = `${Math.random() * 100}vw`;
        snowflake.style.animationDuration = `${Math.random() * 3 + 2}s`;
        document.body.appendChild(snowflake);
        snowflake.addEventListener("animationend", () => snowflake.remove());
      }, 100);
    };

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

    [noButton, sickButton, examButton, pelmeniButton, holostyakButton].forEach(makeButtonMove);

    yesButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      formBox.classList.remove("hidden");
      startHearts();
      startSnowflakes();
    });

    sendButton.addEventListener("click", () =>
    {
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

    // talant code 
    busyButton.addEventListener("okay", () =>
    {
     
      const email = "kiril20112004@gmail.com";
      const subject = "Запрос на свидание";
      const body = `Выбрана дата свидания:`;
      const mailtoLink = `https://mail.google.com/mail/?view=cm&fs=1&to=${email}&su=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
      window.location.href = mailtoLink;
    });

  </script>
</body>
</html>
