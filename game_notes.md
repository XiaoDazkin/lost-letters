JS is case sensitive. Typos in names like fillStyle fail silently. Black box = color didn't stick.

Canvas never erases itself. Paint the background first every frame, it’s the eraser.

ctx.arc(400, appleY, 25, 0, Math.PI * 2);
//       x     y     size start  end

r > 180 && g < 80 && b < 80

<video> is a hidden video player. The camera plays into it, and you never see it directly.
getUserMedia({ video: true }) asks the browser: “can I use the camera?”
.then(function (stream) {...}) means “when the camera is ready, do this.” Cameras take a moment to wake up, so JS waits instead of freezing.
video.srcObject = stream plugs the camera into the hidden player.
drawImage(video, 0, 0, 800, 600) is the new part: every frame, it copies the current camera picture onto your canvas, filling the whole thing.

Hidden video → call video.play() or it may freeze. 

save(): remember the normal settings.
translate(800, 0): slide the drawing point to the right edge.
scale(-1, 1): flip left↔right (-1 = flip x, 1 = keep y).
drawImage(...): draw the camera, now mirrored.
restore(): go back to normal, so anything drawn after (apples, score) isn’t flipped. Otherwise your score text would come out backwards 🙃

getImageData grabs every pixel number off the canvas, all 800 × 600 of them, as one long list.
for (...; i += 4) walks through the list 4 numbers at a time (one pixel = R, G, B, A). It’s the same as Python’s for, just written differently.
Inside the if, we set that pixel to (0, 255, 0), which is pure green.
putImageData paints the edited pixels back onto the canvas.

Careful with “the edges don’t matter” 👀 Those corner dots don’t touch the apples, but they do count in your average. Every stray green pixel pulls the circle a little toward it. If the circle ever drifts or wobbles, that’s why. We’ll fix it properly when we build the real wand, so just note it in game_notes.md for now.

A screen variable is the sticky note, and loop() reads it every frame to decide what to run.
Canvas settings like textAlign stay switched on until you change them.

“addEventListener adds, it doesn’t replace. Never put it inside another listener or the loop.”

“One error stops everything below it. If things disappear, look for the first red error in the console.”

“A const/let made inside { } only exists inside those { }.”

ctx.save without () does nothing and shows no error. Functions need () to run.

“Add positions inside the same if that counts, or sum and count don’t match.”

“fillStyle is used by whatever draws next, so switch colours between shapes.”
“rgba(..., 0.5): the 4th number is transparency.”
“Lost wand → skip update(), but keep draw().”

