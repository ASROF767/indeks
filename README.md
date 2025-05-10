<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>TikrarQuran Web</title>
<style>
  /* Reset & base */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0; padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    background: #e0f2f1;
    color: #004d40;
    max-width: 350px;
    min-height: 600px;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    flex-direction: column;
  }
  header {
    background: #00796b;
    color: white;
    padding: 1rem;
    text-align: center;
    font-weight: 700;
    font-size: 1.4rem;
    user-select:none;
  }
  main {
    flex-grow: 1;
    padding: 0.75rem;
    overflow-y: auto;
  }
  nav {
    background: #004d40;
    display: flex;
    justify-content: space-around;
  }
  nav button {
    flex: 1;
    border: none;
    background: transparent;
    color: #a7ffeb;
    padding: 0.75rem 0;
    font-weight: 600;
    font-size: 0.9rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  nav button.active, nav button:hover {
    background: #00695c;
  }

  section {
    display: none;
    margin: 0 auto;
    max-width: 320px;
  }
  section.active {
    display: block;
  }

  /* Hafalan Tracker */
  #hafalan input, #hafalan select, #hafalan textarea {
    width: 100%;
    margin-bottom: 0.6rem;
    padding: 0.4rem 0.5rem;
    font-size: 1rem;
    border-radius: 4px;
    border: 1.5px solid #00796b;
  }
  #hafalan textarea {
    resize: vertical;
  }
  #hafalan button.add-btn {
    width: 100%;
    background: #00796b;
    color: #e0f2f1;
    border: none;
    padding: 0.6rem;
    font-weight: 700;
    font-size: 1.05rem;
    border-radius: 4px;
    cursor: pointer;
    box-shadow: 0 3px 6px #004d40aa;
    transition: background-color 0.3s ease;
  }
  #hafalan button.add-btn:hover:enabled {
    background: #004d40;
  }
  #hafalan button.add-btn:disabled {
    background: #90a4a3;
    cursor: not-allowed;
  }
  #hafalan-list {
    margin-top: 1rem;
  }
  #hafalan-list .item {
    background: #b2dfdb;
    border-radius: 6px;
    padding: 0.5rem 0.7rem;
    margin-bottom: 0.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 1px 6px #004d4088;
  }
  #hafalan-list .item .info {
    flex-grow: 1;
  }
  #hafalan-list .item .rep {
    font-weight: 700;
    margin-left: 0.5rem;
    color: #004d40;
  }
  #hafalan-list .item button {
    background: transparent;
    border: none;
    cursor: pointer;
    color: #004d40;
    font-weight: 700;
    font-size: 1.2rem;
    padding: 0 0.5rem;
    user-select:none;
  }
  #hafalan-list .item button:hover {
    color: #00796b;
  }

  /* Audio Player */
  #audio-player {
    text-align: center;
  }
  #audio-player select, #audio-player input[type=range] {
    width: 100%;
    margin: 0.8rem 0;
  }
  #audio-player button {
    background: #00796b;
    border: none;
    color: #e0f2f1;
    font-size: 1.2rem;
    padding: 0.7rem 1.2rem;
    border-radius: 6px;
    cursor: pointer;
    margin-bottom: 1rem;
    box-shadow: 0 2px 5px #004d40aa;
    transition: background-color 0.3s ease;
  }
  #audio-player button:hover:enabled {
    background: #004d40;
  }
  #audio-player button:disabled {
    background: #90a4a3;
    cursor: not-allowed;
  }

  /* Reminder */
  #reminder {
    text-align: center;
  }
  #reminder button {
    background: #00796b;
    border: none;
    color: white;
    font-size: 1.1rem;
    padding: 0.7rem 1rem;
    border-radius: 6px;
    cursor: pointer;
    margin: 0.2rem;
    box-shadow: 0 2px 5px #004d40aa;
  }
  #reminder button:hover {
    background: #004d40;
  }
  #reminder .info {
    font-size: 1.1rem;
    margin: 1rem 0;
    font-weight: 700;
  }

  /* Self Evaluation */
  #evaluation {
    text-align: center;
  }
  #evaluation button {
    background: #00796b;
    border: none;
    color: white;
    font-size: 1.2rem;
    padding: 1rem 1.5rem;
    border-radius: 50%;
    cursor: pointer;
    box-shadow: 0 3px 7px #004d40aa;
    margin-bottom: 1rem;
  }
  #evaluation button.recording {
    background: #d32f2f;
    box-shadow: 0 3px 7px #b71c1caa;
  }
  #evaluation .status {
    font-weight: 600;
    font-size: 1.2rem;
    min-height: 2rem;
    margin-bottom: 1rem;
  }
  #evaluation .eval-text {
    background: #b2dfdb;
    padding: 1rem;
    border-radius: 8px;
    box-shadow: 0 1px 5px #004d4099;
  }

  /* Community */
  #community {
    text-align: center;
    color: #004d40dd;
  }
  #community .placeholder {
    margin-top: 3rem;
    font-size: 1.1rem;
    font-weight: 700;
  }
  #community .icon {
    font-size: 6rem;
    color: #00796b;
    margin-bottom: 1rem;
  }

  /* Badge section */
  #badges {
    margin: 1rem 0 1.5rem 0;
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
  }
  #badges .badge {
    background: #004d40;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    color: #a7ffeb;
    font-weight: 700;
    font-size: 0.9rem;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0 3px 6px #00796bbb;
    user-select:none;
  }
  #badges .badge.achieved {
    background: #00796b;
    color: #e0f2f1;
    box-shadow: 0 3px 10px #004d40cc;
  }

  /* Scrollbar minimal styling */
  main::-webkit-scrollbar {
    width: 6px;
  }
  main::-webkit-scrollbar-thumb {
    background: #00796baa;
    border-radius: 3px;
  }
  main::-webkit-scrollbar-track {
    background: #b2dfdb55;
  }
