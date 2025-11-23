<div id="carrossel-container"></div>

<script>
  function createCarousel(images, intervalMs = 3000) {
    if (!images || !images.length) return;

    const container = document.getElementById('carrossel-container');
    Object.assign(container.style, {
      position: 'relative',
      width: '100%',
      maxWidth: '900px',
      margin: '20px auto',
      overflow: 'hidden',
      borderRadius: '12px',
      backgroundColor: '#111',
    });

    const track = document.createElement('div');
    Object.assign(track.style, {
      display: 'flex',
      transition: 'transform 600ms ease',
      height: '0',
      paddingBottom: '56.25%', // proporção 16:9
    });

    images.forEach(src => {
      const slide = document.createElement('div');
      Object.assign(slide.style, {
        minWidth: '100%',
        height: '100%',
        position: 'relative',
        flexShrink: 0,
      });

      const img = document.createElement('img');
      img.src = src;
      Object.assign(img.style, {
        position: 'absolute',
        top: 0,
        left: 0,
        width: '100%',
        height: '100%',
        objectFit: 'cover',
      });

      slide.appendChild(img);
      track.appendChild(slide);
    });

    container.appendChild(track);

    function makeControl(text, side) {
      const btn = document.createElement('button');
      btn.innerHTML = text;
      Object.assign(btn.style, {
        position: 'absolute',
        top: '50%',
        transform: 'translateY(-50%)',
        [side]: '10px',
        zIndex: 40,
        border: 'none',
        padding: '8px 12px',
        borderRadius: '6px',
        background: 'rgba(0,0,0,0.45)',
        color: 'white',
        cursor: 'pointer',
        fontSize: '18px',
      });
      container.appendChild(btn);
      return btn;
    }

    const prevBtn = makeControl('‹', 'left');
    const nextBtn = makeControl('›', 'right');

    let current = 0;
    function update() {
      track.style.transform = `translateX(-${current * 100}%)`;
    }

    prevBtn.onclick = () => {
      current = (current - 1 + images.length) % images.length;
      update();
    };
    nextBtn.onclick = () => {
      current = (current + 1) % images.length;
      update();
    };

    setInterval(() => {
      current = (current + 1) % images.length;
      update();
    }, intervalMs);

    update();
  }

  // **Aqui use suas URLs hospedadas no Blogger**
  createCarousel([
    "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEisUnwNlCrZ79b1Xa9iFiVun8-EBZevfd3VMUYAblJFHejOToIUbig9bzWTl_QndNf7i9lLocxpFx92z0zKcE7uhXw4lijOTeMz5Gtj70mORG3TYfITEEQb_TZo-nl6al-s0BarPRfof6Kd9m5d3hyphenhyphenua0aSLyanO4b7oZIgPUD0YCFAHeoImgqSI72WATZX/s1414/0%20Capa%20bingoint.jpg",
    "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi-vRbsvteTqLhpRicJr6pooqOPF361YiCvcix-3U8dGmaZ7hr0HmGCf8diQQM7oyGsmVFMOp0CdV8nl-mjuBNBoxo1EVJoUxiafrmCVKsXcaEo62NU-KK-_5_4vJmTjAIZesUpdXZWZidUrm1N8Q04jPqV-El3YJaMkigyj-EhZc2FlqlRwwpV74p23C96/s2600/1%20sobrecap%20bingoint.jpg"
  ], 3000);
</script>
