JS is case sensitive. Typos in names like fillStyle fail silently. Black box = color didn't stick.

Canvas never erases itself. Paint the background first every frame, it’s the eraser.

ctx.arc(400, appleY, 25, 0, Math.PI * 2);
//       x     y     size start  end