</style>
</head>
<body>
<header>TikrarQuran Web</header>
<main>
  <!-- Hafalan Tracking Feature -->
  <section id="hafalan" class="active" aria-label="Hafalan Tracking">
    <h2>Tracking Hafalan</h2>
    <label for="mode">Mode Belajar:</label>
    <select id="mode" aria-describedby="modeHelp" aria-required="true">
      <option value="juz30">Juz 30 Pemula</option>
      <option value="tahfidz30">Program Tahfidz 30 Juz</option>
    </select>
    <small id="modeHelp">Pilih target hafalan Anda</small>
    <label for="ayatJuz">Ayat/Juz Hafalan</label>
    <input type="text" id="ayatJuz" placeholder="Misal: Juz 30 atau Al-Fatihah ayat 1-7" aria-required="true" />
    <label for="note">Catatan (opsional)</label>
    <textarea id="note" rows="2" placeholder="Catatan tambahan..."></textarea>
    <button class="add-btn" id="addHafalanBtn" aria-label="Tambah hafalan baru" disabled>Tambah Hafalan</button>
    <div id="hafalan-list" aria-live="polite" aria-relevant="additions removals"></div>

    <h3>Badges dan Achievements</h3>
    <div id="badges" aria-label="Badge pengguna"></div>
  </section>

  <!-- Audio Murotal -->
  <section id="audio-player" aria-label="Audio Murotal">
    <h2>Audio Murotal</h2>
    <label for="audioSelect">Pilih Audio</label>
    <select id="audioSelect" aria-required="true"></select>
    <label for="speedRange">Kecepatan Putar: <span id="speedVal">1.0x</span></label>
    <input id="speedRange" type="range" min="0.5" max="2" value="1" step="0.1" />
    <button id="playBtn" aria-label="Putar audio" disabled>▶ Putar</button>
    <button id="pauseBtn" aria-label="Jeda audio" disabled>⏸ Jeda</button>
    <button id="stopBtn" aria-label="Stop audio" disabled>⏹ Stop</button>
  </section>

  <!-- Reminder Schedule -->
  <section id="reminder" aria-label="Pengingat Jadwal Tikrar">
    <h2>Pengingat Jadwal Tikrar</h2>
    <p id="reminderInfo" aria-live="polite">Pengingat belum diatur.</p>
    <label for="reminderTime">Pilih waktu pengingat:</label><br />
    <input type="time" id="reminderTime" aria-required="true" /><br /><br />
    <button id="setReminderBtn">Atur Pengingat</button>
    <button id="cancelReminderBtn" hidden>Batalkan Pengingat</button>
  </section>

  <!-- Self Evaluation with voice -->
  <section id="evaluation" aria-label="Evaluasi Mandiri">
    <h2>Evaluasi Mandiri Hafalan</h2>
    <button id="recordBtn" aria-label="Mulai rekam suara hafalan">●</button>
    <div class="status" id="recordStatus" aria-live="polite" aria-atomic="true">Tekan tombol untuk mulai merekam</div>
    <div id="evalResult" class="eval-text" aria-live="polite" style="display:none;"></div>
    <p style="margin-top: 1.5rem; font-size: 0.9rem; color: #004d4055;">
      Gunakan rekaman suara untuk menganalisis kelancaran hafalan Anda.
    </p>
  </section>

  <!-- Community placeholder -->
  <section id="community" aria-label="Komunitas TikrarQuran">
    <div class="icon" aria-hidden="true">👥</div>
    <div class="placeholder">
      Fitur komunitas dalam pengembangan.<br />
      Nantikan fitur berbagi pengalaman dan sesi murojaah kelompok.<br />
      Bisa terus berinteraksi di update berikutnya.
    </div>
  </section>
