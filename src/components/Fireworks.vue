<template>
    <div class="fire-panel">
        <canvas id="fireworks"></canvas>
    </div>
</template>

<script>
    import {Particle} from "../handle/Fireworks/Particle";
    import {Firework} from "../handle/Fireworks/Firework";

    export default {
        name: 'fireworks',
        data() {
            return {
                canvas: undefined,
                ctx: undefined,
                cw: 0,
                ch: 0,
                mx: 0,
                my: 0,
                fireworks: [],
                particles: [],
                hue: 120,
                limiterTotal: 5,
                limiterTick: 0,
                timerTotal: 80,
                timerTick: 0,
                mousedown: false
            };
        },
        components: {},
        mounted() {
            this.canvas = document.getElementById('fireworks');
            this.setCanvas();
            this.ready();
        },
        created() {
            window.requestAnimFrame = (function () {
                return window.requestAnimationFrame ||
                    window.webkitRequestAnimationFrame ||
                    window.mozRequestAnimationFrame ||
                    function (callback) {
                        window.setTimeout(callback, 1000 / 60);
                    };
            })();
        },
        methods: {
            setCanvas() {
                let _this = this;
                this.ctx = this.canvas.getContext('2d');
                // full screen dimensions
                this.cw = window.innerWidth;
                this.ch = window.innerHeight;
                // firework collection
                this.fireworks = [];
                // particle collection
                this.particles = [];
                // starting hue
                this.hue = 240;
                // when launching fireworks with a click, too many get launched at once without a limiter, one launch per 5 loop ticks
                this.limiterTotal = 5;
                this.limiterTick = 0;
                // this will time the auto launches of fireworks, one launch per 80 loop ticks
                this.timerTotal = 80;
                this.timerTick = 0;
                this.mousedown = false;
                // mouse x coordinate,
                this.mx = 0;
                // mouse y coordinate
                this.my = 0;
                // set canvas dimensions
                this.canvas.width = this.cw;
                this.canvas.height = this.ch;

                // mouse event bindings
                // update the mouse coordinates on mousemove
                this.canvas.addEventListener('mousemove', function (e) {
                    _this.mx = e.pageX - _this.canvas.offsetLeft;
                    _this.my = e.pageY - _this.canvas.offsetTop;
                });

                // toggle mousedown state and prevent canvas from being selected
                this.canvas.addEventListener('mousedown', function (e) {
                    e.preventDefault();
                    this.mousedown = true;
                });

                this.canvas.addEventListener('mouseup', function (e) {
                    e.preventDefault();
                    this.mousedown = false;
                });


            },

            random(min, max) {
                return Math.random() * (max - min) + min;
            },

            createParticles(x, y) {
                let particleCount = 30;
                while (particleCount--) {
                    this.particles.push(new Particle(x, y, this.hue, this.random, this.particles));
                }
            },

            calculateDistance(p1x, p1y, p2x, p2y) {
                let xDistance = p1x - p2x;
                let yDistance = p1y - p2y;
                return Math.sqrt(Math.pow(xDistance, 2) + Math.pow(yDistance, 2));
            },

            ready() {

                requestAnimFrame(this.ready);

                this.hue += 0.5;

                // normally, clearRect() would be used to clear the canvas
                // we want to create a trailing effect though
                // setting the composite operation to destination-out will allow us to clear the canvas at a specific opacity, rather than wiping it entirely
                this.ctx.globalCompositeOperation = 'destination-out';
                // decrease the alpha property to create more prominent trails
                this.ctx.fillStyle = 'rgba(0, 0, 0, 0.5)';
                this.ctx.fillRect(0, 0, this.cw, this.ch);
                // change the composite operation back to our main mode
                // lighter creates bright highlight points as the fireworks and particles overlap each other
                this.ctx.globalCompositeOperation = 'lighter';

                let text = "";
                this.ctx.font = "50px sans-serif";
                let textData = this.ctx.measureText(text);
                this.ctx.fillStyle = "rgba(" + parseInt(this.random(0, 255)) + "," + parseInt(this.random(0, 255)) + "," + parseInt(this.random(0, 255)) + ",0.3)";
                this.ctx.fillText(text, this.cw / 2 - textData.width / 2, this.ch / 2);

                // loop over each firework, draw it, update it
                let lf = this.fireworks.length;
                while (lf--) {
                    this.fireworks[lf].draw(this.ctx, this.hue);
                    this.fireworks[lf].update(lf, this.fireworks, this.calculateDistance, this.createParticles);
                }

                // loop over each particle, draw it, update it
                let pl = this.particles.length;
                while (pl--) {
                    this.particles[pl].draw(this.ctx);
                    this.particles[pl].update(pl, this.particles);
                }

                // launch fireworks automatically to random coordinates, when the mouse isn't down
                if (this.timerTick >= this.timerTotal) {
                    if (!this.mousedown) {
                        // start the firework at the bottom middle of the screen, then set the random target coordinates, the random y coordinates will be set within the range of the top half of the screen

                        for (let h = 0; h < 50; h++) {
                            this.fireworks.push(new Firework(this.cw / 2, this.ch / 2, this.random(0, this.cw), this.random(0, this.ch), this.random, this.calculateDistance));
                        }
                        this.timerTick = 0;
                    }
                } else {
                    this.timerTick++;
                }

                // limit the rate at which fireworks get launched when mouse is down
                if (this.limiterTick >= this.limiterTotal) {
                    if (this.mousedown) {
                        // start the firework at the bottom middle of the screen, then set the current mouse coordinates as the target
                        this.fireworks.push(new Firework(this.cw / 2, this.ch / 2, this.mx, this.my, this.random, this.calculateDistance));
                        this.limiterTick = 0;
                    }
                } else {
                    this.limiterTick++;
                }
            }
        }
    }
</script>

<style scoped>
    .fire-panel {
        background: #000;
        height:100%;
        width:100%;
    }
</style>