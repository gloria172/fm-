# fm
theboyz上海福利模拟器
<!DOCTYPE html><html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>THE BOYZ 见面会福利抽选模拟器</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Microsoft YaHei", sans-serif;
      background: #f6f7f9;
      padding: 20px;
    }
    .card {
      max-width: 520px;
      margin: 0 auto;
      background: #fff;
      border-radius: 16px;
      padding: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.08);
    }
    h1 {
      text-align: center;
      margin-bottom: 16px;
    }
    select, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      font-size: 16px;
    }
    button {
      border: none;
      border-radius: 8px;
      background: #111;
      color: #fff;
      cursor: pointer;
    }
    button:hover {
      opacity: 0.9;
    }
    .result {
      margin-top: 16px;
      font-size: 18px;
      text-align: center;
      font-weight: bold;
    }
    .note {
      margin-top: 12px;
      font-size: 12px;
      color: #666;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>THE BOYZ 福利抽选模拟器</h1><label>选择票档</label>
<select id="tier">
  <option value="VIP">VIP（1980）</option>
  <option value="A">A档（1280）</option>
  <option value="B">B档（480）</option>
</select>

<label>选择成员</label>
<select id="member">
  <option>Jacob</option>
  <option>泳勋</option>
  <option>贤在</option>
  <option>柱延</option>
  <option>Kevin</option>
  <option>New</option>
  <option>Q</option>
  <option>善旴</option>
  <option>Eric</option>
</select>

<button onclick="draw()">开始抽选</button>

<div class="result" id="result"></div>
<div class="note">* 本模拟器为规则模拟与情绪安慰用途，不代表真实结果</div>

  </div><script>
const members = ["Jacob","泳勋","贤在","柱延","Kevin","New","Q","善旴","Eric"];

const config = {
  VIP: {
    total: 900,
    gm: 280,
    v10: 470,
    polaroid: 50
  },
  A: {
    total: 600,
    gm: 80,
    v10: 130,
    v20: 220,
    polaroid: 30
  },
  B: {
    total: 900,
    polaroid: 10,
    poster: 150
  }
};

function chance(hit, total) {
  return Math.random() < hit / total;
}

function draw() {
  const tier = document.getElementById("tier").value;
  const member = document.getElementById("member").value;
  let res = "很遗憾，没有抽到福利";

  if (tier === "VIP") {
    const gmPerMember = config.VIP.gm / members.length;
    if (chance(gmPerMember, config.VIP.total)) {
      res = `🎉 GM（1v1） - ${member}`;
    } else if (chance(config.VIP.v10, config.VIP.total)) {
      res = "🎉 TBZ v10";
    } else {
      res = "🎉 TBZ v20";
    }
    if (chance(config.VIP.polaroid, config.VIP.total)) {
      res += " + 📸 拍立得";
    }
  }

  if (tier === "A") {
    const gmPerMember = config.A.gm / members.length;
    if (chance(gmPerMember, config.A.total)) {
      res = `🎉 GM（1v1） - ${member}`;
    } else if (chance(config.A.v10, config.A.total)) {
      res = "🎉 TBZ v10";
    } else if (chance(config.A.v20, config.A.total)) {
      res = "🎉 TBZ v20";
    }
    if (chance(config.A.polaroid, config.A.total)) {
      res += " + 📸 拍立得";
    }
  }

  if (tier === "B") {
    if (chance(config.B.polaroid, config.B.total)) {
      res = "🎉 签名拍立得";
    } else if (chance(config.B.poster, config.B.total)) {
      res = "🎉 签名海报";
    }
  }

  document.getElementById("result").innerText = res;
}
</script></body>
</html>
