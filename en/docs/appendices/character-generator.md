# Character Generator

Create and customize your Ironwake character. Fill in your identity, roll and assign attributes, and save your work!

<style>
  .cg-container {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    margin: 1.5rem 0;
  }

  /* Character Sheet styles */
  .cg-sheet {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }
  .cg-section {
    background: var(--md-code-bg, #1e1e2e);
    border-radius: 12px;
    padding: 1.5rem;
  }
  .cg-section h2 {
    margin-top: 0;
    margin-bottom: 1rem;
    font-size: 1.2rem;
    color: #e94560;
  }
  .cg-field-group {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
    margin-bottom: 1rem;
  }
  .cg-field {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }
  .cg-field label {
    font-size: 0.85rem;
    opacity: 0.8;
  }
  .cg-field input,
  .cg-field select,
  .cg-field textarea {
    background: var(--md-default-bg-color, #fff);
    color: var(--md-typeset-color, #111);
    border: 1px solid var(--md-default-fg-color--lightest, #ccc);
    border-radius: 6px;
    padding: 0.5rem 0.75rem;
    font-size: 0.95rem;
  }
  .cg-field textarea {
    min-height: 80px;
    resize: vertical;
  }

  /* Attribute slots in sheet */
  .cg-attrs {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 0.75rem;
    margin-bottom: 1.5rem;
  }
  .cg-attr-box {
    background: var(--md-default-bg-color, #fff);
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    border: 2px dashed transparent;
    transition: border-color 0.2s, background 0.2s;
    min-height: 7rem;
  }
  .cg-attr-box.drag-over {
    border-color: #e94560;
    background: rgba(233, 69, 96, 0.08);
  }
  .cg-attr-box.filled {
    border-color: transparent;
    cursor: grab;
  }
  .cg-attr-box h3 {
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin: 0 0 0.4rem;
    opacity: 0.7;
  }
  .cg-attr-box .score {
    font-size: 2.2rem;
    font-weight: 700;
    color: #e94560;
    line-height: 1.1;
  }
  .cg-attr-box .modifier {
    font-size: 0.85rem;
    opacity: 0.6;
    margin-bottom: 0.5rem;
  }
  .cg-attr-box .drop-placeholder {
    font-size: 0.8rem;
    opacity: 0.35;
    padding: 1rem 0;
  }
  .cg-attr-asi {
    margin-top: 0.5rem;
    font-size: 0.75rem;
  }
  .cg-attr-asi input {
    width: 100%;
    font-size: 0.75rem;
    padding: 0.25rem 0.4rem;
  }

  /* Roller styles */
  .attr-roller {
    margin-bottom: 1.5rem;
  }
  .attr-roller .controls {
    display: flex;
    gap: 0.75rem;
    align-items: center;
    flex-wrap: wrap;
    margin-bottom: 1rem;
  }
  .attr-roller .score-pool {
    margin-bottom: 1rem;
  }
  .attr-roller .controls label {
    font-size: 0.85rem;
  }
  .attr-roller .controls input {
    background: var(--md-default-bg-color, #fff);
    color: var(--md-typeset-color, #111);
    border: 1px solid var(--md-default-fg-color--lightest, #ccc);
    border-radius: 6px;
    padding: 0.4rem 0.6rem;
    font-size: 0.9rem;
    width: 4rem;
    text-align: center;
  }
  .btn {
    background: #e94560;
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 0.5rem 1.25rem;
    font-size: 0.95rem;
    cursor: pointer;
    font-weight: 600;
  }
  .btn:hover {
    opacity: 0.85;
  }

  /* Score pool */
  .score-pool {
    display: flex;
    gap: 0.75rem;
    flex-wrap: wrap;
    padding: 1rem;
    background: var(--md-default-bg-color, #fff);
    border-radius: 10px;
    border: 2px dashed #555;
    min-height: 4rem;
    align-items: center;
    justify-content: center;
    transition: border-color 0.2s, background 0.2s;
  }
  .score-pool.drag-over {
    border-color: #e94560;
    background: rgba(233, 69, 96, 0.06);
  }
  .score-pool-label {
    width: 100%;
    text-align: center;
    font-size: 0.8rem;
    opacity: 0.6;
    margin-bottom: 0.25rem;
  }
  .pool-chip {
    background: #0f3460;
    color: #eee;
    border-radius: 8px;
    padding: 0.6rem 0.8rem;
    text-align: center;
    cursor: grab;
    user-select: none;
    transition: transform 0.15s, box-shadow 0.15s, opacity 0.15s;
    min-width: 4rem;
  }
  .pool-chip:active {
    cursor: grabbing;
  }
  .pool-chip.dragging {
    opacity: 0.4;
    transform: scale(0.95);
  }
  .pool-chip .chip-total {
    font-size: 1.4rem;
    font-weight: 700;
    color: #e94560;
  }
  .pool-chip .chip-mod {
    font-size: 0.75rem;
    opacity: 0.6;
  }

  /* Dice styles */
  .pool-chip .dice-row {
    display: flex;
    gap: 0.3rem;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 0.5rem;
  }
  .pool-chip .die {
    width: 1.5rem;
    height: 1.5rem;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.75rem;
    font-weight: 600;
    background: #0f3460;
    color: #eee;
  }
  .pool-chip .die.kept {
    background: #e94560;
  }
  .pool-chip .die.dropped {
    background: #333;
    color: #777;
  }

  .attr-roller .summary {
    margin-top: 1rem;
    font-size: 0.8rem;
    opacity: 0.6;
  }

  /* Identity section buttons */
  .identity-controls {
    display: flex;
    gap: 1rem;
    align-items: center;
    margin-bottom: 1rem;
  }
</style>

<div class="cg-container">
  <!-- Character Sheet -->
  <div class="cg-sheet">
    <!-- Identity -->
    <div class="cg-section">
      <h2>Identity</h2>
      <div class="identity-controls">
        <button class="btn" onclick="rollKai()">Roll Kai</button>
      </div>
      <input type="hidden" id="kai-position" value="0">
      <div class="cg-field-group">
        <div class="cg-field">
          <label for="cg-char-name">Character Name</label>
          <input type="text" id="cg-char-name" placeholder="Enter character name">
        </div>
        <div class="cg-field">
          <label for="cg-player-name">Player Name</label>
          <input type="text" id="cg-player-name" placeholder="Enter player name">
        </div>
      </div>
      <div class="cg-field-group">
        <div class="cg-field">
          <label for="cg-lineage">Lineage</label>
          <select id="cg-lineage">
            <option value="">Select lineage</option>
            <option value="Church-raised">Church-raised</option>
            <option value="Guild-born">Guild-born</option>
            <option value="Frontier-settled">Frontier-settled</option>
            <option value="Urban-underclass">Urban-underclass</option>
            <option value="Nomadic">Nomadic</option>
            <option value="Academic">Academic</option>
            <option value="Military">Military</option>
            <option value="Other">Other</option>
          </select>
        </div>
        <div class="cg-field" id="cg-lineage-other-field" style="display: none;">
          <label for="cg-lineage-other">Custom Lineage</label>
          <input type="text" id="cg-lineage-other" placeholder="Enter custom lineage">
        </div>
        <div class="cg-field">
          <label for="cg-class">Class</label>
          <select id="cg-class">
            <option value="">Select class</option>
            <option value="fighter">fighter</option>
            <option value="healer">healer</option>
            <option value="spellcaster">spellcaster</option>
            <option value="rogue">rogue</option>
          </select>
        </div>
      </div>
      <div class="cg-field-group">
        <div class="cg-field">
          <label for="cg-kai-tier">Kai Tier</label>
          <select id="cg-kai-tier">
            <option value="">Select tier</option>
            <option value="Forge" data-kai="4000">4-Forge</option>
            <option value="Blaze" data-kai="5000">5-Blaze</option>
            <option value="Pyre" data-kai="6000">6-Pyre</option>
            <option value="Inferno" data-kai="7000">7-Inferno</option>
            <option value="Conflagration" data-kai="8000">8-Conflagration</option>
            <option value="Stellar" data-kai="9000">9-Stellar</option>
            <option value="Other" data-kai="0">Other</option>
          </select>
        </div>
        <div class="cg-field" id="cg-kai-other-field" style="display: none;">
          <label for="cg-kai-other">Custom Kai Tier Name</label>
          <input type="text" id="cg-kai-other" placeholder="Enter custom tier name">
        </div>
        <div class="cg-field">
          <label for="cg-kai-value">Exact Kai Value</label>
          <input type="number" id="cg-kai-value" placeholder="Enter kai value" min="1">
        </div>
      </div>
      <div class="cg-field-group">
        <div class="cg-field">
          <label for="cg-level">Level</label>
          <input type="number" id="cg-level" value="1" min="1" max="20">
        </div>
        <div class="cg-field">
          <label for="cg-xp">XP</label>
          <input type="number" id="cg-xp" value="0" min="0">
        </div>
      </div>
    </div>

    <!-- Attributes -->
    <div class="cg-section">
      <h2>Attributes</h2>
      <div class="attr-roller">
        <div class="controls">
          <label>Dice <input type="number" id="rcount" value="4" min="1" max="20"></label>
          <label>d <input type="number" id="rsides" value="6" min="2" max="100"></label>
          <label>Keep best <input type="number" id="rkeep" value="3" min="1" max="20"></label>
          <button class="btn" onclick="rollAll()">Roll Attributes</button>
        </div>
        <div class="score-pool" id="rpool"></div>
        <div class="summary" id="rsummary"></div>
      </div>
      <div class="cg-attrs" id="cg-attrs">
        <!-- Generated by JS -->
      </div>
    </div>
  </div>
</div>

<script>
(function () {
  const ATTRS = ["Strength", "Dexterity", "Constitution", "Intelligence", "Wisdom", "Charisma"];
  var scorePool = [];
  var assignments = {};

  function modifier(score) {
    var m = Math.floor((score - 10) / 2);
    return (m >= 0 ? "+" : "") + m;
  }

  function rollDice(count, sides) {
    return Array.from({ length: count }, function () { return Math.floor(Math.random() * sides) + 1; });
  }

  function makeScore(id, count, sides, keepN, mode) {
    var dice = rollDice(count, sides);
    var sorted = dice.slice().sort(function (a, b) { return a - b; });
    var kept = mode === "best" ? sorted.slice(-keepN) : sorted.slice(0, keepN);
    var total = kept.reduce(function (s, v) { return s + v; }, 0);
    var keptVals = kept.slice();
    var used = [];
    var dieClasses = dice.map(function (v) {
      var idx = keptVals.findIndex(function (kv, ki) { return kv === v && used.indexOf(ki) === -1; });
      if (idx !== -1) { used.push(idx); return "kept"; }
      return "dropped";
    });
    return { id: id, total: total, modifier: modifier(total), dice: dice, dieClasses: dieClasses };
  }

  function findScoreById(id) {
    var s = scorePool.find(function (s) { return s.id === id; });
    if (s) return s;
    for (var i = 0; i < ATTRS.length; i++) {
      if (assignments[ATTRS[i]] && assignments[ATTRS[i]].id === id) {
        return assignments[ATTRS[i]];
      }
    }
    return null;
  }

  function findAttrByScoreId(id) {
    for (var i = 0; i < ATTRS.length; i++) {
      if (assignments[ATTRS[i]] && assignments[ATTRS[i]].id === id) {
        return ATTRS[i];
      }
    }
    return null;
  }

  function removeScoreFromEverywhere(id) {
    scorePool = scorePool.filter(function (s) { return s.id !== id; });
    for (var i = 0; i < ATTRS.length; i++) {
      if (assignments[ATTRS[i]] && assignments[ATTRS[i]].id === id) {
        assignments[ATTRS[i]] = null;
      }
    }
  }

  function renderPool() {
    var poolDiv = document.getElementById("rpool");
    if (scorePool.length === 0) {
      poolDiv.style.display = "none";
      return;
    }
    poolDiv.style.display = "flex";
    var html = '<div class="score-pool-label">Score Pool — drag to an attribute</div>';
    for (var i = 0; i < scorePool.length; i++) {
      var score = scorePool[i];
      html += '<div class="pool-chip" draggable="true" data-score-id="' + score.id + '">' +
        '<div class="chip-total">' + score.total + '</div>' +
        '<div class="chip-mod">' + score.modifier + '</div>' +
        '<div class="dice-row">' +
          score.dice.map(function (v, j) { return '<span class="die ' + score.dieClasses[j] + '">' + v + '</span>'; }).join("") +
        '</div>' +
      '</div>';
    }
    poolDiv.innerHTML = html;
  }

  function renderAttrBoxes() {
    var attrsDiv = document.getElementById("cg-attrs");
    var html = "";
    for (var i = 0; i < ATTRS.length; i++) {
      var attr = ATTRS[i];
      var score = assignments[attr];
      var asiId = "asi-" + attr.toLowerCase();
      if (score) {
        html += '<div class="cg-attr-box filled" draggable="true" data-score-id="' + score.id + '" data-attr="' + attr + '">' +
          '<h3>' + attr + '</h3>' +
          '<div class="score">' + score.total + '</div>' +
          '<div class="modifier">' + score.modifier + '</div>' +
          '<div class="cg-attr-asi"><label>ASIs: <input type="text" id="' + asiId + '" placeholder="Notes"></label></div>' +
        '</div>';
      } else {
        html += '<div class="cg-attr-box" data-attr="' + attr + '">' +
          '<h3>' + attr + '</h3>' +
          '<div class="drop-placeholder">Drop score here</div>' +
          '<div class="cg-attr-asi"><label>ASIs: <input type="text" id="' + asiId + '" placeholder="Notes"></label></div>' +
        '</div>';
      }
    }
    attrsDiv.innerHTML = html;
  }

  function handleDragStart(e) {
    e.dataTransfer.setData("text/plain", e.currentTarget.dataset.scoreId);
    e.dataTransfer.effectAllowed = "move";
    e.currentTarget.classList.add("dragging");
  }

  function handleDragEnd(e) {
    e.currentTarget.classList.remove("dragging");
    document.querySelectorAll(".cg-attr-box, .score-pool").forEach(function (el) { el.classList.remove("drag-over"); });
  }

  function handleDragOver(e) {
    e.preventDefault();
    e.dataTransfer.dropEffect = "move";
    e.currentTarget.classList.add("drag-over");
  }

  function handleDragEnter(e) {
    e.preventDefault();
    e.currentTarget.classList.add("drag-over");
  }

  function handleDragLeave(e) {
    e.currentTarget.classList.remove("drag-over");
  }

  function handleDropOnAttrBox(e) {
    e.preventDefault();
    e.currentTarget.classList.remove("drag-over");
    var scoreId = e.dataTransfer.getData("text/plain");
    var targetAttr = e.currentTarget.dataset.attr;
    var draggedScore = findScoreById(scoreId);
    if (!draggedScore) return;

    var sourceAttr = findAttrByScoreId(scoreId);
    var existingScore = assignments[targetAttr];

    if (sourceAttr && existingScore) {
      // Swap them!
      assignments[sourceAttr] = existingScore;
      assignments[targetAttr] = draggedScore;
    } else if (existingScore) {
      // Put existing back to pool
      scorePool.push(existingScore);
      removeScoreFromEverywhere(scoreId);
      assignments[targetAttr] = draggedScore;
    } else {
      // Just assign
      removeScoreFromEverywhere(scoreId);
      assignments[targetAttr] = draggedScore;
    }

    render();
  }

  function handleDropOnPool(e) {
    e.preventDefault();
    e.currentTarget.classList.remove("drag-over");
    var scoreId = e.dataTransfer.getData("text/plain");
    if (scorePool.some(function (s) { return s.id === scoreId; })) return;
    var draggedScore = findScoreById(scoreId);
    if (!draggedScore) return;
    for (var i = 0; i < ATTRS.length; i++) {
      if (assignments[ATTRS[i]] && assignments[ATTRS[i]].id === scoreId) {
        assignments[ATTRS[i]] = null;
        break;
      }
    }
    scorePool.push(draggedScore);
    render();
  }

  function attachDragListeners() {
    document.querySelectorAll(".pool-chip").forEach(function (chip) {
      chip.addEventListener("dragstart", handleDragStart);
      chip.addEventListener("dragend", handleDragEnd);
    });
    document.querySelectorAll(".cg-attr-box.filled").forEach(function (box) {
      box.addEventListener("dragstart", handleDragStart);
      box.addEventListener("dragend", handleDragEnd);
    });
    document.querySelectorAll(".cg-attr-box").forEach(function (box) {
      box.addEventListener("dragover", handleDragOver);
      box.addEventListener("dragenter", handleDragEnter);
      box.addEventListener("dragleave", handleDragLeave);
      box.addEventListener("drop", handleDropOnAttrBox);
    });
    var poolDiv = document.getElementById("rpool");
    poolDiv.addEventListener("dragover", handleDragOver);
    poolDiv.addEventListener("dragenter", handleDragEnter);
    poolDiv.addEventListener("dragleave", handleDragLeave);
    poolDiv.addEventListener("drop", handleDropOnPool);
  }

  function render() {
    renderPool();
    renderAttrBoxes();
    attachDragListeners();
  }

  window.rollAll = function () {
    var count = parseInt(document.getElementById("rcount").value) || 4;
    var sides = parseInt(document.getElementById("rsides").value) || 6;
    var keepN = parseInt(document.getElementById("rkeep").value) || 3;
    var mode = "best";
    scorePool = [];
    assignments = {};
    for (var i = 0; i < ATTRS.length; i++) {
      assignments[ATTRS[i]] = null;
    }
    for (var i = 0; i < 6; i++) {
      scorePool.push(makeScore("score-" + i, count, sides, keepN, mode));
    }
    render();
    document.getElementById("rsummary").textContent = count + "d" + sides + ", keep best " + keepN;
  };

  // Kai tier change handler
  function handleKaiTierChange() {
    var tierSelect = document.getElementById("cg-kai-tier");
    var kaiValueInput = document.getElementById("cg-kai-value");
    var kaiOtherField = document.getElementById("cg-kai-other-field");
    var kaiOtherInput = document.getElementById("cg-kai-other");
    var kaiPositionInput = document.getElementById("kai-position");
    var selectedOption = tierSelect.options[tierSelect.selectedIndex];
    var kaiValue = selectedOption.getAttribute("data-kai");
    var tierValue = selectedOption.value;
    var kaiPosition = parseInt(kaiPositionInput.value) || 0;

    // Disable the "Select tier" option once a choice is made
    tierSelect.options[0].disabled = true;

    if (tierValue === "Other") {
      kaiOtherField.style.display = "flex";
      kaiValueInput.value = "";
      kaiValueInput.placeholder = "Enter custom kai value";
    } else {
      kaiOtherField.style.display = "none";
      if (kaiValue) {
        kaiValueInput.value = parseInt(kaiValue) + kaiPosition;
      }
    }
  }

  // Roll Kai function
  window.rollKai = function () {
    var tierSelect = document.getElementById("cg-kai-tier");
    var kaiValueInput = document.getElementById("cg-kai-value");
    var kaiPositionInput = document.getElementById("kai-position");
    var randomKaiPosition = Math.floor(Math.random() * 1000);

    // Set kai-position
    kaiPositionInput.value = randomKaiPosition;

    // If a tier is already selected, update the kai value
    var selectedOption = tierSelect.options[tierSelect.selectedIndex];
    var kaiValue = selectedOption.getAttribute("data-kai");
    var tierValue = selectedOption.value;

    if (kaiValue && tierValue !== "Other") {
      kaiValueInput.value = parseInt(kaiValue) + randomKaiPosition;
    }
  };

  // Lineage change handler
  function handleLineageChange() {
    var lineageSelect = document.getElementById("cg-lineage");
    var lineageOtherField = document.getElementById("cg-lineage-other-field");
    var lineageValue = lineageSelect.options[lineageSelect.selectedIndex].value;

    // Disable the "Select lineage" option once a choice is made
    lineageSelect.options[0].disabled = true;

    if (lineageValue === "Other") {
      lineageOtherField.style.display = "flex";
    } else {
      lineageOtherField.style.display = "none";
    }
  }

  // Class change handler
  function handleClassChange() {
    var classSelect = document.getElementById("cg-class");
    // Disable the "Select class" option once a choice is made
    classSelect.options[0].disabled = true;
  }

  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", function () {
      window.rollAll();
      document.getElementById("cg-kai-tier").addEventListener("change", handleKaiTierChange);
      document.getElementById("cg-lineage").addEventListener("change", handleLineageChange);
      document.getElementById("cg-class").addEventListener("change", handleClassChange);
    });
  } else {
    window.rollAll();
    document.getElementById("cg-kai-tier").addEventListener("change", handleKaiTierChange);
    document.getElementById("cg-lineage").addEventListener("change", handleLineageChange);
    document.getElementById("cg-class").addEventListener("change", handleClassChange);
  }
})();
</script>
