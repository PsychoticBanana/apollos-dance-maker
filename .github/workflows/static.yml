<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Apollo's Dance Module Builder</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap');

  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #7fff6e;
    --accent2: #ff6ef7;
    --accent3: #6ebaff;
    --text: #e8e8f0;
    --muted: #5a5a72;
    --danger: #ff6e6e;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(127,255,110,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(127,255,110,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .container {
    max-width: 760px;
    margin: 0 auto;
    padding: 48px 24px 80px;
    position: relative;
    z-index: 1;
  }

  header {
    margin-bottom: 48px;
  }

  .logo-tag {
    font-family: 'Syne', sans-serif;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    background: rgba(127,255,110,0.08);
    border: 1px solid rgba(127,255,110,0.2);
    display: inline-block;
    padding: 4px 10px;
    margin-bottom: 16px;
  }

  h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 5vw, 42px);
    font-weight: 800;
    line-height: 1.1;
    color: #fff;
  }

  h1 span {
    color: var(--accent);
  }

  .subtitle {
    margin-top: 12px;
    color: var(--muted);
    font-size: 13px;
    line-height: 1.6;
  }

  /* Sections */
  .section {
    margin-bottom: 32px;
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 24px;
    position: relative;
  }

  .section::before {
    content: attr(data-num);
    position: absolute;
    top: -1px;
    left: -1px;
    font-family: 'Syne', sans-serif;
    font-size: 10px;
    font-weight: 800;
    letter-spacing: 0.15em;
    color: var(--bg);
    background: var(--accent);
    padding: 2px 8px;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 20px;
    margin-top: 4px;
  }

  .field-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  @media (max-width: 520px) {
    .field-row { grid-template-columns: 1fr; }
  }

  .field {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .field.full { grid-column: 1 / -1; }

  label {
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
  }

  input[type="text"], textarea {
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 13px;
    padding: 10px 14px;
    outline: none;
    transition: border-color 0.15s;
    width: 100%;
    resize: vertical;
  }

  input[type="text"]:focus, textarea:focus {
    border-color: var(--accent);
  }

  input[type="text"]::placeholder, textarea::placeholder {
    color: var(--muted);
    opacity: 0.6;
  }

  /* Drop zones */
  .dropzone {
    border: 1.5px dashed var(--border);
    background: var(--bg);
    padding: 28px 20px;
    text-align: center;
    cursor: pointer;
    transition: border-color 0.15s, background 0.15s;
    position: relative;
  }

  .dropzone:hover, .dropzone.dragover {
    border-color: var(--accent);
    background: rgba(127,255,110,0.04);
  }

  .dropzone.has-file {
    border-color: var(--accent);
    border-style: solid;
  }

  .dropzone.rbxm:hover, .dropzone.rbxm.dragover {
    border-color: var(--accent2);
    background: rgba(255,110,247,0.04);
  }

  .dropzone.rbxm.has-file {
    border-color: var(--accent2);
  }

  .dropzone input[type="file"] {
    position: absolute;
    inset: 0;
    opacity: 0;
    cursor: pointer;
    width: 100%;
    height: 100%;
  }

  .dz-icon {
    font-size: 28px;
    margin-bottom: 8px;
    display: block;
  }

  .dz-label {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 4px;
  }

  .dz-sub {
    font-size: 11px;
    color: var(--muted);
  }

  .dz-filename {
    font-size: 12px;
    color: var(--accent);
    margin-top: 8px;
    font-weight: 700;
    word-break: break-all;
  }

  .dropzone.rbxm .dz-filename { color: var(--accent2); }

  /* Build button */
  .build-btn {
    width: 100%;
    padding: 16px;
    background: var(--accent);
    border: none;
    color: var(--bg);
    font-family: 'Syne', sans-serif;
    font-size: 15px;
    font-weight: 800;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    cursor: pointer;
    transition: opacity 0.15s, transform 0.1s;
    margin-top: 8px;
  }

  .build-btn:hover { opacity: 0.9; transform: translateY(-1px); }
  .build-btn:active { transform: translateY(0); }
  .build-btn:disabled { opacity: 0.3; cursor: not-allowed; transform: none; }

  /* Status log */
  .log-area {
    background: var(--bg);
    border: 1px solid var(--border);
    padding: 16px;
    font-size: 12px;
    line-height: 1.8;
    min-height: 80px;
    margin-top: 24px;
    display: none;
  }

  .log-area.visible { display: block; }

  .log-line { color: var(--muted); }
  .log-line.ok { color: var(--accent); }
  .log-line.err { color: var(--danger); }
  .log-line.info { color: var(--accent3); }

  /* Downloads */
  .downloads {
    display: none;
    margin-top: 24px;
    border: 1px solid var(--border);
    padding: 20px;
    background: var(--surface);
  }

  .downloads.visible { display: block; }

  .downloads h3 {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 16px;
  }

  .dl-list { display: flex; flex-direction: column; gap: 10px; }

  .dl-btn {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    text-decoration: none;
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    transition: border-color 0.15s;
    cursor: pointer;
  }

  .dl-btn:hover { border-color: var(--accent3); }
  .dl-btn:hover .dl-arrow { color: var(--accent); }

  .dl-ext {
    font-family: 'Syne', sans-serif;
    font-size: 10px;
    font-weight: 800;
    letter-spacing: 0.1em;
    padding: 3px 7px;
    background: rgba(110,186,255,0.1);
    color: var(--accent3);
    border: 1px solid rgba(110,186,255,0.2);
    flex-shrink: 0;
  }

  .dl-ext.lua { background: rgba(127,255,110,0.1); color: var(--accent); border-color: rgba(127,255,110,0.2); }
  .dl-ext.anim { background: rgba(255,110,247,0.1); color: var(--accent2); border-color: rgba(255,110,247,0.2); }

  .dl-name { flex: 1; }
  .dl-arrow { color: var(--muted); font-size: 16px; }

  .hint {
    font-size: 11px;
    color: var(--muted);
    margin-top: 6px;
    line-height: 1.5;
  }

  .hint span { color: var(--accent3); }
</style>
</head>
<body>
<div class="container">
  <header>
    <div class="logo-tag">UhhhhhhReanim</div>
    <h1>Apollo's Dance Module<br><span>Builder</span></h1>
    <p class="subtitle" style="font-style:italic; color:var(--muted); font-size:11px; margin-top:8px;">website made by AI</p>
  </header>

  <!-- Section 1: Info -->
  <div class="section" data-num="01 — INFO">
    <div class="section-title">Dance/Module Details</div>
    <div class="field-row">
      <div class="field">
        <label>Dance Name</label>
        <input type="text" id="danceName" placeholder="e.g. Dance Example" />
        <p class="hint">You can have spaces in the name</p>
      </div>
      <div class="field">
        <label>File Names</label>
        <input type="text" id="fileName" placeholder="e.g. Name Example" />
        <p class="hint">You can have spaces in the name · Used for all files: <span id="fileHint">Name Example.mp3 / .anim</span></p>
      </div>
      <div class="field full">
        <label>Description</label>
        <textarea id="description" rows="2" placeholder="e.g. Description Example 😔🙏"></textarea>
        <p class="hint">You can have emojis and spaces in the description</p>
      </div>
    </div>
  </div>

  <!-- Section 2: Audio -->
  <div class="section" data-num="02 — AUDIO">
    <div class="section-title">Audio/Video → mp3</div>
    <div class="dropzone" id="audioDrop">
      <input type="file" id="audioInput" accept="audio/*,video/*,.mp3,.wav,.ogg,.m4a,.mp4,.mov" />
      <div class="dz-label">Drop audio / video here</div>
      <div class="dz-sub">MP3, WAV, OGG, M4A, MP4, MOV, etc. — exports as .mp3</div>
      <div class="dz-filename" id="audioName"></div>
    </div>
    <p class="hint" style="margin-top:10px">⚠️ MP3 conversion runs in your browser via FFmpeg.wasm — first load may take ~20s. Already-MP3 files skip conversion instantly.</p>
  </div>

  <!-- Section 3: RBXM -->
  <div class="section" data-num="03 — ANIMATION">
    <div class="section-title">RBXM File → .anim</div>
    <div class="dropzone rbxm" id="rbxmDrop">
      <input type="file" id="rbxmInput" accept=".rbxm,.rbxmx" />
      <div class="dz-label">Drop .rbxm or .rbxmx here</div>
      <div class="dz-sub">Rbxm → Anim</div>
      <div class="dz-filename" id="rbxmName"></div>
    </div>
  </div>

  <!-- Build -->
  <button class="build-btn" id="buildBtn" disabled>⬇ Build &amp; Download All Files</button>

  <!-- Log -->
  <div class="log-area" id="logArea"></div>

  <!-- Downloads -->
  <div class="downloads" id="downloads">
    <h3>✔ Files Ready</h3>
    <div class="dl-list" id="dlList"></div>
  </div>
</div>

<script type="module">
// ── FFmpeg ESM (v0.12) ─────────────────────────────────
import { FFmpeg } from 'https://unpkg.com/@ffmpeg/ffmpeg@0.12.10/dist/esm/index.js';
import { fetchFile, toBlobURL } from 'https://unpkg.com/@ffmpeg/util@0.12.1/dist/esm/index.js';
window._FFmpeg    = FFmpeg;
window._fetchFile = fetchFile;
window._toBlobURL = toBlobURL;
window._ffmpegReady = true;
</script>

<script>
// ─── UI refs ───────────────────────────────────────────
const nameEl       = document.getElementById('danceName');
const fileNameEl   = document.getElementById('fileName');
const descEl       = document.getElementById('description');
const audioInput   = document.getElementById('audioInput');
const rbxmInput    = document.getElementById('rbxmInput');
const buildBtn     = document.getElementById('buildBtn');
const logArea      = document.getElementById('logArea');
const dlContainer  = document.getElementById('downloads');
const dlList       = document.getElementById('dlList');
const fileHint     = document.getElementById('fileHint');

let audioFile = null, rbxmFile = null;

// ─── File hint update ──────────────────────────────────
fileNameEl.addEventListener('input', () => {
  const v = fileNameEl.value.trim() || 'Hat throw';
  fileHint.textContent = `${v}.mp3 / ${v}.anim`;
});

// ─── Drag-drop wiring ──────────────────────────────────
function wireDrop(zone, inputEl, onFile) {
  zone.addEventListener('dragover', e => { e.preventDefault(); zone.classList.add('dragover'); });
  zone.addEventListener('dragleave', () => zone.classList.remove('dragover'));
  zone.addEventListener('drop', e => {
    e.preventDefault();
    zone.classList.remove('dragover');
    const f = e.dataTransfer.files[0];
    if (f) onFile(f);
  });
  inputEl.addEventListener('change', () => {
    if (inputEl.files[0]) onFile(inputEl.files[0]);
  });
}

wireDrop(document.getElementById('audioDrop'), audioInput, f => {
  audioFile = f;
  document.getElementById('audioName').textContent = f.name;
  document.getElementById('audioDrop').classList.add('has-file');
  checkReady();
});

wireDrop(document.getElementById('rbxmDrop'), rbxmInput, f => {
  rbxmFile = f;
  document.getElementById('rbxmName').textContent = f.name;
  document.getElementById('rbxmDrop').classList.add('has-file');
  checkReady();
});

function checkReady() {
  const ok = nameEl.value.trim() && fileNameEl.value.trim() && audioFile && rbxmFile;
  buildBtn.disabled = !ok;
}
nameEl.addEventListener('input', checkReady);
fileNameEl.addEventListener('input', checkReady);

// ─── Logging ───────────────────────────────────────────
function log(msg, cls = '') {
  logArea.classList.add('visible');
  const d = document.createElement('div');
  d.className = 'log-line ' + cls;
  d.textContent = msg;
  logArea.appendChild(d);
  logArea.scrollTop = logArea.scrollHeight;
}

// ─── LUA template (EXACT same as original) ──────────────────────────────────────
function buildLua(name, fileName, description) {
  return `-- UhhhhhhReanim/Modules/${name}.lua

local modules = {}

table.insert(modules, function()
    local m = {}

    m.ModuleType  = "DANCE"
    m.Name        = "${name}"
    m.Description = "${description}"
    m.Assets = {"${fileName}.anim", "${fileName}.mp3"}

    m.Config = function(parent)
        Util_CreateText(parent, "No settings.", 14, Enum.TextXAlignment.Center)
    end

    m.SaveConfig = function() return {} end
    m.LoadConfig  = function(save) end

    local animator = nil
    local start    = 0

    m.Init = function(figure)
        SetOverrideDanceMusic(AssetGetContentId("${fileName}.mp3"), "${name}", 0.8, NumberRange.new(0, 45.5))

        start           = os.clock()
        animator        = AnimLib.Animator.new()
        animator.rig    = figure
        animator.track  = AnimLib.Track.fromfile(AssetGetPathFromFilename("${fileName}.anim"))
        animator.looped = true
        animator.speed  = 1
    end

    m.Update = function(dt, figure)
        animator:Step(os.clock() - start)
    end

    m.Destroy = function(figure)
        animator = nil
    end

    return m
end)



return modules
`;
}

// ============================================================================
// FIXED RBXM → .anim CONVERTER (handles both binary and XML, finds KeyframeSequence properly)
// ============================================================================
const E_STYLE = ["Linear","Constant","Elastic","Cubic","Bounce","CubicV2"];
const E_DIREC = ["In","Out","InOut"];

function encodeAnim({ name, keyframes }) {
  const parts = [];
  function putU16(v) { const b=new Uint8Array(2); new DataView(b.buffer).setUint16(0,v,true); parts.push(b); }
  function putU32(v) { const b=new Uint8Array(4); new DataView(b.buffer).setUint32(0,v,true); parts.push(b); }
  function putF32(v) { const b=new Uint8Array(4); new DataView(b.buffer).setFloat32(0,v,true); parts.push(b); }
  function putStr(s) {
    const enc = new TextEncoder().encode(s);
    putU16(enc.length);
    parts.push(enc);
  }

  putStr(name);
  putU32(keyframes.length);

  for (const kf of keyframes) {
    putF32(kf.time);
    putU32(kf.poses.length);
    for (const pose of kf.poses) {
      putStr(pose.name);
      putF32(pose.weight || 0);
      putStr(E_STYLE[pose.easingStyle] || 'Linear');
      putStr(E_DIREC[pose.easingDir]   || 'In');
      for (const c of pose.cf) putF32(c);
    }
  }

  const total = parts.reduce((s,p) => s+p.length, 0);
  const out = new Uint8Array(total);
  let off = 0;
  for (const p of parts) { out.set(p, off); off+=p.length; }
  return out;
}

// LZ4 decompressor for binary RBXM
function lz4Decompress(src, uncompressedSize) {
  const dst = new Uint8Array(uncompressedSize);
  let si = 0, di = 0;
  while (si < src.length) {
    const token = src[si++];
    let litLen = (token >> 4) & 0xf;
    if (litLen === 15) { let x; do { x = src[si++]; litLen += x; } while (x === 255); }
    dst.set(src.slice(si, si + litLen), di);
    si += litLen; di += litLen;
    if (si >= src.length) break;
    const offset = src[si] | (src[si+1] << 8); si += 2;
    let matchLen = (token & 0xf) + 4;
    if (matchLen - 4 === 15) { let x; do { x = src[si++]; matchLen += x; } while (x === 255); }
    let msrc = di - offset;
    for (let i = 0; i < matchLen; i++) dst[di++] = dst[msrc++];
  }
  return dst;
}

// Main RBXM parser (handles both binary and XML)
function parseRBXMToKeyframeSequence(arrayBuffer) {
  const bytes = new Uint8Array(arrayBuffer);
  // Check if XML (starts with "<roblox" or "<?xml")
  const isXml = (bytes[0] === 0x3c && bytes[1] === 0x72 && bytes[2] === 0x6f && bytes[3] === 0x62 && bytes[4] === 0x6c);
  if (isXml) {
    return parseXMLRBXM(bytes);
  } else {
    return parseBinaryRBXM(bytes);
  }
}

function parseXMLRBXM(bytes) {
  const text = new TextDecoder('utf-8').decode(bytes);
  const parser = new DOMParser();
  const doc = parser.parseFromString(text, 'text/xml');
  
  // Find KeyframeSequence (works with your exact XML structure)
  let kfsEl = doc.querySelector('Item[class="KeyframeSequence"]');
  if (!kfsEl) {
    // Try alternate selector
    kfsEl = doc.querySelector('KeyframeSequence');
    if (!kfsEl) throw new Error('No KeyframeSequence found in XML RBXM');
  }
  
  const nameEl2 = kfsEl.querySelector('Properties string[name="Name"], Name');
  const seqName = nameEl2 ? nameEl2.textContent.trim() : 'Animation';
  
  const keyframes = [];
  const kfNodes = kfsEl.querySelectorAll('Item[class="Keyframe"], Keyframe');
  
  function collectPoses(parentEl, poses) {
    const poseNodes = parentEl.querySelectorAll(':scope > Item[class="Pose"], :scope > Pose');
    for (const poseNode of poseNodes) {
      const nameNode = poseNode.querySelector('Properties string[name="Name"], Name');
      const weightNode = poseNode.querySelector('Properties float[name="Weight"], Weight');
      const styleNode = poseNode.querySelector('Properties token[name="EasingStyle"], EasingStyle');
      const dirNode = poseNode.querySelector('Properties token[name="EasingDirection"], EasingDirection');
      const cfNode = poseNode.querySelector('Properties CoordinateFrame[name="CFrame"], CoordinateFrame, CFrame');
      
      let cf = [0,0,0, 1,0,0, 0,1,0, 0,0,1];
      if (cfNode) {
        const get = (tag) => { const n = cfNode.querySelector(tag); return n ? parseFloat(n.textContent) : 0; };
        cf = [get('X'), get('Y'), get('Z'),
              get('R00'), get('R01'), get('R02'),
              get('R10'), get('R11'), get('R12'),
              get('R20'), get('R21'), get('R22')];
      }
      
      poses.push({
        name: nameNode ? nameNode.textContent.trim() : 'Unknown',
        weight: weightNode ? parseFloat(weightNode.textContent) : 1.0,
        easingStyle: styleNode ? parseInt(styleNode.textContent) : 0,
        easingDir: dirNode ? parseInt(dirNode.textContent) : 0,
        cf: cf
      });
      collectPoses(poseNode, poses);
    }
  }
  
  for (const kfNode of kfNodes) {
    const timeNode = kfNode.querySelector('Properties float[name="Time"], Time');
    const time = timeNode ? parseFloat(timeNode.textContent) : 0;
    const poses = [];
    collectPoses(kfNode, poses);
    keyframes.push({ time, poses });
  }
  
  keyframes.sort((a,b) => a.time - b.time);
  return { name: seqName, keyframes };
}

function parseBinaryRBXM(bytes) {
  // Check header
  if (bytes[0] !== 0x3C || bytes[7] !== 0x21) throw new Error('Not a valid binary RBXM');
  
  let off = 16;
  const classMap = new Map();
  const instances = new Map();
  const parentMap = new Map();
  
  function deinterleaveInt32s(data, count) {
    const out = new Int32Array(count);
    for (let i = 0; i < count; i++) {
      const enc = ((data[i]<<24)|(data[i+count]<<16)|(data[i+count*2]<<8)|data[i+count*3])>>>0;
      out[i] = (enc & 1) ? -((enc>>>1)+1) : (enc>>>1);
    }
    return out;
  }
  
  function deinterleaveFloat32s(data, count) {
    const out = new Float32Array(count);
    const tmp = new Uint8Array(4);
    const tmpDv = new DataView(tmp.buffer);
    for (let i = 0; i < count; i++) {
      const enc = ((data[i]<<24)|(data[i+count]<<16)|(data[i+count*2]<<8)|data[i+count*3])>>>0;
      const rot = ((enc >>> 1) | (enc << 31)) >>> 0;
      tmpDv.setUint32(0, rot, false);
      out[i] = tmpDv.getFloat32(0, false);
    }
    return out;
  }
  
  function readChunk() {
    if (off + 16 > bytes.length) return null;
    const tag = String.fromCharCode(bytes[off], bytes[off+1], bytes[off+2], bytes[off+3]); off+=4;
    const dv = new DataView(bytes.buffer, bytes.byteOffset, bytes.byteLength);
    const compLen = dv.getUint32(off, true); off+=4;
    const uncompLen = dv.getUint32(off, true); off+=4;
    off += 4; // reserved
    const compData = bytes.slice(off, off + compLen); off += compLen;
    let payload;
    if (uncompLen === 0) payload = compData;
    else payload = lz4Decompress(compData, uncompLen);
    return { tag, payload };
  }
  
  while (true) {
    const chunk = readChunk();
    if (!chunk) break;
    const { tag, payload } = chunk;
    const pdv = new DataView(payload.buffer, payload.byteOffset, payload.byteLength);
    let p = 0;
    
    if (tag === 'INST') {
      const classId = pdv.getInt32(p, true); p+=4;
      const nameLen = pdv.getInt32(p, true); p+=4;
      const cname = new TextDecoder().decode(payload.slice(p, p+nameLen)); p+=nameLen;
      p += 1; // isService
      const count = pdv.getInt32(p, true); p+=4;
      const rawIds = payload.slice(p, p+count*4); p+=count*4;
      const refsRaw = deinterleaveInt32s(rawIds, count);
      let acc = 0;
      const refs = [];
      for (let i = 0; i < count; i++) { acc += refsRaw[i]; refs.push(acc); }
      classMap.set(classId, { name: cname, refs: refs });
      for (const ref of refs) instances.set(ref, { className: cname, props: {} });
    }
    else if (tag === 'PROP') {
      const classId = pdv.getInt32(p, true); p+=4;
      const propLen = pdv.getInt32(p, true); p+=4;
      const propName = new TextDecoder().decode(payload.slice(p, p+propLen)); p+=propLen;
      const propType = payload[p]; p+=1;
      const cls = classMap.get(classId);
      if (!cls) continue;
      const count = cls.refs.length;
      if (count === 0) continue;
      
      try {
        if (propType === 0x01) {
          for (let i = 0; i < count; i++) {
            const slen = pdv.getUint32(p, true); p+=4;
            const str = new TextDecoder().decode(payload.slice(p, p+slen)); p+=slen;
            instances.get(cls.refs[i]).props[propName] = str;
          }
        } else if (propType === 0x04) {
          const vals = deinterleaveInt32s(payload.slice(p, p+count*4), count); p+=count*4;
          for (let i = 0; i < count; i++) instances.get(cls.refs[i]).props[propName] = vals[i];
        } else if (propType === 0x05) {
          const vals = deinterleaveFloat32s(payload.slice(p, p+count*4), count); p+=count*4;
          for (let i = 0; i < count; i++) instances.get(cls.refs[i]).props[propName] = vals[i];
        } else if (propType === 0x0E) {
          for (let i = 0; i < count; i++) {
            const special = payload[p++];
            let cf = [0,0,0, 1,0,0, 0,1,0, 0,0,1];
            if (special !== 0) {
              const x = pdv.getFloat32(p,true); p+=4;
              const y = pdv.getFloat32(p,true); p+=4;
              const z = pdv.getFloat32(p,true); p+=4;
              cf = [x,y,z, 1,0,0, 0,1,0, 0,0,1];
            } else {
              const x=pdv.getFloat32(p,true); p+=4;
              const y=pdv.getFloat32(p,true); p+=4;
              const z=pdv.getFloat32(p,true); p+=4;
              const r00=pdv.getFloat32(p,true); p+=4;
              const r01=pdv.getFloat32(p,true); p+=4;
              const r02=pdv.getFloat32(p,true); p+=4;
              const r10=pdv.getFloat32(p,true); p+=4;
              const r11=pdv.getFloat32(p,true); p+=4;
              const r12=pdv.getFloat32(p,true); p+=4;
              const r20=pdv.getFloat32(p,true); p+=4;
              const r21=pdv.getFloat32(p,true); p+=4;
              const r22=pdv.getFloat32(p,true); p+=4;
              cf = [x,y,z, r00,r01,r02, r10,r11,r12, r20,r21,r22];
            }
            instances.get(cls.refs[i]).props[propName] = cf;
          }
        }
      } catch(e) {}
    }
    else if (tag === 'PRNT') {
      p += 1;
      const count = pdv.getInt32(p, true); p+=4;
      const childRaw = payload.slice(p, p+count*4); p+=count*4;
      const parentRaw = payload.slice(p, p+count*4);
      const children = deinterleaveInt32s(childRaw, count);
      const parents = deinterleaveInt32s(parentRaw, count);
      let childAcc = 0, parentAcc = 0;
      for (let i = 0; i < count; i++) {
        childAcc += children[i];
        parentAcc += parents[i];
        if (parentAcc >= 0) parentMap.set(childAcc, parentAcc);
      }
    }
    else if (tag === 'END\0') break;
  }
  
  // Find KeyframeSequence
  let kfsRef = null;
  for (const [ref, inst] of instances) {
    if (inst.className === 'KeyframeSequence') { kfsRef = ref; break; }
  }
  if (!kfsRef) throw new Error('No KeyframeSequence found in binary RBXM');
  
  const kfsInst = instances.get(kfsRef);
  const seqName = kfsInst.props['Name'] || 'Animation';
  const keyframes = [];
  const allRefs = Array.from(instances.keys());
  
  for (const ref of allRefs) {
    const inst = instances.get(ref);
    if (inst.className === 'Keyframe' && parentMap.get(ref) === kfsRef) {
      const time = inst.props['Time'] ?? 0;
      const poses = [];
      
      function collectPosesRec(parentRef) {
        for (const childRef of allRefs) {
          const child = instances.get(childRef);
          if (child.className === 'Pose' && parentMap.get(childRef) === parentRef) {
            const cf = child.props['CFrame'] || [0,0,0, 1,0,0, 0,1,0, 0,0,1];
            poses.push({
              name: child.props['Name'] || 'Unknown',
              weight: child.props['Weight'] ?? 1.0,
              easingStyle: child.props['EasingStyle'] ?? 0,
              easingDir: child.props['EasingDirection'] ?? 0,
              cf: cf
            });
            collectPosesRec(childRef);
          }
        }
      }
      collectPosesRec(ref);
      keyframes.push({ time, poses });
    }
  }
  
  keyframes.sort((a,b) => a.time - b.time);
  return { name: seqName, keyframes };
}

// ─── FIXED MP3 conversion via FFmpeg.wasm ───────────────────────────────────
let ffmpegInstance = null;
async function convertToMp3(file, outName) {
  if (file.name.toLowerCase().endsWith('.mp3') || file.type === 'audio/mpeg') {
    log('File is already MP3, passing through...', 'info');
    const buf = await file.arrayBuffer();
    return new Uint8Array(buf);
  }

  log('Loading FFmpeg.wasm (first load ~15s)...', 'info');

  let attempts = 0;
  while (!window._ffmpegReady && attempts < 100) {
    await new Promise(r => setTimeout(r, 100));
    attempts++;
  }
  if (!window._ffmpegReady) throw new Error('FFmpeg ESM module failed to load');

  if (!ffmpegInstance) {
    ffmpegInstance = new window._FFmpeg();
  }
  const ffmpeg = ffmpegInstance;

  if (!ffmpeg.loaded) {
    const baseURL = 'https://unpkg.com/@ffmpeg/core@0.12.6/dist/esm';
    await ffmpeg.load({
      coreURL: await window._toBlobURL(`${baseURL}/ffmpeg-core.js`, 'text/javascript'),
      wasmURL: await window._toBlobURL(`${baseURL}/ffmpeg-core.wasm`, 'application/wasm'),
    });
    log('FFmpeg core loaded', 'ok');
  }

  log('Converting to MP3...', 'info');
  const inName = 'input_' + file.name.replace(/[^a-zA-Z0-9._-]/g, '_');
  await ffmpeg.writeFile(inName, await window._fetchFile(file));
  await ffmpeg.exec(['-i', inName, '-vn', '-codec:a', 'libmp3lame', '-q:a', '2', outName]);
  const data = await ffmpeg.readFile(outName);
  await ffmpeg.deleteFile(inName);
  await ffmpeg.deleteFile(outName);
  return data;
}

// ─── Download helper ───────────────────────────────────
function addDownload(label, ext, data, mime) {
  const blob = new Blob([data], { type: mime });
  const url  = URL.createObjectURL(blob);
  const div  = document.createElement('div');
  div.className = 'dl-btn';
  div.innerHTML = `<span class="dl-ext ${ext}">.${ext}</span><span class="dl-name">${label}</span><span class="dl-arrow">↓</span>`;
  div.addEventListener('click', () => {
    const a = document.createElement('a');
    a.href = url; a.download = label;
    a.click();
    setTimeout(() => URL.revokeObjectURL(url), 100);
  });
  dlList.appendChild(div);
}

// ─── Main build ────────────────────────────────────────
buildBtn.addEventListener('click', async () => {
  buildBtn.disabled = true;
  logArea.innerHTML = '';
  dlList.innerHTML = '';
  dlContainer.classList.remove('visible');

  const danceName  = nameEl.value.trim();
  const baseName   = fileNameEl.value.trim();
  const desc       = descEl.value.trim();

  try {
    // 1. Lua
    log('Building Lua module...', 'info');
    const lua = buildLua(danceName, baseName, desc);
    log(`✔ Lua ready: ${baseName}.lua`, 'ok');

    // 2. RBXM → .anim (FIXED)
    log('Converting RBXM to .anim...', 'info');
    const rbxmBuf = await rbxmFile.arrayBuffer();
    let animData;
    try {
      const seqData = parseRBXMToKeyframeSequence(rbxmBuf);
      animData = encodeAnim(seqData);
      log(`✔ .anim ready: ${baseName}.anim (${seqData.keyframes.length} keyframes)`, 'ok');
    } catch(e) {
      log(`✘ RBXM error: ${e.message}`, 'err');
      animData = null;
    }

    // 3. Audio → MP3 (FIXED)
    let mp3Data = null;
    try {
      mp3Data = await convertToMp3(audioFile, baseName + '.mp3');
      log(`✔ MP3 ready: ${baseName}.mp3`, 'ok');
    } catch(e) {
      log(`✘ MP3 error: ${e.message}`, 'err');
    }

    // 4. Show downloads
    dlContainer.classList.add('visible');
    addDownload(`${baseName}.lua`, 'lua', new TextEncoder().encode(lua), 'text/plain');
    if (animData) addDownload(`${baseName}.anim`, 'anim', animData, 'application/octet-stream');
    if (mp3Data)  addDownload(`${baseName}.mp3`,  'mp3',  mp3Data,  'audio/mpeg');
    log('All done! Click files above to download.', 'ok');

  } catch(e) {
    log('✘ Fatal error: ' + e.message, 'err');
    buildBtn.disabled = false;
  }
});
</script>
</body>
</html>
