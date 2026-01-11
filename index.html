<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- 캐시 방지 -->
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate">
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Expires" content="0">

<title>머더 역할 + 능력 추첨기</title>

<style>
/* ===== 전체 배경 ===== */
body {
  font-family: Arial, sans-serif;
  background:
    radial-gradient(circle at top, #2b2b2b 0%, #121212 60%),
    repeating-linear-gradient(
      45deg,
      rgba(255,255,255,0.03),
      rgba(255,255,255,0.03) 2px,
      transparent 2px,
      transparent 6px
    );
  margin: 0;
  padding: 20px;
  text-align: center;
  color: black;
}

/* ===== 제목 ===== */
h1 {
  font-size: clamp(24px, 6vw, 36px);
  margin-bottom: 25px;
  color: white;
}

/* ===== 입력 & 버튼 ===== */
input[type=number] {
  padding: 12px;
  font-size: 18px;
  width: 90px;
  text-align: center;
  border-radius: 10px;
  border: none;
}

button {
  padding: 16px 30px;
  margin: 14px;
  font-size: clamp(16px, 4.5vw, 20px);
  cursor: pointer;
  border-radius: 14px;
  border: none;
}

/* ===== 영역 ===== */
#menu, #draw-area {
  margin-top: 40px;
}

#draw-area {
  color: white;
  font-size: 20px;
}

#result {
  display: none;
  background: white;
  padding: 36px 22px;
  border-radius: 20px;
  margin-top: 40px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.45);
}

/* ===== 텍스트 ===== */
#role, #skill {
  font-size: clamp(30px, 9vw, 48px);
  font-weight: bold;
  margin-bottom: 14px;
}

#desc {
  font-size: clamp(16px, 4.5vw, 20px);
  line-height: 1.4;
  margin-bottom: 30px;
}

/* ===== 역할 색상 ===== */
.role-murder { color: #FF1801; }
.role-sheriff { color: #3712FF; }
.role-doctor {
  color: #FFFFFF;
  -webkit-text-stroke: 1.5px black;
}
.role-citizen {
  color: #1BD51A; /* 무고한 초록 */
}

/* ===== 능력 색상 ===== */
.skill-yellow { color: #FFDC00; }
.skill-pink { color: #FB66FF; }

/* 총잡이 대각선 */
.skill-gunslinger {
  background: linear-gradient(45deg, #FF1801 50%, #3712FF 50%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  display: inline-block;
}
</style>
</head>

<body>

<h1>머더 역할 + 능력 추첨기</h1>

<div id="menu">
  <div style="color:white; font-size:18px; margin-bottom:12px;">
    인원 수 입력
  </div>
  <input type="number" id="playerCount" min="4" max="20" value="6">
  <br>
  <button onclick="startGame()">시작</button>
</div>

<div id="draw-area" style="display:none;">
  <div id="playerNum"></div>
  <button onclick="draw()">뽑기</button>
</div>

<div id="result">
  <div id="role"></div>
  <div id="skill"></div>
  <div id="desc"></div>
  <button onclick="nextPlayer()">다음</button>
</div>

<script>
const skills = {
  머더: [
    { name: "방탄", desc: "한 번 공격을 버팁니다.(2목숨)" },
    { name: "가방", desc: "죽인 대상이 살아있는 것처럼 행동하다가 마지막에 사망합니다.(1명)" },
    { name: "총잡이", desc: "보안관과 같은 방식으로 처치합니다.", special: "gunslinger" },
    { name: "무능력", desc: "능력이 없습니다." },
    { name: "무능력", desc: "능력이 없습니다." }
  ],
  보안관: [
    { name: "강인한", desc: "목숨이 2개가 됩니다." },
    { name: "마피아", desc: "머더와 모든 시민을 제거하면 즉시 승리합니다.", special: "yellow" },
    { name: "무능력", desc: "능력이 없습니다." },
    { name: "무능력", desc: "능력이 없습니다." }
  ],
  의사: [
    { name: "자가치유", desc: "자신을 치료할 수 있습니다.(1회)" },
    { name: "전문 의사", desc: "최대 2명까지 치료할 수 있습니다." },
    { name: "구급상자", desc: "생존자 1명에게 미리 지급해 스스로 치료하게 합니다." },
    { name: "무능력", desc: "능력이 없습니다." }
  ],
  시민: [
    { name: "스파이", desc: "시민/보안관을 죽일수록 최대 2목숨까지 증가합니다. 머더를 죽이면 자신도 사망하며 시민 승리.", special: "yellow" },
    { name: "퍼블win", desc: "가장 먼저 머더에게 죽으면 즉시 시민 승리.", special: "pink" },
    { name: "패링", desc: "한 번 공격을 막아냅니다." },
    { name: "무능력", desc: "능력이 없습니다." }
  ]
};

let totalPlayers = 0;
let current = 0;
let roles = [];
let usedCitizenSpecials = [];

function startGame() {
  totalPlayers = parseInt(document.getElementById("playerCount").value);
  if (isNaN(totalPlayers) || totalPlayers < 4) {
    alert("최소 4명 이상 필요합니다.");
    return;
  }

  roles = ["머더", "보안관", "의사"];
  for (let i = 4; i <= totalPlayers; i++) roles.push("시민");
  roles.sort(() => Math.random() - 0.5);

  current = 0;
  usedCitizenSpecials = [];

  document.getElementById("menu").style.display = "none";
  document.getElementById("draw-area").style.display = "block";
  document.getElementById("playerNum").textContent = "플레이어 1";
}

function draw() {
  const role = roles[current];
  let chosen;

  if (role === "시민") {
    const specials = skills.시민.filter(
      s => s.special && !usedCitizenSpecials.includes(s.name)
    );

    if (specials.length > 0 && usedCitizenSpecials.length < 2 && Math.random() < 0.5) {
      chosen = specials[Math.floor(Math.random() * specials.length)];
      usedCitizenSpecials.push(chosen.name);
    } else {
      chosen = skills.시민.find(s => s.name === "무능력");
    }
  } else {
    const list = skills[role];
    chosen = list[Math.floor(Math.random() * list.length)];
  }

  const roleDiv = document.getElementById("role");
  const skillDiv = document.getElementById("skill");
  const descDiv = document.getElementById("desc");

  roleDiv.textContent = role;
  roleDiv.className =
    role === "머더" ? "role-murder" :
    role === "보안관" ? "role-sheriff" :
    role === "의사" ? "role-doctor" :
    "role-citizen";

  skillDiv.textContent = chosen.name;
  skillDiv.className = "";
  if (chosen.special === "yellow") skillDiv.className = "skill-yellow";
  if (chosen.special === "pink") skillDiv.className = "skill-pink";
  if (chosen.special === "gunslinger") skillDiv.className = "skill-gunslinger";

  descDiv.textContent = chosen.desc;

  document.getElementById("draw-area").style.display = "none";
  document.getElementById("result").style.display = "block";
}

function nextPlayer() {
  current++;
  if (current >= totalPlayers) {
    alert("모든 플레이어 추첨 완료. 초기화됩니다.");
    location.reload();
    return;
  }

  document.getElementById("result").style.display = "none";
  document.getElementById("draw-area").style.display = "block";
  document.getElementById("playerNum").textContent = `플레이어 ${current + 1}`;
}
</script>

</body>
</html>
