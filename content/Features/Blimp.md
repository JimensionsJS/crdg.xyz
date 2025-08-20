<div class="countdown-box" data-interval="10800000" style="text-align:center;background:#000;color:#fff;padding:10px;font-family:Arial;">
  <div style="font-size:1.25em;font-weight:bold;margin-bottom:6px;">Next event starts in...</div>
  <div class="countdown-timer" style="font-size:2.1em;font-family:'Comic Neue',sans-serif;">--:--:--</div>
</div>
<script>
(function() {
  function startCountdown(el) {
    const interval = parseInt(el.dataset.interval, 10) || 3*60*60*1000; // default 3h
    const timer = el.querySelector(".countdown-timer");

    function update() {
      const now = Date.now();
      const timeInto = now % interval;
      const timeLeft = interval - timeInto;
      const h = Math.floor(timeLeft / 3600000);
      const m = Math.floor((timeLeft % 3600000) / 60000);
      const s = Math.floor((timeLeft % 60000) / 1000);
      timer.textContent =
        (h > 0 ? h + "h " : "") +
        String(m).padStart(2, "0") + "m " +
        String(s).padStart(2, "0") + "s";
    }
    update();
    setInterval(update, 1000);
  }

  document.querySelectorAll(".countdown-box").forEach(startCountdown);
})();
</script>

---

The **Blimp** is a feature added on **August 18th, 2025**. Whenever the time in-game reaches night or noon, the **Blimp** will come flying to either the [[Gas Station]] or [[content/Places/Cathedral|Cathedral]] and stay there for a few hours. 

---
## Overview

When inside of the **Blimp**, you will be prompted by the owner, **Filbubar**. He’s an anthropomorhic bear wearing sunglasses and owns the store. Along with him are three stands with a randomly selected decoration to buy honey with, the prices of them chosen by luck. After night ends, **Filbubar** will drive the blimp back off into the sky and restock once it’s night time again.