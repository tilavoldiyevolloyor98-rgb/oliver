[index.html](https://github.com/user-attachments/files/28307220/index.html)
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Umumiy Psixologiya Testi</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:system-ui,sans-serif;background:#f5f5f3;min-height:100vh;display:flex;align-items:flex-start;justify-content:center;padding:2rem 1rem}
#app{background:#fff;border-radius:16px;border:1px solid #e0e0d8;padding:2rem;width:100%;max-width:640px}
#header{display:flex;align-items:center;justify-content:space-between;margin-bottom:1rem;flex-wrap:wrap;gap:8px}
#title{font-size:15px;font-weight:500;color:#111}
#stats{display:flex;gap:12px;font-size:13px;color:#666}
.stat{display:flex;align-items:center;gap:4px}
#progress-bar{height:4px;background:#e8e8e4;border-radius:2px;margin-bottom:1.5rem;overflow:hidden}
#progress-fill{height:100%;background:#1D9E75;border-radius:2px;transition:width 0.3s}
#q-counter{font-size:12px;color:#999;margin-bottom:0.5rem}
#question{font-size:16px;font-weight:500;color:#111;line-height:1.6;margin-bottom:1.25rem}
#options{display:flex;flex-direction:column;gap:8px;margin-bottom:1.25rem}
.opt{display:flex;align-items:flex-start;gap:10px;padding:12px 14px;border:1px solid #e0e0d8;border-radius:10px;cursor:pointer;transition:all 0.15s;background:#fff;text-align:left;width:100%}
.opt:hover:not(:disabled){border-color:#bbb;background:#f9f9f7}
.opt-letter{width:24px;height:24px;border-radius:50%;background:#f0f0ec;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:500;color:#666;flex-shrink:0;transition:all 0.15s}
.opt-text{font-size:14px;line-height:1.5;color:#222;padding-top:2px}
.opt.correct{border-color:#0F6E56;background:#E1F5EE}
.opt.correct .opt-letter{background:#1D9E75;color:#fff}
.opt.wrong{border-color:#993C1D;background:#FAECE7}
.opt.wrong .opt-letter{background:#D85A30;color:#fff}
.opt.faded{opacity:0.4}
.opt:disabled{cursor:default}
#feedback{font-size:13px;padding:10px 14px;border-radius:10px;margin-bottom:1rem;display:none}
#feedback.show{display:block}
#feedback.correct-fb{background:#E1F5EE;color:#085041}
#feedback.wrong-fb{background:#FAECE7;color:#4A1B0C}
#next-btn,#restart-btn,#start-btn{padding:10px 22px;border-radius:10px;font-size:14px;cursor:pointer;border:1px solid #ddd;background:#fff;color:#111;font-weight:500}
#next-btn:hover,#restart-btn:hover{background:#f5f5f3}
#start-btn{background:#1D9E75;color:#fff;border:none;font-size:15px;padding:12px 28px}
#start-btn:hover{background:#0F6E56}
#results{display:none;padding:1rem 0;text-align:center}
#results.show{display:block}
#score-circle{width:100px;height:100px;border-radius:50%;background:#f5f5f3;display:flex;flex-direction:column;align-items:center;justify-content:center;margin:0 auto 1.25rem;border:1px solid #e0e0d8}
#score-num{font-size:28px;font-weight:600;color:#111}
#score-den{font-size:13px;color:#888}
#results h2{font-size:20px;font-weight:600;margin-bottom:0.5rem}
#results p{font-size:14px;color:#666;margin-bottom:1.5rem}
.results-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:1.5rem}
.res-card{background:#f5f5f3;border-radius:10px;padding:12px}
.res-card .rc-num{font-size:22px;font-weight:600;margin-bottom:2px}
.res-card .rc-label{color:#888;font-size:12px}
.rc-correct .rc-num{color:#0F6E56}
.rc-wrong .rc-num{color:#993C1D}
.mode-btns{display:flex;gap:8px;margin-bottom:1.25rem;flex-wrap:wrap}
.mode-btn{padding:7px 16px;border-radius:8px;font-size:13px;cursor:pointer;border:1px solid #ddd;background:#fff;color:#666}
.mode-btn.active{background:#E1F5EE;color:#085041;border-color:#9FE1CB;font-weight:500}
#start-screen h2{font-size:20px;font-weight:600;margin-bottom:0.5rem;color:#111}
#start-screen p{font-size:14px;color:#666;margin-bottom:1.25rem;line-height:1.6}
.badge{display:inline-block;background:#f0f0ec;color:#555;font-size:12px;padding:3px 10px;border-radius:20px;margin-bottom:1rem}
</style>
</head>
<body>
<div id="app">

  <div id="start-screen">
    <div class="badge">📚 100 ta savol</div>
    <h2>Umumiy Psixologiya Testi</h2>
    <p>Psixologiya fanidan bilimingizni sinab ko'ring. Nechtasini ishlashni xohlaysiz?</p>
    <div class="mode-btns">
      <button class="mode-btn active" data-n="10">10 ta</button>
      <button class="mode-btn" data-n="20">20 ta</button>
      <button class="mode-btn" data-n="50">50 ta</button>
      <button class="mode-btn" data-n="100">Barchasi</button>
    </div>
    <button id="start-btn">Boshlash →</button>
  </div>

  <div id="quiz-body" style="display:none">
    <div id="header">
      <div id="title">Umumiy Psixologiya</div>
      <div id="stats">
        <div class="stat">✅ <span id="correct-count">0</span></div>
        <div class="stat">❌ <span id="wrong-count">0</span></div>
      </div>
    </div>
    <div id="progress-bar"><div id="progress-fill"></div></div>
    <div id="q-counter"></div>
    <div id="question"></div>
    <div id="options"></div>
    <div id="feedback"></div>
    <div><button id="next-btn" style="display:none">Keyingisi →</button></div>
  </div>

  <div id="results">
    <div id="score-circle">
      <div id="score-num"></div>
      <div id="score-den"></div>
    </div>
    <h2 id="results-title"></h2>
    <p id="results-msg"></p>
    <div class="results-grid">
      <div class="res-card rc-correct"><div class="rc-num" id="r-correct"></div><div class="rc-label">To'g'ri</div></div>
      <div class="res-card rc-wrong"><div class="rc-num" id="r-wrong"></div><div class="rc-label">Noto'g'ri</div></div>
      <div class="res-card"><div class="rc-num" id="r-pct"></div><div class="rc-label">Foiz</div></div>
    </div>
    <button id="restart-btn">Qayta boshlash</button>
  </div>

</div>
<script>
const ALL_Q=[{"q":"Psixologiya fani nimani о'rganadi?","a":["Psixik faktlar va uning mexanizmlari, onuniyatlari haqidagi fan","Xayvonot dunyosida psixika paydo bо'lishining psixologik qonuniyatlarini","Psixik jarayonlar, dalillar va yuzaga kelish mexanizmlarini va ularning taraqqiyot qonunlarini","Psixik hayotning filogenetik taraqqiyotini"],"c":0},{"q":"Psixologiya fan sohalarini tasniflab 3 guruhga ajiratgan olim qaysi qatorda to'g'ri ko'rsatilgan?","a":["A.V.Petrovskiy","V.Karimova","E.G'oziyev","K.D.Ushiniskiy"],"c":0},{"q":"Qachon psixologiya fani falsafa fanidan mustaqil fan bо'lib ajralib chiqdi?","a":["XIX asrda","XX asr о'rtasida","XVII asr oxirida","XX asr boshida"],"c":0},{"q":"Bilish jarayonlari qaysi qatorda tо'g'ri kо'rsatilgan?","a":["Sezgi, idrok, xayol, xotira, tafakkur","Iroda, xissiyot, tafakkur, iroda, temperament","Idrok, sezgi, qobiliyat, iroda, tafakkur","Qobiliyat, nutq, xayol, idrok tafakkur"],"c":0},{"q":"\"Dualizm\" oqimining asoschisi qaysi qatorda to'g'ri ko'rsatilgan?","a":["Platon","Geraklit","Demokrit","Fales"],"c":0},{"q":"Jon о'z mohiyatiga kо'ra olovsimon uchqundan iboratligini ilgari surgan olim?","a":["Geraklit","Aflotun","Demokrit","Arastu"],"c":0},{"q":"Psixikaning eng yuksak darajasi bo'lib u, faqat insongagina xosdir?","a":["Ong","Psixika","Ongsizlik","Tafakkur"],"c":0},{"q":"Ong nima?","a":["Psixikaning eng yuksak darajasi bo'lib u faqat insongagina xosdir","Ong -ijtimoiy muhit mahsuli","Ong - insonning о'z oldiga aniq maqsad kо'yib, faoliyat kо'rsatishidir","Ong -mehnat faoliyati jarayoni va natijasi"],"c":0},{"q":"Psixika nima?","a":["Yuksak darajada tashkil topgan materiyaning obyektiv voqelikni aks ettirishdan iborat","Psixika dunyoni umumlashtirib aks ettirish xususiyati","Psixika bizning sezgilarimiz, fikr va mulohazalarimiz, kechinmalarimizdir","Psixika narsa va xodisalarning uhim xususiyatidir"],"c":0},{"q":"Refleks nima?","a":["Organizmning tashqi muhit ta'siriga nerv tizimi orqali beradigan javob reaksiyasi","Bu insonga xos aks ettirish","Tirik organizmning javob reaksiyasi","Bu insonga xos aks ettirish"],"c":0},{"q":"Ong va faoliyat bir-biriga qarama-qarshi ham aynan bir narsa emas ular bir butunlikni tashkil etadi?","a":["Ong va faoliyat birligi","Determinizm","Ongni faoliyatda rivojlanishi","Ong psixikada rivojlanishi"],"c":0},{"q":"Muloqot – bu...?","a":["Ikki yoki undan ortiq kishilar o'rtasidagi axborot ayirboshlash o'zaro ta'sir va bir-birini tushunishdan iborat jarayon","Insonning amaliy va nazariy faoliyatini tashkil qilish usuli","E'tiqod, dunyoqarash va ideallarning shakllanish jarayoni","Bolalarda aqliy, axloqiy hislarning paydo bо'lish jarayoni"],"c":0},{"q":"Monologik nutq nima?","a":["Bir kishining o'ziga yoki boshqalarga qaratilgan nutqidir","Bir necha suhbatdoshlar о'rasidagi muloqot","Kishilar orasidagi о'zaro munosabat","Suhbatdoshga ta'sir kо'rsatish"],"c":0},{"q":"Faoliyat nima?","a":["Anglangan maqsad bilan boshqariladigan ichki (psixik) va tashqi (jismoniy) harakatlar","Maqsadlarimiz mazmuni va uni bajarish usuli","Kо'nikma va malakalar jarayonining sodir bо'lishi","Bilishga bо'lgan extiyoj asosda shakllanadigan motivlar"],"c":0},{"q":"Kо'nikma bu…?","a":["Biror faoliyatni amalga oshirish uchun mavjud bilimlardan va malakalardan foydalana olish","Faoliyatda faollik kо'rsatish ish-harakatlar yig'indisi","Avtomatlashgan xarakatlar ish-harakatlar yig'indisi","Faoliyatda ish-harakatlar yig'indisi, avtomatlashgan xarakatlar yig'indisi"],"c":0},{"q":"Xozirgi zamon psixologiyasida shaxs faolligi manbai – bu?","a":["Ehtiyoj. Qiziqish","Ishtiyoq. Motiv","Jinsiy mayllar","Motiv. Ishtiyoq"],"c":0},{"q":"Avval ongli bajarib, keyinchalik avtomatlashgan xatti-harakatlarga nima aytiladi?","a":["Malaka","Ko'nikma","Odat","Motiv"],"c":0},{"q":"Motiv bu-…?","a":["Ehtiyojlarni qondirish bilan bog'liq bо'lgan faoliyatga undovchi kuch","Ehtiyojlarning hissiy namoyon bо'lishini aks ettiruvchi kechinmalari","Dо'stlik, о'rtoqlik, uyatchanlik, sevgi hissini aks ettiruvchi kechinmalari","Shaxsning ijtimoiy aks ettiruvchi ichki va tashqi kechinmalari"],"c":0},{"q":"Emotsiya bu -…?","a":["Ehtiyoj va qiziqishlar bilan bog'liq bо'lgan yoqimli va yoqimsiz kechinmalari","Ongimizning ma'lum narsa va hodisalarga yо'nalishi","Dо'stlik, о'rtoqlik, uyatchanlik, sevgi hissini aks ettiruvchi kechinmalari","Shaxsning ijtimoiy aks ettiruvchi ichki va tashqi kechinmalari"],"c":0},{"q":"Iroda ta'rifini aniqlang.","a":["Maqsadga erishishda qiyinchiliklarni, tо'siqlarni yengish bilan bog'liq bо'lgan ixtiyoriy, ongli harakat","Narsa va xodisalarning ayrim xususiyatlarini ongda aks ettirish jarayoni","Narsa va hodisalar о'rtasidagi munosabatlarning umumlashgan holda aks etishi jarayoni","Kishining ma'lum bir faoliyatni bajara olishga bо'lgan layoqatni aks etishi jarayoni"],"c":0},{"q":"Individuallik bu...?","a":["Ayrim psixologik jarayonlarning har bir shaxsning о'zigagina xos bо'lgan xususiyatlari","Chaqaloq, tilni va oddiy malakalarni о'zlashtira olmaydigan odam","Shaxs psixologik xususiyatlarining qaytarilmaydigan birikmasi","Shaxsning hayot davomida orttirgan tajribasi"],"c":0},{"q":"Diqqatning ta'rifi qaysi javobda tо'g'ri berilgan?","a":["Ongni bir nuqtaga to'plab, muayyan bir obyektga faol qaratilishini aytamiz","Narsa va hodisalarni umumlashtirib aks etgirish","Har qanday faoliyatning zaruriy sharti","Narsa va xodisalarni yaxlit aks ettirish"],"c":0},{"q":"Sezgi – bu...?","a":["Atrofimizdagi narsa va hodisalarning sezgi a'zolarimizga bevosita ta'sir etishi natijasida ularning ayrim belgi va xususiyatlarini miyamizda aks ettirilishini aytamiz.","Narsalarning muhim belgi va xususiyatlarini yaxlit aks ettirish","Dunyoni umumlashtirib aks ettirish","Sezish jarayonida tug'iladigan xush va noxush tuyg'ularni aks etgirish"],"c":0},{"q":"Qorni ochlikni, chanqashni sezish qaysi sezgi turiga oid?","a":["Organik sezgi","To'yish sezgi","Eshitish sezgi","Teri sezgi"],"c":0},{"q":"Analizator – bu...?","a":["Tashqi va ichki muhitdan keladigan ta'sirotlarni qabul qilib olib, fiziologik jarayon bo'lgan qo'zg'alishni psixik jarayonga, ya'ni sezgilarga aylantiruvchi nerv mexanizmlari tizimi.","Sezgi a'zolarining bir turi afferent nerv, retseptor","Afferent nerv, retseptor, maxsus markaz","Bosh miya pо'stidagi maxsus markaz"],"c":0},{"q":"Idrok ta'rifini aniqlang?","a":["Sezgi a'zolariga bevosita ta'sir etib turgan narsa-hodisalar obrazlarini kishi ongida bir butun holda aks ettirilishiga aytiladi","Butun organizmdagi sezgilar yig'indisini aks ettirish","Narsa va hodisalarning muhim belgi va xususiyatlarini yaxlit aks ettirish","Voqelikni ilgari egallagan tajriba va malakalar asosida aks ettirish"],"c":0},{"q":"Gallyutsinatsiya - bu ...?","a":["Inson ongida turli obrazlarning xayolan, fikran paydo bo'lishidan iborat idrokning psixopatalogik hodisasi","Bor narsani to'g'ri idrok qilish","Shaxsning idrok qilish qobiliyati","Idrokning shaxs va uning tajribasiga bog'liqligi"],"c":0},{"q":"Narsa va hodisalarni, uni ayni paytda idrok qilmay esga tushirish…….?","a":["Eslash","Esga tushirish","Bevosita esga tushirish","Vaqt o'tkazib eslash"],"c":0},{"q":"O'tmishda idrok qilingan narsalarning ongimizda qayta tiklanishi deb ataladi?","a":["Esga tushirish","Bevosita tushirish","Vaqt o'tkazib esga tushirish","Vaqt o'tkazmay tushirish"],"c":0},{"q":"Beixtiyor esda qoldirishda qaysi jarayon asosiy rol o'ynaydi?","a":["Qiziqish","Hajmi","Tajriba","Shakl"],"c":0},{"q":"Faoliyat turlari?","a":["O'yin, ta'lim, mehnat","Ijodiy ish jarayoni","Ta'lim-tarbiya jarayoni","Qiziqish, intilish, faollik kо'rsatish"],"c":0},{"q":"Hissiyot bu -...?","a":["Narsa va xodisalarga bо'lgan munosabatimiz va ulardan hosil bо'ladigan kechinmalarning ongda aks etishi","Inson psixikasining о'ziga xosligi va atrofidagilarga bо'lgan munosabatida namoyon bо'ladi","Narsa va xodisalarni, kechirilgan tuyg'u va hislarni esda qoldirish, esga tushirishdan iborat psixik jarayon","Kishining yashash sharoiti, ta'lim-tarbiyasi va atrofidagilarga bо'lgan munosabatida namoyon bо'ladi"],"c":0},{"q":"Idrok qanday psixik jarayon?","a":["Murakkab psixik jarayon","Oddiy psixik jarayon","Og'riqli psixik jarayon","Muvozanatli psixik jarayon"],"c":0},{"q":"Faoliyat maqsadiga ko'ra xotira turini aniqlang?","a":["Ixtiyoriy, ixtiyorsiz","Harakat, emotsional, obrazli","Qisqa va uzoq muddatli","Operativ, sо'z-mantiq"],"c":0},{"q":"Odam o'ziga hech qanday maqsad qo'ymasdan irodani ishga solmasdan obraz va tasavvurlar yaratishga nima aytiladi?","a":["Ixtiyorsiz xayol","Fantastik xayol","Ijodiy xayol","Tasavvur xayol"],"c":0},{"q":"Oldindan belgilangan maqsad asosida iroda kuchini ishga solib, muayyan obraz va tasavvurlarni yaratishga aytiladi?","a":["Ixtiyoriy xayol","Ixtiyorsiz xayol","Tasavvur xayol","Fantastik xayol"],"c":0},{"q":"Tafakkur bu-?","a":["Inson aqliy faoliyatining yuksak shaklidir","Insonning fikrlash faoliyati","Muammoli vaziyatni hal qilish","Ongda aks ettirilish."],"c":0},{"q":"Narsa va hodisalarni fikran yoki amaliy tahlil qiladigan tafakkur operasiyasi?","a":["Analiz","Taqqoslash","Klassifikasiya","Abstraksiyalash"],"c":0},{"q":"Analizda bo'lingan qismlarni fikran birlashtirib butun holiga keltiruvchi tafakkur operasiyasi?","a":["Sintez","Taqqoslash","Klassifikasiya","Abstraksiyalash"],"c":0},{"q":"Narsa va hodisalar haqida tasdiqlab yoki inkor qilib aytilgan fikr deb ataladi?","a":["Hukm","Abstraksiyalash","Tushuncha","Mavhumlashtirish"],"c":0},{"q":"Uzoq davom etadigan anchagina kuchli hissiy holatdir?","a":["Stress","Kayfiyat","Hissiyot","Extiros"],"c":0},{"q":"Stress so'zining ma'nosi nima?","a":["Inglizcha – zo'riqish","Lotincha – ichki xayajonlanish","Yunoncha – kuch","Yunoncha – zaiflik"],"c":0},{"q":"Odamning aqliy faoliyati bilan bog'liq hislar?","a":["Intellektual hislar","Axloqiy hislar","Estetik hislar","Praksik hislar"],"c":0},{"q":"Oldindan maqsad qo'yib, ongli ravishda zo'r berish natijasida voqe bo'ladigan faollik?","a":["Iroda","Stress","Affekt","Extiros"],"c":0},{"q":"Temperament so'zining ma'nosi?","a":["Lotincha «temperamentum» – aralashma demakdir","Turkcha «temperamentum» – aralashma demakdir","O'zbekcha «temperamentum» – aralashma demakdir","Arabcha «temperamentum» – aralashma demakdir"],"c":0},{"q":"Temperament haqidagi dastlabki ta'limot kim tomonidan yaratilgan?","a":["Gippokrat","Aritsotel","I.P.Pavlov","Demokrit"],"c":0},{"q":"Xolerik bu…?","a":["Kuchli, lekin muvozanatsiz, qo'zg'alish tormozlanishdan ustun chiqadigan, qizg'in, jo'shqin tip","Aktiv, harakatchan, ko'ngilsizliklarni yengil o'tkazib yuboruvchi tip","Yuragi keng, harakatlari va nutqi bir maromda bo'lgan tip","Ta'sirchan, chuqur kechinmalarga ega, gap ko'tara olmaydigan tip"],"c":0},{"q":"Xarakter-bu...?","a":["Shaxsda muhit va tarbiya ta'siri ostida tarkib topgan va uning irodaviy faolligida namoyon bo'ladigan individual xususiyat","Kishining xulq-atvorida namoyon bo'ladigan tug'ma xususiyat","Kishining xatti-harakatlarida namoyon bo'ladigan tug'ma xususiyat","Odamning mardlik, salobatlilik, rostgo'ylik ko'rsatishidagi yakka xususiyat"],"c":0},{"q":"O'zini suhbatdoshi o'rniga qo'yib uning kechinmalarini tushunishga intilish?","a":["Empatiya","Kommunikasiya","Steriotiplashtirish","Identifikasiya"],"c":0},{"q":"Inson tanasi yoki uning qismlari yordamida ifodalanadigan harakatlar tizimidir?","a":["Pantomimika","Jestlar","Astenik","Stenik"],"c":0},{"q":"Qobiliyatlar nimada namoyon bo'ladi?","a":["Faoliyat jarayonida","Yashash jarayonida","O'yinda","Ta'lim jarayonida"],"c":0},{"q":"Inson organizmining beshta asosiy tuyg'ulari?","a":["Ko'rish, eshitish, ta'm bilish, hid bilish va sezish","Diqqat, xotira, idrok, sezish","Xayol, tafakkur, eshitish","O'qish, yozish, ta'lim"],"c":0},{"q":"Xotira jarayonlari ko'rsatilgan qatorni toping?","a":["Esda olib qolish, esda saqlash, esga tushirish, unutish, tanish, eslash","Ixtiyoriy, ixtiyorsiz","Obrazli, mantiqiy","Harakatli, emotsional"],"c":0},{"q":"Faoliyatda motiv qanday vazifani bajaradi?","a":["Undovchilik","Signallik aks ettirish","Ko'nikma-malakalarni namoyon etish","Maqsadga yo'naltirish va aks ettirish"],"c":0},{"q":"Odamning har xil yosh bosqichlarida psixik rivojlanish xususiyatlarini o'rganadigan psixologiya tarmog'i?","a":["Yosh davrlar psixologiyasi","Umumiy psixologiya","Zopsixologiya","Pedagogik psixologiya"],"c":0},{"q":"\"Biz bolalarni o'rgana olmasdan turib, tarbiyalay olmaymiz\" ushbu fikr muallifi kim?","a":["Ushinskiy","Elkoni","Petroviskiy","Xoll"],"c":0},{"q":"Yosh psixologiyasining predmeti?","a":["Inson psixikasining yosh jihatdan taraqqiyoti, psixik jarayonlar hamda inson shaxsi xislatlarining ontogenezini o'rganishdan iborat.","Psixik jarayonlarning, bilimlarni o'zlashtirishning yosh imkoniyatlarini tadqiq qilish","Shaxs rivojlanishining muhim omillarini o'rganish","Psixologiyani qonuniyatlari va mexanizmlarini o'rganishdan iborat"],"c":0},{"q":"\"Inson tarbiya predmeti sifatida\" nomli asar muallifi?","a":["K.D. Ushinskiy","S.Xoll","V.Preyer","N. Elkonin"],"c":0},{"q":"E.Erikson bo'yicha 3-davr nima deb nomlanadi?","a":["O'yin yoshi","Bog'cha yoshi","Maktab yoshi","O'smirlik yoshi"],"c":0},{"q":"Senzitiv davr bu....?","a":["U yoki bu psixik xususiyatlarning rivojlanishi uchun eng qulay sharoitlar bo'lgan yosh davrlari","Har xillik davri","Bolalilikdan o'smirlikka o'tish davri","Kamolot bo'sag'asi davri"],"c":0},{"q":"Yosh va pedagogik psixologiya fan sifatida qachon rivojlangan?","a":["XIX asrning ikkinchi yarmida","XX asrning ikkinchi yarmida","XIX asrning birinchi yarmida","XX asrning boshlarida"],"c":0},{"q":"Yosh psixologiyasining asosiy metodologik tamoyillari bu….?","a":["Determinizm tamoyili, ong va faoliyatning birligi tamoyili, psixikaning faoliyatda rivojlanishi tamoyili","Determinizm tamoyili, ko'rsatmalilik","Ong va faoliyatning birligi tamoyili, izchillik","Barcha javoblar to'g'ri"],"c":0},{"q":"Yosh va pedagogik psixologiya fanini rivojlantirgan o'zbekistonlik olimlar?","a":["M.G.Davletshin, E.G'.G'oziev","V.N.Taytishev, N.I.Novikov","A.N.Radishchev, G.Davletshin","N.V.Krutetskiy, E.G'.G'oziev"],"c":0},{"q":"Ontogenez bu...?","a":["Insonning tug'ilganidan umrining oxirigacha bo'lgan taraqqiyot davri.","Har bir davrdagi rivojlanishning o'ziga xos qulay davri.","Inglizcha so'z bo'lib, sinash, tekshirish demakdir","Psixik rivojlanish davri"],"c":0},{"q":"Prenatal davr qanday davr?","a":["Xomila davri","Keksalik davri","Bolalaik davri","O'smirlik davri"],"c":0},{"q":"\"Men\", \"o'zim\" konsepsiyasi bolada qaysi yosh davrida vujudga keladi?","a":["Ilk bolalikda","Yoshlik davrida","Go'daklik davrida","Yetuklik davrida"],"c":0},{"q":"Ilk bolalik davrining asosiy faoliyati bu…?","a":["Predmetli faoliyat","O'yin faoliyati","O'qish faoliyati","Mehnat faoliyati"],"c":0},{"q":"Maktabgacha yosh davri nechta bosqichni o'z ichiga oladi?","a":["3 bosqich: kichik, o'rta, katta","2 bosqich: kichik, o'rta","2 bosqich: kichik, katta","1 bosqich: katta"],"c":0},{"q":"Maktabgacha yosh davrining asosiy faoliyati bu…?","a":["O'yin","O'qish","Mehnat","To'g'ri javob berilmagan"],"c":0},{"q":"Bolaning o'yin jarayonida tajriba, bilim va ko'nikmalardan ijodiy foydalanishi….","a":["O'yin kompetensiyasi","Kommunikativ kompetensiya","Ijtimoiy kompetensiya","Bilish kompetensiyasi"],"c":0},{"q":"Maktabgacha yoshidagi bolalar diqqatining qaysi turi rivojlangan bo'ladi?","a":["Ixtiyorsiz","Ixtiyoriy","Moslashgan","Barcha turlari"],"c":0},{"q":"Bolalardagi predmetni idrok qilish necha oydan boshlanadi?","a":["7 oydan","6 oydan","5 oydan","8 oydan"],"c":0},{"q":"Bolaning shaxsi va shaxsiy xislatlari qaysi davrda rivojlanadi?","a":["Bog'cha davrida","O'spirinlik davrida","Maktab davrida","Etuklik davrida"],"c":0},{"q":"Kichik maktab yoshida o'quv jarayonida asosan o'qituvchilar nimani talab qiladi?","a":["Diqqat","Xotira","Xayol","Xissiyot"],"c":0},{"q":"Bolaning psixik faoliyatni rejalashtirish, boshqarish, nazorat qilish bo'limlari necha yoshda to'liq rivojlanadi?","a":["12","11","7","8"],"c":0},{"q":"Kichik maktab yoshidagi o'quvchi faolligining nech xil ko'rinishi mavjud?","a":["3","5","8","7"],"c":0},{"q":"Kichik maktab yoshi davrida qanday xotira rivojlanadi?","a":["Obrazli","Tezkor","Passiv","Aktiv"],"c":0},{"q":"Qo'yilgan savollarga javob olishga mo'ljallangan ijtimoiy psixologiya metodi?","a":["So'rovnoma","Sotsiometrik","Biografiya","Qiyoslash"],"c":0},{"q":"\"Akseleratsiya\" so'zining ma'nosi nima?","a":["Jadallashish","Sekinlashish","Yetuklik","Balog'at"],"c":0},{"q":"O'smirlik yoshida «tanglik» davrining kechishi nima bilan aniqlanadi?","a":["O'smir organizmida anatomfiziologik o'zgarishlar bilan","O'smir shaxsining shakllanish xususiyatlari o'sishi bilan","O'smirda o'qish motivlarining sekin tarkib topishi bilan","Ota-onalar bilan munosabat o'zgarishi bilan"],"c":0},{"q":"O'smirlik davri qanday psixologik ko'rinishlari bilan xarakterlanadi?","a":["«O'tish davri», «krizis davr», «qiyin davr»","Balog'at davri","Rahnomolik, homiylik","Kamolot bo'sag'asi"],"c":0},{"q":"O'smirlik davri necha bosqichga bo'linadi?","a":["2 bosqich: kichik va katta","1 bosqich: o'smirlik","3 bosqich: kichik, o'rta, katta","Barcha javoblar to'g'ri"],"c":0},{"q":"O'smirlik davrining asosiy faoliyati bu…?","a":["O'qish","Mehnat","O'yin","Muloqot"],"c":0},{"q":"Ta'surotni qabul qilib oladigan retseptorlar hamda javob reaktsiyasini qaytaruvchi organlar bilan bog'laydigan sezuvchi nervlar bu...?","a":["Periferik","Kinestetik","Vegitativ","Verbal"],"c":0},{"q":"Ilk o'spirinlik yoshi necha yoshlarni o'z ichiga oladi?","a":["14-15-17-18 yosh","15-25-28 yosh","11-13-15 yosh","7-9-10 yosh"],"c":0},{"q":"Kim tomonidan 1920 yilda o'spirinlik haqida nazariyalar ko'pligi ta'kidlangan va 3 ta yirik yo'nalish ajratib ko'rsatilgan?","a":["L.Vigotskiy","G.Levin","S.Xoll","V.Stellin"],"c":0},{"q":"Odamning fuqaro sifatida shakllanishi, ijtimoiy jihatdan yetilishi va o'z taqdirini o'zi hal qilishi qaysi davr?","a":["O'spirinlik davri","Yetuklik davri","O'smirlik davri","Maktabgacha yosh davri"],"c":0},{"q":"Yoshlik davri necha yoshlarni o'z ichiga oladi?","a":["23-28 yosh","20-30 yosh","35-40 yosh","18-23 yosh"],"c":0},{"q":"Sezgirlikning barqarorlashuvi necha yoshgacha davom etadi?","a":["25-50 yoshgacha","30-35 yoshgacha","15-45 yoshgacha","40-55 yoshgacha"],"c":0},{"q":"\"Ong faoliyatda paydo bo'lib, faoliyatda shakillanadi\" degan fikr muallifi bu…?","a":["S.L.Rubinshteyn","I.S.Vigotiskiy","Stenli Xoll, Bolduin","Usheniskiy"],"c":0},{"q":"G.S. Abramova bo'yicha yosh davrlari nechta turi ko'rsatilgan?","a":["11","10","7","8"],"c":0},{"q":"Freydizm yo'nalishiga kim asos solgan?","a":["Z.Freyd","Dj.Lokk","D.Paven","B.Bekon"],"c":0},{"q":"Anketa metodi qanday usulda o'tkaziladi va nechta guruhga bo'linadi?","a":["Ommaviy so'roq asosida, 3 turli","Turli aqliy o'yinlar asosida, 2 turli","Sinalovchining o'ziga bildirmagan holda kuzatish, 3 turli","Sinalovchi qiziqan fan asosida savollar berish orqali, 5 turda"],"c":0},{"q":"Pubertat (jinsiy yetilish) davri necha yoshlarni o'z ichiga oladi?","a":["14 yoshdan 18 yoshgacha","6 yoshdan 10 yoshgacha","7 yoshdan 12 yoshgacha","18 yoshdan 25 yoshgacha"],"c":0},{"q":"Kichik yoshdagi o'quvchilarni xotirasi kattalarning xotirasidan…?","a":["Ko'p jihatdan farq qiladi","Unchalik farq qilmaydi","Qisman ozgina farq qiladi","Umuman boshqa-boshqa"],"c":0},{"q":"Maktabgacha davrdagi bolalarda qanday psixik jarayon rivojlanadi?","a":["Irodaviy","Ta'limiy","Jismoniy","Nutqiy"],"c":0},{"q":"Obrazli xotira qaysi davrda kuchli rivojlanadi?","a":["Kichik maktab davrida","Maktabgacha davrida","O'rta maktab yoshida","Chaqaloqlik davrida"],"c":0},{"q":"Qaysi davr bolaning nutq faoliyati to'g'ri maqsadga muvofiq rivojlanishi bosqichi hisoblanadi?","a":["Maktabgacha yoshi davri","Kichik maktab yosh davri","Ilk bolalik davri","Go'daklik davri"],"c":0},{"q":"Yetuklik davrining birinchi bosqichi qaysi yosh oralig'ini qamrab oladi?","a":["28–35 yosh","18–25 yosh","36–45 yosh","55–65 yosh"],"c":0},{"q":"Yetuklik davrida faoliyat samaradorligi asosan nimaga tayanadi?","a":["Malaka va mahoratga","Kuchli asab zo'riqishiga","Tasodifiy harakatlarga","Faqat jismoniy kuchga"],"c":0}];

const LETTERS=['A','B','C','D'];
let questions=[],idx=0,correct=0,wrong=0,answered=false,numQ=10;

function shuffle(arr){for(let i=arr.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[arr[i],arr[j]]=[arr[j],arr[i]];}return arr;}

function prepareQuestions(n){
  const pool=shuffle([...ALL_Q]).slice(0,n);
  questions=pool.map(orig=>{
    const ct=orig.a[orig.c];
    const sh=shuffle([...orig.a]);
    return{q:orig.q,a:sh,c:sh.indexOf(ct)};
  });
}

document.querySelectorAll('.mode-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.mode-btn').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    numQ=parseInt(btn.dataset.n);
  });
});

document.getElementById('start-btn').addEventListener('click',()=>{
  prepareQuestions(numQ);
  idx=0;correct=0;wrong=0;
  document.getElementById('start-screen').style.display='none';
  document.getElementById('quiz-body').style.display='block';
  showQuestion();
});

function showQuestion(){
  answered=false;
  const q=questions[idx];
  document.getElementById('q-counter').textContent=`Savol ${idx+1} / ${questions.length}`;
  document.getElementById('question').textContent=q.q;
  document.getElementById('progress-fill').style.width=(idx/questions.length*100)+'%';
  document.getElementById('correct-count').textContent=correct;
  document.getElementById('wrong-count').textContent=wrong;
  const fb=document.getElementById('feedback');
  fb.className='';fb.textContent='';
  document.getElementById('next-btn').style.display='none';
  const opts=document.getElementById('options');
  opts.innerHTML='';
  q.a.forEach((text,i)=>{
    const btn=document.createElement('button');
    btn.className='opt';
    btn.innerHTML=`<span class="opt-letter">${LETTERS[i]}</span><span class="opt-text">${text}</span>`;
    btn.addEventListener('click',()=>selectAnswer(i));
    opts.appendChild(btn);
  });
}

function selectAnswer(chosen){
  if(answered)return;
  answered=true;
  const q=questions[idx];
  const opts=document.querySelectorAll('.opt');
  const fb=document.getElementById('feedback');
  opts.forEach((btn,i)=>{
    btn.disabled=true;
    if(i===q.c)btn.classList.add('correct');
    else if(i===chosen&&chosen!==q.c)btn.classList.add('wrong');
    else btn.classList.add('faded');
  });
  if(chosen===q.c){
    correct++;
    fb.className='show correct-fb';
    fb.textContent="✓ To'g'ri!";
  } else {
    wrong++;
    fb.className='show wrong-fb';
    fb.textContent=`✗ Noto'g'ri. To'g'ri javob: ${q.a[q.c]}`;
  }
  document.getElementById('correct-count').textContent=correct;
  document.getElementById('wrong-count').textContent=wrong;
  document.getElementById('next-btn').style.display='inline-block';
}

document.getElementById('next-btn').addEventListener('click',()=>{
  idx++;
  if(idx>=questions.length)showResults();
  else showQuestion();
});

function showResults(){
  document.getElementById('quiz-body').style.display='none';
  const res=document.getElementById('results');
  res.className='show';
  const pct=Math.round(correct/questions.length*100);
  document.getElementById('score-num').textContent=correct;
  document.getElementById('score-den').textContent='/ '+questions.length;
  document.getElementById('r-correct').textContent=correct;
  document.getElementById('r-wrong').textContent=wrong;
  document.getElementById('r-pct').textContent=pct+'%';
  let title,msg;
  if(pct>=90){title="Ajoyib natija! 🎉";msg="Siz mavzuni mukammal bilasiz!";}
  else if(pct>=70){title="Yaxshi natija! 👍";msg="Ko'p narsalarni bilasiz. Bir oz takrorlash foyda qiladi.";}
  else if(pct>=50){title="O'rtacha natija";msg="Yana bir marta o'qib, qayta sinab ko'ring.";}
  else{title="Mashq kerak 📖";msg="Mavzuni qayta o'rganib chiqing.";}
  document.getElementById('results-title').textContent=title;
  document.getElementById('results-msg').textContent=msg;
}

document.getElementById('restart-btn').addEventListener('click',()=>{
  document.getElementById('results').className='';
  document.getElementById('start-screen').style.display='block';
});
</script>
</body>
</html>
