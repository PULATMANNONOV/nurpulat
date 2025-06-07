# nurpulat
ombor test
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>2-test: Koreyscha so‘zlar testi</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 700px;
      margin: auto;
      background: #fff;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      margin-bottom: 25px;
    }
    .question {
      font-size: 18px;
      margin-bottom: 15px;
    }
    .answers button {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 12px;
      font-size: 16px;
      border: 2px solid #ccc;
      border-radius: 8px;
      background: #f9f9f9;
      cursor: pointer;
      transition: all 0.3s;
    }
    .answers button:hover {
      background: #eef;
    }
    .answers button.correct {
      background-color: #c8f7c5;
      border-color: #4CAF50;
    }
    .answers button.wrong {
      background-color: #f9c0c0;
      border-color: #f44336;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>2-test: Koreyscha so‘zlar bo‘yicha test</h2>
    <div id="quiz">
      <div class="question" id="question"></div>
      <div class="answers" id="answers"></div>
    </div>
  </div>

  <script>
    const questions = [
      {
        question: "1. Bo‘lim boshlig‘i o‘rinbosari qanday deyiladi?",
        options: ["지도사님", "과장님", "책임자", "직장님"],
        correct: "과장님"
      },
      {
        question: "2. Quloq pinning koreyschasi?",
        options: ["안전화", "귀마개", "작업복", "가방"],
        correct: "귀마개"
      },
      {
        question: "3. “Kabel yo‘lak” koreys tilida?",
        options: ["코밍", "케이블 태그", "에프 비(플랫 바)", "배선"],
        correct: "배선"
      },
      {
        question: "4. “Rahmat” so‘zi koreys tilida qanday?",
        options: ["감사합니다", "네, 알겠습니다", "아니요", "네"],
        correct: "감사합니다"
      },
      {
        question: "5. “Kran” so‘zi koreys tilida?",
        options: ["드럼", "스타 카드", "크레인", "지게차"],
        correct: "크레인"
      },
      {
        question: "6. “Shim” koreys tilida qanday?",
        options: ["콜티", "바지", "안전 밸트", "작업복"],
        correct: "바지"
      },
      {
        question: "7. “O‘g‘irlikdan saqlanish” koreys tilida?",
        options: ["제한 속도 30", "안전", "금지", "위험"],
        correct: "금지"
      },
      {
        question: "8. “Ofis” so‘zi koreys tilida?",
        options: ["배선반", "코밍", "사무실", "작업복"],
        correct: "사무실"
      },
      {
        question: "9. “Yaxshi ishlang” degan so‘z?",
        options: ["수고하세요", "고생하셨습니다", "안녕하세요", "감사합니다"],
        correct: "수고하세요"
      },
      {
        question: "10. “Lesa (ish stoli)” koreys tilida qanday?",
        options: ["족장", "조장", "반장님", "프로님"],
        correct: "족장"
      },
      {
        question: "11. “Kabel boylagich” so‘zi koreys tilida?",
        options: ["케이블 태그", "배선", "케이블타이", "에프 비(플랫 바)"],
        correct: "케이블타이"
      },
      {
        question: "12. “Narvon” koreys tilida qanday?",
        options: ["사다리", "지게차", "우마", "크레인"],
        correct: "사다리"
      },
      {
        question: "13. “Chekish mumkin emas” so‘zining koreyschasi?",
        options: ["품연 금지", "금지", "흡연 구역", "접근 금지"],
        correct: "품연 금지"
      },
      {
        question: "14. “Maska” so‘zi koreys tilida?",
        options: ["콜티", "작업복", "마스크", "안전모"],
        correct: "마스크"
      },
      {
        question: "15. “Payvandlash” so‘zining koreyschasi?",
        options: ["배선", "용접", "결선", "계장"],
        correct: "용접"
      },
      {
        question: "16. “Mini narvoncha” koreys tilida qanday?",
        options: ["지게차", "사다리", "우마", "크레인"],
        correct: "우마"
      },
      {
        question: "17. “Qaychi” so‘zining koreyschasi?",
        options: ["가위", "도면", "작업복", "귀마개"],
        correct: "가위"
      },
      {
        question: "18. “Sifat nazoratchisi” so‘zi koreys tilida?",
        options: ["과장님", "책임자", "지도사님", "관리자"],
        correct: "관리자"
      },
      {
        question: "19. “Qolingiz yaxshi” so‘zining koreyschasi?",
        options: ["감사합니다", "안녕하세요", "안녕히 가세요", "안녕히 계세요"],
        correct: "안녕히 계세요"
      },
      {
        question: "20. “Truba montaji” so‘zining koreyschasi?",
        options: ["배선", "계장", "배선반", "결선"],
        correct: "계장"
      },
    ];

    let current = 0;

    function showQuestion() {
      const q = questions[current];
      document.getElementById("question").textContent = q.question;

      const shuffled = [...q.options].sort(() => Math.random() - 0.5);
      const answersDiv = document.getElementById("answers");
      answersDiv.innerHTML = "";

      shuffled.forEach(option => {
        const btn = document.createElement("button");
        btn.textContent = option;
        btn.onclick = () => {
          if (option === q.correct) {
            btn.classList.add("correct");
            setTimeout(() => {
              current++;
              if (current < questions.length) {
                showQuestion();
              } else {
                document.getElementById("quiz").innerHTML = "<h3>Barcha savollarga javob berdingiz!</h3>";
              }
            }, 800);
          } else {
            btn.classList.add("wrong");
          }
        };
        answersDiv.appendChild(btn);
      });
    }

    showQuestion();
  </script>
</body>
</html>
