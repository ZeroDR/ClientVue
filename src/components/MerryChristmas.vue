<template>
    <div class="panel-merry">
        <canvas id="merry"></canvas>
    </div>
</template>
<script>
    export default {
        name: 'merry',
        data() {
            return {};
        },
        mounted() {
            let c = document.getElementById('merry');
            this.createMerry(c.getContext('2d'), c);
        },
        created() {

        },
        methods: {
            createMerry(a, c) {
                let M = Math;
                let Q = M.random;
                let J = [];
                let U = 16;
                let T = M.sin;
                let E = M.sqrt;
                let W = 1200;
                let x, z, j, i, k, O = 0;
                let I, H, y, R, P, D, B, L, V, A, font;
                for (O, k = 0; x = z = j = i = k < 370;) {
                    let cvs = M[k] = k ? c.cloneNode(0) : c;
                    cvs.width = W;
                    cvs.height = k ? 32 : 500;
                    let c2d = cvs.getContext('2d');
                    if (k > 10 || !k)
                        for (font = '60px Impact',
                                 V = 'rgba('; I = i * U,
                                 c2d.fillStyle = k ? k === 13 ? V + '255,255,255,.15)' : V + (147 + I) + ',' + (k % 2 ? 128 + I : 0) + ',' + I + ',.5)' : '#cca',
                             i < 7;)
                            c2d.beginPath(c2d.fill(c2d.arc(U - i / 3, 24 - i / 2, k === 13 ? 4 - (i++) / 2 : 8 - i++, 0, M.PI * 2, 1)));
                    else
                        for (; x = T(i),
                                   y = Q() * 2 - 1,
                                   D = x * x + y * y,
                                   B = E(D - x / .9 - 1.5 * y + 1),
                                   R = 67 * (B + 1) * (L = k / 9 + .8) >> 1,
                               i++ < W;)
                            if (D < 1)
                                c2d.beginPath(c2d.strokeStyle = V + R + ',' + (R + B * L >> 0) + ',40,.1)'),
                                    c2d.moveTo(U + x * 8, U + y * 8),
                                    c2d.lineTo(U + x * U, U + y * U),
                                    c2d.stroke();
                    for (y = H = k + E(k++) * 25,
                             R = Q() * W; P = 3,
                         j < H;)
                        J[O++] = [x += T(R) * P + Q() * 6 - 3, y += Q() * U - 8, z += T(R - 11) * P + Q() * 6 - 3, j / H * 20 + ((j += U) > H & Q() > .8 ? Q(P = 9) * 4 : 0) >> 1]
                }
                setInterval(function G(m, l) {
                    A = T(D - 11);
                    if (l) {
                        return (m[2] - l[2]) * A + (l[0] - m[0]) * T(D);
                    }
                    a.clearRect(0, 0, W, W);
                    J.sort(G);
                    for (i = 0; L = J[i++]; a.drawImage(M[L[3] + 1], 207 + L[0] * A + L[2] * T(D) >> 0, L[1] >> 1)) {
                        if (i === 2e3)
                            a.fillText('', U, 345);
                        if (!(i % 7))
                            a.drawImage(M[13], ((157 * (i * i) + T(D * 5 + i * i) * 5) % W) >> 0, ((113 * i + (D * i) / 60) % (290 + i / 99)) >> 0);
                    }
                    D += .02
                }, 1)
            }
        }
    };
</script>
<style scoped>
    .panel-merry {
    }
</style>