</main>
<nav aria-label="Navigasi utama aplikasi">
  <button class="active" id="navHafalan" aria-controls="hafalan" aria-selected="true" role="tab">Hafalan</button>
  <button id="navAudio" aria-controls="audio-player" aria-selected="false" role="tab">Audio</button>
  <button id="navReminder" aria-controls="reminder" aria-selected="false" role="tab">Pengingat</button>
  <button id="navEvaluation" aria-controls="evaluation" aria-selected="false" role="tab">Evaluasi</button>
  <button id="navCommunity" aria-controls="community" aria-selected="false" role="tab">Komunitas</button>
</nav>

<script>
  // Navigation
  const sections = {
    hafalan: document.getElementById('hafalan'),
    audio: document.getElementById('audio-player'),
    reminder: document.getElementById('reminder'),
    evaluation: document.getElementById('evaluation'),
    community: document.getElementById('community'),
  };
  const navButtons = {
    hafalan: document.getElementById('navHafalan'),
    audio: document.getElementById('navAudio'),
    reminder: document.getElementById('navReminder'),
    evaluation: document.getElementById('navEvaluation'),
    community: document.getElementById('navCommunity'),
  };
  function activateTab(tabKey) {
    for (const key in sections) {
      if (key === tabKey) {
        sections[key].classList.add('active');
        navButtons[key].classList.add('active');
        navButtons[key].setAttribute('aria-selected', 'true');
        sections[key].setAttribute('tabindex', '0');
      } else {
        sections[key].classList.remove('active');
        navButtons[key].classList.remove('active');
        navButtons[key].setAttribute('aria-selected', 'false');
        sections[key].setAttribute('tabindex', '-1');
      }
    }
  }
  Object.keys(navButtons).forEach(key => {
    navButtons[key].addEventListener('click', e => {
      e.preventDefault();
      activateTab(key);
    });
  });

  // Hafalan Tracking Logic
  const hafalanListEl = document.getElementById('hafalan-list');
  const addBtn = document.getElementById('addHafalanBtn');
  const ayatJuzInput = document.getElementById('ayatJuz');
  const noteInput = document.getElementById('note');
  const modeSelect = document.getElementById('mode');
  const badgesContainer = document.getElementById('badges');

  function loadHafalan() {
    const stored = localStorage.getItem('hafalan_records');
    let arr = [];
    if(stored){
      try {
        arr = JSON.parse(stored);
      } catch { arr = []; }
    }
    return arr;
  }
  function saveHafalan(arr){
    localStorage.setItem('hafalan_records', JSON.stringify(arr));
  }
  function loadMode(){
    let mode = localStorage.getItem('study_mode');
    if(!mode) return 'juz30';
    return mode;
  }
  function saveMode(mode){
    localStorage.setItem('study_mode', mode);
  }

  // badges System
  function calculateBadges(records){
    const badges = [
      {id:1, name:'Pemula', condition: r => r.length >= 1},
      {id:2, name:'Pengulang', condition: r => r.some(item => item.repeats >= 3)},
      {id:3, name:'Konsisten', condition: r => r.length >= 10},
      {id:4, name:'Ahli', condition: r => r.some(item => item.repeats >= 10)},
      {id:5, name:'Master 30 Juz', condition: r => {
        const made30 = r.filter(i => i.ayatJuz.toLowerCase().includes('juz 30')).length;
        return made30 >= 5;
      }},
    ];
    let result = badges.map(b => {
      try {
        return {...b, achieved: b.condition(records)};
      } catch {
        return {...b, achieved:false};
      }
    });
    return result;
  }

  function refreshBadges(){
    const records = loadHafalan();
    const badges = calculateBadges(records);
    badgesContainer.innerHTML = '';
    badges.forEach(badge => {
      const bEl = document.createElement('div');
      bEl.classList.add('badge');
      if(badge.achieved) bEl.classList.add('achieved');
      bEl.setAttribute('title', badge.name + (badge.achieved ? ' (Dicapai)' : ' (Belum dicapai)'));
      bEl.textContent = badge.name;
      badgesContainer.appendChild(bEl);
    });
  }

  function renderHafalanList(){
    const records = loadHafalan();
    hafalanListEl.innerHTML = '';
    if(records.length === 0){
      hafalanListEl.textContent = 'Belum ada pencatatan hafalan.';
      return;
    }
    records.forEach((rec, idx) => {
      const item = document.createElement('div');
      item.className = 'item';
      const info = document.createElement('div');
      info.className = 'info';
      info.textContent = rec.ayatJuz + ' (x' + rec.repeats + ')';
      if(rec.note) {
        info.textContent += ' - ' + rec.note;
      }
      const incBtn = document.createElement('button');
      incBtn.textContent = '↻';
      incBtn.title = 'Tambah pengulangan';
      incBtn.onclick = () => {
        records[idx].repeats++;
        saveHafalan(records);
        renderHafalanList();
        refreshBadges();
      };
      const delBtn = document.createElement('button');
      delBtn.textContent = '×';
      delBtn.title = 'Hapus';
      delBtn.onclick = () => {
        if(confirm('Hapus catatan hafalan ini?')){
          records.splice(idx,1);
          saveHafalan(records);
          renderHafalanList();
          refreshBadges();
        }
      };
      item.appendChild(info);
      item.appendChild(incBtn);
      item.appendChild(delBtn);
      hafalanListEl.appendChild(item);
    });
  }

  function validateInputs(){
    if(ayatJuzInput.value.trim() === '') {
      addBtn.disabled = true;
    } else {
      addBtn.disabled = false;
    }
  }

  ayatJuzInput.addEventListener('input', validateInputs);

  addBtn.addEventListener('click', () => {
    const records = loadHafalan();
    records.push({
      date: new Date().toISOString(),
      ayatJuz: ayatJuzInput.value.trim(),
      note: noteInput.value.trim(),
      repeats: 1,
      mode: modeSelect.value,
    });
    saveHafalan(records);
    ayatJuzInput.value = '';
    noteInput.value = '';
    addBtn.disabled = true;
    renderHafalanList();
    refreshBadges();
  });

  modeSelect.addEventListener('change', e => {
    saveMode(e.target.value);
  });

  // Initialize Hafalan section
  modeSelect.value = loadMode();
  validateInputs();
  renderHafalanList();
  refreshBadges();

  // Audio Murotal
  const audioSources = [
    {title:'Surah Al-Fatihah', url:'https://download.quranicaudio.com/quran/mishaari_raashid_al_3afaasee/001.mp3'},
    {title:'Surah Al-Baqarah 2:1-5', url:'https://download.quranicaudio.com/quran/mishaari_raashid_al_3afaasee/002001.mp3'},
  ];

  const audioSelect = document.getElementById('audioSelect');
  const playBtn = document.getElementById('playBtn');
  const pauseBtn = document.getElementById('pauseBtn');
  const stopBtn = document.getElementById('stopBtn');
  const speedRange = document.getElementById('speedRange');
  const speedVal = document.getElementById('speedVal');
  let audio = new Audio();
  let isPlaying = false;

  function populateAudioSelect(){
    for(let i=0; i < audioSources.length; i++){
      const option = document.createElement('option');
      option.value = i;
      option.textContent = audioSources[i].title;
      audioSelect.appendChild(option);
    }
  }
  populateAudioSelect();

  function playAudio(){
    const idx = parseInt(audioSelect.value);
    if(isNaN(idx)) return;
    audio.src = audioSources[idx].url;
    audio.playbackRate = parseFloat(speedRange.value);
    audio.play();
    isPlaying = true;
    toggleAudioButtons();
  }
  function pauseAudio(){
    audio.pause();
    isPlaying = false;
    toggleAudioButtons();
  }
  function stopAudio(){
    audio.pause();
    audio.currentTime = 0;
    isPlaying = false;
    toggleAudioButtons();
  }
  function toggleAudioButtons(){
    playBtn.disabled = isPlaying;
    pauseBtn.disabled = !isPlaying;
    stopBtn.disabled = !isPlaying;
  }

  audioSelect.addEventListener('change', () => {
    playBtn.disabled = false;
  });
  playBtn.addEventListener('click', () => {
    playAudio();
  });
  pauseBtn.addEventListener('click', () => {
    pauseAudio();
  });
  stopBtn.addEventListener('click', () => {
    stopAudio();
  });
  speedRange.addEventListener('input', () => {
    speedVal.textContent = speedRange.value + 'x';
    if(isPlaying){
      audio.playbackRate = parseFloat(speedRange.value);
    }
  });

  toggleAudioButtons();

  // Reminder Logic using browser notification API
  const reminderTimeInput = document.getElementById('reminderTime');
  const setReminderBtn = document.getElementById('setReminderBtn');
  const cancelReminderBtn = document.getElementById('cancelReminderBtn');
  const reminderInfo = document.getElementById('reminderInfo');

  // store reminder in localStorage
  function loadReminder() {
    let storedTime = localStorage.getItem('tikrar_reminder');
    if(storedTime){
      reminderTimeInput.value = storedTime;
      reminderInfo.textContent = 'Pengingat diatur pada ' + formatTimeHM(storedTime);
      cancelReminderBtn.hidden = false;
    } else {
      reminderInfo.textContent = 'Pengingat belum diatur.';
      cancelReminderBtn.hidden = true;
    }
  }
  loadReminder();

  // format hh:mm to hh:mm am/pm for display
  function formatTimeHM(timeStr){
    const [h,m] = timeStr.split(':').map(x => parseInt(x));
    const ampm = h >= 12 ? 'PM' : 'AM';
    let hour12 = h % 12; hour12 = hour12 === 0 ? 12 : hour12;
    return hour12 + ':' + (m<10?'0':'')+m + ' ' + ampm;
  }

  // schedule repeating daily reminder (simulate with setTimeout + localStorage)
  let reminderTimeout;

  // permission check & request
  function requestNotificationPermission(){
    if('Notification' in window){
      if(Notification.permission === "default"){
        return Notification.requestPermission();
      }
      return Promise.resolve(Notification.permission);
    }
    return Promise.reject("Notification not supported");
  }

  function scheduleReminder(timeStr){
    if(reminderTimeout) clearTimeout(reminderTimeout);
    const now = new Date();
    const [hour, min] = timeStr.split(':').map(x => parseInt(x));
    let nextTime = new Date();
    nextTime.setHours(hour, min, 0, 0);
    if(nextTime <= now){
      nextTime.setDate(nextTime.getDate() +1);
    }
    const delay = nextTime.getTime() - now.getTime();

    reminderTimeout = setTimeout(() => {
      showNotification();
      scheduleReminder(timeStr);
    }, delay);
  }

  function showNotification(){
    if(Notification.permission === 'granted'){
      let notif = new Notification('Pengingat TikrarQuran', {
        body: 'Waktunya melakukan pengulangan hafalan Anda.',
        icon: '',
        tag: 'tikrar_reminder'
      });
      notif.onclick = () => window.focus();
    }
  }

  setReminderBtn.addEventListener('click', async () => {
    let val = reminderTimeInput.value;
    if(!val){
      alert('Silakan pilih waktu pengingat.');
      return;
    }
    try {
      const perm = await requestNotificationPermission();
      if(perm !== 'granted'){
        alert('Izin notifikasi dibutuhkan agar pengingat dapat bekerja.');
        return;
      }
      localStorage.setItem('tikrar_reminder', val);
      scheduleReminder(val);
      reminderInfo.textContent = 'Pengingat diatur pada ' + formatTimeHM(val);
      cancelReminderBtn.hidden = false;
      alert('Pengingat berhasil diatur.');
    } catch(e){
      alert('Gagal mengatur pengingat: ' + e);
    }
  });
  cancelReminderBtn.addEventListener('click', () => {
    localStorage.removeItem('tikrar_reminder');
    if(reminderTimeout) clearTimeout(reminderTimeout);
    reminderTimeout = null;
    reminderInfo.textContent = 'Pengingat belum diatur.';
    cancelReminderBtn.hidden = true;
    alert('Pengingat dibatalkan.');
  });

  if(localStorage.getItem('tikrar_reminder')){
    scheduleReminder(localStorage.getItem('tikrar_reminder'));
  }

  // Self Evaluation - Voice recording
  const recordBtn = document.getElementById('recordBtn');
  const recordStatus = document.getElementById('recordStatus');
  const evalResult = document.getElementById('evalResult');

  let mediaRecorder;
  let audioChunks = [];

  recordBtn.addEventListener('click', async () => {
    if(mediaRecorder && mediaRecorder.state === 'recording'){
      mediaRecorder.stop();
      return;
    }
    // start recording
    if(!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia){
      alert('Fitur rekam suara tidak didukung browser Anda.');
      return;
    }
    try {
      const stream = await navigator.mediaDevices.getUserMedia({audio:true});
      mediaRecorder = new MediaRecorder(stream);
      audioChunks = [];
      mediaRecorder.ondataavailable = e => {
        audioChunks.push(e.data);
      };
      mediaRecorder.onstop = e => {
        stream.getTracks().forEach(t => t.stop());
        let audioBlob = new Blob(audioChunks, {type:'audio/webm'});
        // We can do with audioBlob as needed, here we simulate evaluation
        evaluateRecording(audioBlob);
      };
      mediaRecorder.start();
      recordStatus.textContent = 'Sedang merekam... Tekan lagi untuk berhenti.';
      recordBtn.classList.add('recording');
      evalResult.style.display = 'none';
      evalResult.textContent = '';
    } catch(e) {
      alert('Gagal mengakses mikrofon: ' + e);
    }
  });

  function evaluateRecording(blob){
    // Simulate evaluation using timeout (in real app, send to server or AI)
    recordStatus.textContent = 'Memproses evaluasi...';
    setTimeout(() => {
      recordStatus.textContent = 'Evaluasi selesai!';
      evalResult.style.display = 'block';
      evalResult.textContent = 'Hasil evaluasi: Hafalan Anda terdengar lancar dan baik. Teruskan latihan!';
      recordBtn.classList.remove('recording');
    }, 2500);
  }
</script>
</body>
</html>

