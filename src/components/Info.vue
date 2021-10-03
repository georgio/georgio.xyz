<template>
  <div class="container mx-auto p-4 antialiased">
    <div class="flex items-center">
      <div class="flex-grow-0">
        <div
          class="
            font-mono
            self-center
            text-4xl
            tracking-tighter
            font-effect-anaglyph
          "
        >
          Georgio Nicolas
        </div>
      </div>
      <div class="flex-auto">
        <canvas id="canvas" width="160" height="220" />
      </div>
    </div>

    <div class="pb-1">
      I'm a member of the
      <a href="https://www.esat.kuleuven.be/cosic" target="_blank">
        COSIC group at KU Leuven
      </a>
      as a pre-doctoral student.
      <br />
      My research interests primarily revolve around the intersection of
      Cryptography and Privacy Enhancing Technologies.
    </div>

    <div class="py-1" v-if="nextConference.title">
      The next conference I will be attending is:
      <a :href="nextConference.url" target="_blank">
        {{ nextConference.title }}
      </a>
      <span
        v-if="nextConference.extraText"
        v-html="nextConference.extraText"
      />.
    </div>

    <div class="py-1">
      <div class="font-mono text-2xl font-black">Social Links:</div>
      <div class="font-mono antialiased">
        {
        <div class="grid grid-cols-2 ml-5">
          <template v-for="(link, i) in links" :key="i">
            <div class="col-end-1">
              {{ `"${link.title}": ` }}
            </div>
            <div class="col-start-1 ml-1">
              "<a :href="link.url" target="_blank"> {{ link.urlText }} </a>",
            </div>
          </template>
        </div>
        }
      </div>
    </div>

    <div class="py-1">
      <div class="font-mono text-2xl font-black">
        Projects I've Contributed To:
      </div>
      <div class="font-mono antialiased">
        {

        <div class="grid grid-cols-1 ml-5">
          <template v-for="(foss, i) in foss" :key="i">
            <div>
              "<a :href="foss.url" target="_blank"> {{ foss.title }} </a>":
              <span class="font-mono antialiased">
                [
                <div
                  v-for="(contribution, j) in foss.contributions"
                  :key="j"
                  class="ml-5"
                >
                  {{ `"${contribution}",` }}
                </div>
                ],
              </span>
            </div>
          </template>
        </div>
        }
      </div>
    </div>

    <div class="py-1">
      <div class="font-mono text-2xl font-black">Publications and Posts:</div>
      <div class="font-mono text-base">
        -
        <a href="https://eprint.iacr.org/2019/971"
          >Verifpal: Cryptographic Protocol Analysis for the Real World</a
        >
        (ACM CCSW 2020, Indocrypt 2020, Real World Crypto 2021)<br />
        -
        <a href="https://blog.symbolic.software/2020/04/05/dp-3t-verifpal"
          >How Verifpal Dramatically Sped Up the Formal Modeling Efforts for a
          New Pandemic-Tracing Protocol</a
        ><br />
        -
        <a
          href="https://www.computer.org/csdl/proceedings-article/euros&p/2019/114800a356/1cI6f6upxi8"
          >Noise Explorer: Fully Automated Modeling and Verification for
          Arbitrary Noise Protocols</a
        >
        (IEEE Euro S&P 2019)<br />
      </div>
    </div>

    <div class="py-1">
      <div class="font-mono text-2xl font-black">Links to stuff I like:</div>
      <div class="font-mono text-base">
        <a href="https://letterboxd.com/film/tampopo/"> Tampopo </a> <br />
        <a href="https://www.youtube.com/channel/UC9-y-6csu5WGm29I7JiwpnA">
          Computerphile
        </a>
        <br />
        <a href="https://www.quantamagazine.org/tag/the-joy-of-x-podcast/">
          The joy of x
        </a>
        <br />
        <a
          href="https://people.eecs.berkeley.edu/~christos/classics/Feynman.pdf"
        >
          Cool Paper#1
        </a>
        (<a href="https://www.youtube.com/watch?v=86x0_-JGlGQ">Related Talk</a>)
        <br />
        <a
          href="https://homepages.inf.ed.ac.uk/wadler/papers/propositions-as-types/propositions-as-types.pdf"
        >
          Cool Paper#2
        </a>
        (<a href="https://vimeo.com/100976695">Related Talk</a>)<br />
      </div>
    </div>
    <div class="py-1 font-mono">
      <div class="font-black font-bold text-2xl">E-mail Address:</div>
      <div>me[at]georgio[dot]xyz</div>
    </div>
  </div>
</template>
<script>
import info from "./info.json";
import { ref } from "vue";
export default {
  mounted() {
    this.drawAttractor();
  },
  data() {
    return {
      links: info.links,
      foss: info.foss,
      nextConference: info.nextConference,
    };
  },
  methods: {
    async drawAttractor() {
      return new Promise((resolve) => {
        const canvas = document.getElementById("canvas");

        canvas.style.width = "160px";
        canvas.style.height = "220px";
        let pixelScalingFactor = window.devicePixelRatio;
        canvas.width = Math.floor(canvas.width * pixelScalingFactor);
        canvas.height = Math.floor(canvas.height * pixelScalingFactor);
        const context = canvas.getContext("2d");
        context.scale(pixelScalingFactor, pixelScalingFactor);

        context.lineCap = "round";
        context.lineWidth = 0.5;

        let x = 0;
        let y = 1;
        let z = 13;

        const beta = 8.0 / 3.0;
        const sigma = 10;
        const rho = 28;

        const dt = 0.005;

        const initX = 80;
        const initY = 110;
        const scale = 4;

        let numIterations = 25519;

        const interval = setInterval(() => {
          if (numIterations != 0) {
            const dx = sigma * (y - x) * dt;
            const dy = (x * (rho - z) - y) * dt;
            const dz = (x * y - beta * z) * dt;

            context.beginPath();
            context.moveTo(initX + x * scale, initY + y * scale);
            x += dx;
            y += dy;
            z += dz;
            context.lineTo(initX + x * scale, initY + y * scale);
            context.stroke();

            numIterations -= 1;
          } else {
            clearInterval(interval);
            resolve();
          }
        }, dt);
      });
    },
  },
};
</script>
