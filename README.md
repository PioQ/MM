# MM
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Marek's Page</title>
    <canvas id="cnv"> </canvas>
    <body style="background-color: rgb(83, 11, 11)"></body>
  </head>
  <body id="lucek"></body>
  <ol>
    <li>Hey!</li>
    <li>You!</li>
    <li>Yes! You!</li>
  </ol>
</html>

<script>
  lucek.style.background = 'grey';

  let li = document.querySelectorAll('ol>li');
  li[0].style.background = 'red';
  li[0].style.color = 'yellow';

  li[1].style.background = 'green';
  li[1].style.color = 'yellow';

  li[2].style.background = 'blue';
  li[2].style.color = 'yellow';

  const cnv = document.querySelector('#cnv');
  const ctx = cnv.getContext('2d');
  let borderX = 700;
  let borderY = 700;
  cnv.width = borderX; //window.innerWidth - 100;
  cnv.height = borderY; //window.innerHeight - 20;
  cnv.style.color = 'red';
  const numberOfDots = 100;
  const nodes = [];
  const maxDistance = 80;

  cnv.style =
    'position: absolute; top: 0px; left: 0px; right: 0px; bottom: 0px; margin: auto; border:2px solid rgb(73, 1, 3); background-color: rgb(83, 11, 11)';

  let checkDistance = (ax, ay, bx, by) => {
    let dx = bx - ax;
    let dy = by - ay;
    let distance = Math.sqrt(dx * dx + dy * dy);
    return distance;
  };

  for (let i = 0; i < numberOfDots; i++) {
    nodes.push({
      x: Math.random() * borderX,
      y: Math.random() * borderY,
      vx: Math.random() * 0.04 - 0.005,
      vy: Math.random() * 0.05 - 0.01,
    });
  }

  let animate = () => {
    ctx.clearRect(0, 0, cnv.width, cnv.height);

    for (let i = 0; i < numberOfDots - 1; i++) {
      let nodeA = nodes[i];
      for (let j = i + 1; j < numberOfDots; j++) {
        let nodeB = nodes[j];
        nodeA.x += nodeA.vx;
        nodeA.y += nodeA.vy;
        nodeB.x += nodeB.vx;
        nodeB.y += nodeB.vy;
        if (nodeA.x >= borderX) {
          nodeA.vx *= -1;
        }
        if (nodeA.x <= 0) {
          nodeA.vx *= -1;
        }
        if (nodeB.x >= borderX) {
          nodeB.vx *= -1;
        }
        if (nodeB.x <= 0) {
          nodeB.vx *= -1;
        }
        if (nodeA.y >= borderY) {
          nodeA.vy *= -1;
        }
        if (nodeA.y <= 0) {
          nodeA.vy *= -1;
        }
        if (nodeB.y >= borderY) {
          nodeB.vy *= -1;
        }
        if (nodeB.y <= 0) {
          nodeB.vy *= -1;
        }

        if (nodeA.x && nodeB.x < cnv.width && nodeA.y && nodeB.y < cnv.height) {
          let distance = checkDistance(nodeA.x, nodeA.y, nodeB.x, nodeB.y);
          if (distance < 7) {
            // [nodeA.vx, nodeB.vx] = [nodeB.vx, nodeA.vx];
            // [nodeA.vy, nodeB.vy] = [nodeB.vy, nodeA.vy];
            let vxTemp = nodeA.vx;
            let vyTemp = nodeA.vy;

            nodeA.vx = nodeB.vx;
            nodeB.vx = vxTemp;
            nodeA.vy = nodeB.vy;
            nodeB.vy = vyTemp;
          }

          // ctx.fillStyle = 'yellow';
          // ctx.lineWidth = 1;
          // ctx.beginPath();
          // ctx.arc(nodeA.x, nodeA.y, 1, 0, 2 * Math.PI, true);
          // ctx.fill();
          // ctx.closePath();

          if (distance < maxDistance) {
            //} && nodeA === nodes[0]) {
            ctx.lineWidth = maxDistance / 3 / distance;
            ctx.strokeStyle = 'red';
            ctx.beginPath();
            ctx.moveTo(nodeA.x, nodeA.y);
            ctx.lineTo(nodeB.x, nodeB.y);
            ctx.closePath();
            ctx.stroke();
          }
        }
      }
    }
    requestAnimationFrame(animate);
  };

  animate();

  // document.body.style.background = 'grey';
  // document.querySelectorAll('li')[0].style.background = 'red';
  // document.querySelectorAll('li')[0].style.color = 'yellow';

  // document.querySelectorAll('li')[1].style.background = 'green';
  // document.querySelectorAll('li')[1].style.color = 'yellow';

  // document.querySelectorAll('li')[2].style.background = 'blue';
  // document.querySelectorAll('li')[2].style.color = 'yellow';
</script>
