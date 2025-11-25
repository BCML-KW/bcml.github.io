---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: hero
    content:
      title: |
        Bio Computing & Machine Learning Lab
      image:
        filename: welcome.jpg
      text: |
        <canvas id="neuralNetwork" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; opacity: 0.3;"></canvas>
        <script>
        (function() {
          const canvas = document.getElementById('neuralNetwork');
          const ctx = canvas.getContext('2d');
          let width, height;
          const neurons = [];
          const numNeurons = 30;
          
          function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            const dpr = window.devicePixelRatio || 1;
            
            width = rect.width;
            height = rect.height;
            
            canvas.width = width * dpr;
            canvas.height = height * dpr;
            
            ctx.setTransform(1, 0, 0, 1, 0, 0);
            ctx.scale(dpr, dpr);
          }
          
          class Neuron {
            constructor() {
              this.reset();
            }
            
            reset() {
              this.x = Math.random() * width;
              this.y = Math.random() * height;
              this.vx = (Math.random() - 0.5) * 0.5;
              this.vy = (Math.random() - 0.5) * 0.5;
              this.radius = 2;
            }

            update() {
              this.x += this.vx;
              this.y += this.vy;
              if (this.x < 0 || this.x > width) this.vx *= -1;
              if (this.y < 0 || this.y > height) this.vy *= -1;
            }

            draw() {
              ctx.beginPath();
              ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
              ctx.fillStyle = 'rgba(138, 22, 1, 0.8)';
              ctx.fill();
            }
          }

          function initNeurons() {
            neurons.length = 0;
            for (let i = 0; i < numNeurons; i++) {
              neurons.push(new Neuron());
            }
          }

          function connectNeurons() {
            for (let i = 0; i < neurons.length; i++) {
              for (let j = i + 1; j < neurons.length; j++) {
                const dx = neurons[i].x - neurons[j].x;
                const dy = neurons[i].y - neurons[j].y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                if (distance < 100) {
                  ctx.beginPath();
                  ctx.moveTo(neurons[i].x, neurons[i].y);
                  ctx.lineTo(neurons[j].x, neurons[j].y);
                  ctx.strokeStyle = 'rgba(138, 22, 1, ' + (0.4 * (1 - distance / 100)) + ')';
                  ctx.lineWidth = 1;
                  ctx.stroke();
                }
              }
            }
          }

          function animate() {
            ctx.clearRect(0, 0, width, height);
            connectNeurons();
            neurons.forEach(neuron => {
              neuron.update();
              neuron.draw();
            });
            requestAnimationFrame(animate);
          }
          
          // Initialize after a short delay to ensure proper layout
          setTimeout(function() {
            resizeCanvas();
            initNeurons();
            animate();
          }, 100);
          
          window.addEventListener('resize', function() {
            resizeCanvas();
            neurons.forEach(neuron => neuron.reset());
          });
        })();
        </script>
        <div class="hero-copy">
          <p>At BCML, we explore the intersection of biology, computation, and machine learning to push computational neuroscience forward.</p>
          <p>Our research focuses on Spiking Neural Networks, Reinforcement Learning, and Medical AI to advance healthcare innovation.</p>
          <p class="hero-location">Department of Computer Engineering, Kwangwoon University, Seoul, South Korea</p>
        </div>
  
  - block: collection
    content:
      title: Research Projects
      subtitle: 'Explore our cutting-edge research'
      text:
      count: 5
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: project
    design:
      view: showcase
      columns: '1'
  
  - block: collection
    content:
      title: Latest Publications
      text: ""
      count: 5
      filters:
        folders:
          - publication
        publication_type: ''
    design:
      view: citation
      columns: '1'
      css_class: latest-publications-gif

  - block: markdown
    content:
      title:
      subtitle:
      text: |
        {{% cta cta_link="./people/" cta_text="Meet the team →" %}}
    design:
      columns: '1'
      css_class: bcml-gif-section
---
