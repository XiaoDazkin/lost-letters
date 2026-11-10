Game notes · MD
Game Notes — Lost Letters

🐛 Debugging
JS is case sensitive. Typos like fillstyle fail silently (black box = the colour didn't stick).
One error stops everything below it. If things disappear or freeze, look for the first red error in the console.
ctx.save without () does nothing and shows no error. Functions need () to run.

🎨 Canvas drawing
Canvas never erases itself. Paint the background first every frame — it's the eraser.
Settings stay switched on until you change them (fillStyle, textAlign, textBaseline…).
fillStyle is used by whatever draws next, so switch colours between shapes.
rgba(..., 0.5) — the 4th number is transparency (0 = invisible, 1 = solid).
js
ctx.arc(400, appleY, 25, 0, Math.PI * 2);
//       x     y    size start  end
Bar / ring = part ÷ whole.

🔁 Game loop & screens
A screen variable is the sticky note; loop() reads it every frame to decide what to run.
addEventListener adds, it doesn't replace. Never put it inside another listener or the loop.
Lost wand → skip update(), but keep draw().
A message that lasts = a timer counting down (set to 60, take away 1 per frame).
Check the number, not the text.

📷 Webcam
<video> is a hidden video player. The camera plays into it; you never see it directly.
getUserMedia({ video: true }) asks the browser "can I use the camera?"
.then(function (stream) {...}) = "when the camera is ready, do this." Cameras take a moment to wake up, so JS waits instead of freezing.
video.srcObject = stream plugs the camera into the hidden player.
Hidden video → call video.play() or it may freeze.
drawImage(video, 0, 0, 800, 600) copies the current camera picture onto the canvas every frame.
Mirroring
save() — remember the normal settings
translate(800, 0) — slide the drawing point to the right edge
scale(-1, 1) — flip left↔right (-1 = flip x, 1 = keep y)
drawImage(...) — draw the camera, now mirrored
restore() — back to normal, so apples and score aren't flipped backwards 🙃

🟢 Reading pixels
getImageData grabs every pixel number off the canvas as one long list.
for (...; i += 4) walks the list 4 numbers at a time (one pixel = R, G, B, A). Same as Python's for, written differently.
Set a pixel to (0, 255, 0) = pure green. putImageData paints edited pixels back.
Old fixed red rule: r > 180 && g < 80 && b < 80 (replaced by the scanned wand colour).
Add positions inside the same if that counts, or sum and count don't match.
Stray matching pixels pull the average toward them → fixed in Week 3 by only counting pixels near the wand.

📦 Variables, lists & bags
A const / let made inside { } only exists inside those { }.
list[0] = first item. list.length = how many. (Not Python's len()!)
while repeats as long as it's true. return hands a value back.
new X(...) builds a fresh bag of a built-in kind.

🔊 Voice
new SpeechSynthesisUtterance(text) makes a "sentence to speak" bag 🎒
speak() needs that bag, not plain text.
cancel() first, so voices don't pile up and queue.
Talking is a "once" thing — call say() at the event, never in draw().

🎯 Catching a change (once, not every frame)
Remember the old value
Set the new one
Compare: now true AND before false

