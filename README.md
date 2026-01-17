<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Thi Vật Lí – Bắc Ninh 2026</title>
<style>
body{font-family:Arial;max-width:900px;margin:auto}
.question{margin-bottom:18px;padding:10px;border-bottom:1px solid #ccc}
#timer{font-size:22px;color:red;font-weight:bold}
.lock{pointer-events:none;opacity:0.6}
</style>
</head>

<body>
<h2 style="text-align:center">PHẦN I – TRẮC NGHIỆM (18 CÂU)</h2>
<p>Thời gian còn lại: <span id="timer">15:00</span></p>

<form id="quiz"></form>
<button onclick="submitQuiz()">Nộp bài</button>
<h3 id="result"></h3>

<script>
const data = [
{
q:"Câu 1: Cung cấp nhiệt lượng 120 J cho một khối khí trong xi lanh, khí nở ra và thực hiện công 90 J. Độ biến thiên nội năng của khối khí là",
a:["A. −30 J","B. 210 J","C. 30 J","D. −20 J"], c:"C"
},
{
q:"Câu 2: Ở Nam Cực, nhiệt độ bề mặt lớp băng là −32°C. Trong thang Kelvin, nhiệt độ này là",
a:["A. 305 K","B. 273 K","C. 241 K","D. 32 K"], c:"C"
},
{
q:"Câu 3: Công thức tính nhiệt nóng chảy riêng của chất rắn là",
a:["A. λ = 1/Qm","B. λ = Q/m","C. λ = m/Q","D. λ = Qm"], c:"B"
},
{
q:"Câu 4: Bề mặt ngoài cốc nước lạnh bị ướt là do",
a:["A. Hơi nước trong không khí ngưng tụ",
   "B. Thành cốc nóng chảy",
   "C. Nước thấm qua cốc",
   "D. Nước trong cốc bay hơi"], c:"A"
},
{
q:"Câu 5: Mỗi độ chia 1°C trong thang Celsius bằng bao nhiêu khoảng cách giữa nhiệt độ nóng chảy và sôi của nước?",
a:["A. 273/100","B. 1/100","C. 100/273","D. 1/273"], c:"B"
},
{
q:"Câu 6: Phát biểu nào sau đây sai khi nói về khí lí tưởng?",
a:["A. Có thể bỏ qua khối lượng phân tử",
   "B. Phân tử coi là chất điểm",
   "C. Chuyển động thẳng đều",
   "D. Va chạm đàn hồi"], c:"A"
},
{
q:"Câu 7: Nén đẳng nhiệt một khối khí lí tưởng thì",
a:["A. Áp suất tăng","B. Mật độ giảm","C. Áp suất giảm","D. Khối lượng riêng không đổi"], c:"A"
},
{
q:"Câu 8: Nội năng đồng xu biến đổi do thực hiện công khi",
a:["A. Phơi nắng","B. Cọ xát đồng xu xuống sàn",
   "C. Đốt bằng bếp","D. Nhúng nước nóng"], c:"B"
},
{
q:"Câu 9: Nội năng của một vật là",
a:["A. Tổng động năng các phân tử",
   "B. Tổng động năng của vật",
   "C. Tổng thế năng các phân tử",
   "D. Tổng động năng và thế năng các phân tử"], c:"D"
},
{
q:"Câu 10: Động năng tịnh tiến trung bình của một phân tử khí là",
a:["A. 3/2 kT²","B. 1/3 kT²","C. 3/2 kT","D. 1/3 kT"], c:"C"
},
{
q:"Câu 11: Quá trình đẳng áp, nhiệt độ tăng hai lần thì thể tích",
a:["A. Tăng hai lần","B. Giảm hai lần","C. Tăng bốn lần","D. Giảm bốn lần"], c:"A"
},
{
q:"Câu 12: Đơn vị SI của nhiệt hóa hơi riêng là",
a:["A. J","B. J/kg·K","C. J/K","D. J/kg"], c:"D"
},
{
q:"Câu 13: Mạt sắt tập trung nhiều nhất ở",
a:["A. Dưới hai cực","B. Mọi điểm",
   "C. Trên hai cực","D. Giữa hai cực"], c:"D"
},
{
q:"Câu 14: Nhiệt độ không tuyệt đối là",
a:["A. 100°C","B. 273,16 K","C. 0 K","D. 0°C"], c:"C"
},
{
q:"Câu 15: Đại lượng cho biết nhiệt lượng cần để tăng 1 kg chất lên 1 K là",
a:["A. Nhiệt nóng chảy","B. Nhiệt hóa hơi",
   "C. Nhiệt dung riêng","D. Nhiệt độ nóng chảy"], c:"C"
},
{
q:"Câu 16: Trên đồ thị p–V, quá trình (1→2) là",
a:["A. Đẳng nhiệt","B. Đẳng áp","C. Đẳng tích","D. Đẳng nhiệt nén"], c:"A"
},
{
q:"Câu 17: Phát biểu sai về chất lỏng là",
a:["A. Dao động quanh vị trí cân bằng",
   "B. Thể tích xác định",
   "C. Lực tương tác lớn hơn chất rắn",
   "D. Không có hình dạng riêng"], c:"C"
},
{
q:"Câu 18: Phương trình Clapeyron là",
a:["A. TV = 2Rp","B. pV = nR/T",
   "C. pV = n/RT","D. pV = nRT"], c:"D"
}
];

const quiz=document.getElementById("quiz");
data.forEach((x,i)=>{
  let html=`<div class="question"><b>${x.q}</b><br>`;
  x.a.forEach((o,j)=>{
    const v=String.fromCharCode(65+j);
    html+=`<label><input type="radio" name="q${i}" value="${v}"> ${o}</label><br>`;
  });
  html+="</div>";
  quiz.innerHTML+=html;
});

let t=900;
const timer=document.getElementById("timer");
const cd=setInterval(()=>{
  let m=Math.floor(t/60),s=t%60;
  timer.textContent=`${m}:${s.toString().padStart(2,"0")}`;
  t--;
  if(t<0){clearInterval(cd);submitQuiz();}
},1000);

function submitQuiz(){
  clearInterval(cd);
  let score=0;
  data.forEach((x,i)=>{
    const c=document.querySelector(`input[name="q${i}"]:checked`);
    if(c&&c.value===x.c) score++;
  });
  quiz.classList.add("lock");
  result.innerText=`Đúng ${score}/18 câu – Điểm ${(score/18*10).toFixed(2)}`;
}
</script>
</body>
</html>
