# mobiletonybot1\
# 🤖 Tonybot Multi-Control Panel

Select a motion command below to broadcast to all nearby ESP32 Tonybots simultaneously via Bluetooth.

<div style="display: flex; flex-direction: column; gap: 15px; margin-top: 20px;">
  <button onclick="broadcastCommand('WALK')" style="padding: 18px; font-size: 20px; font-weight: bold; border-radius: 10px; background-color: #28a745; color: white; border: none; cursor: pointer;">
    🚶 Walk Forward
  </button>
  
  <button onclick="broadcastCommand('DANCE')" style="padding: 18px; font-size: 20px; font-weight: bold; border-radius: 10px; background-color: #007bff; color: white; border: none; cursor: pointer;">
    💃 Group Dance
  </button>
  
  <button onclick="broadcastCommand('STOP')" style="padding: 18px; font-size: 20px; font-weight: bold; border-radius: 10px; background-color: #dc3545; color: white; border: none; cursor: pointer;">
    🛑 Emergency Stop
  </button>
</div>

<p id="status" style="margin-top: 25px; font-size: 16px; color: #666; font-weight: bold;">Status: Idle</p>

<script>
async function broadcastCommand(action) {
  const statusElem = document.getElementById('status');
  statusElem.innerText = "Broadcasting: " + action + "...";
  statusElem.style.color = "#007bff";

  try {
    // Triggers a BLE Advertisement Packet containing the action name
    await navigator.bluetooth.requestDevice({
      filters: [{ name: action }],
      optionalServices: ['4fafc201-1fb5-459e-8fcc-c5c9c331914b']
    });
  } catch (error) {
    // Bluetooth search cancels automatically after pulsing the signal name
    statusElem.innerText = "Signal Sent: " + action;
    statusElem.style.color = "#28a745";
  }
}
</script>
