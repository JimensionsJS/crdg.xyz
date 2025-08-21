<!-- Countdown Table -->
<table style="border-collapse: collapse; background: #000; color: #fff; width: 100%; max-width: 500px; margin: auto; text-align: center; font-family: Arial, sans-serif; border: 1px solid #ddd;">
  <tr>
    <th style="font-size: 15pt; padding: 10px; border: 1px solid #ddd;">Global Schedule</th>
    <td style="border: 1px solid #ddd; padding: 10px;">
      <div id="phase" style="font-size: 1.25em; font-weight: bold; margin-bottom: 4px;">Loading...</div>
      <div id="timer" style="font-size: 2.1em; font-family: 'Comic Neue', sans-serif;">--:--:--</div>
    </td>
  </tr>
</table>

<script>
(function() {
  const elTimer = document.getElementById("timer");
  const elPhase = document.getElementById("phase");

  const dailyPhases = [
    { name: "Mid-Day Phase", windows: [{start: "08:00", end: "09:00"}, {start: "20:00", end: "21:00"}] },
    { name: "Night Phase", windows: [{start: "01:00", end: "02:00"}, {start: "13:00", end: "14:00"}] }
  ];

  function parseTime(timeStr) {
    const [h,m] = timeStr.split(":").map(Number);
    return {h,m};
  }

  function update() {
    const now = new Date();
    const nowUTC = new Date(now.getTime() + now.getTimezoneOffset() * 60000);
    
    let currentPhase = null;
    let timeLeft = 0;

    for (let phase of dailyPhases) {
      for (let window of phase.windows) {
        const startT = parseTime(window.start);
        const endT = parseTime(window.end);

        const start = new Date(Date.UTC(
          nowUTC.getUTCFullYear(), nowUTC.getUTCMonth(), nowUTC.getUTCDate(),
          startT.h, startT.m, 0
        ));
        const end = new Date(Date.UTC(
          nowUTC.getUTCFullYear(), nowUTC.getUTCMonth(), nowUTC.getUTCDate(),
          endT.h, endT.m, 0
        ));

        if (nowUTC >= start && nowUTC < end) {
          currentPhase = phase;
          timeLeft = end - nowUTC;
          break;
        }

        if (nowUTC < start && (!currentPhase || start < currentPhase.nextStart)) {
          currentPhase = {...phase, nextStart: start};
          timeLeft = start - nowUTC;
        }
      }
      if (currentPhase && currentPhase.nextStart && timeLeft > 0) break;
    }

    elPhase.textContent = currentPhase.name;

    const h = Math.floor(timeLeft / 3600000);
    const m = Math.floor((timeLeft % 3600000) / 60000);
    const s = Math.floor((timeLeft % 60000) / 1000);

    elTimer.textContent =
      (h > 0 ? h + "h " : "") +
      String(m).padStart(2,"0") + "m " +
      String(s).padStart(2,"0") + "s";
  }

  update();
  setInterval(update, 1000);
})();
</script>

---

The **Blimp** is a feature added on **August 18th, 2025**. Whenever the time in-game reaches night or noon, the **Blimp** will come flying to either the [[Gas Station]] or [[content/Places/Cathedral|Cathedral]] and stay there for a few hours. 

---
## Overview

When inside of the **Blimp**, you will be prompted by the owner, **Filbubar**. He’s an anthropomorhic bear wearing sunglasses and owns the store. Along with him are three stands with a randomly selected decoration to buy honey with, the prices of them chosen by luck. After night ends, **Filbubar** will drive the blimp back off into the sky and restock once it’s night time again.
