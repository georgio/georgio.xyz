<template>
  <div class="container mx-auto p-4 antialiased">
    <div class="flex items-center">
      <div class="grow-0">
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
      I'm a doctoral student under the supervision of <a href="https://homes.esat.kuleuven.be/~preneel/">Bart Preneel</a> and <a href="https://nigelsmart.github.io">Nigel Smart</a> at
      <a href="https://www.esat.kuleuven.be/cosic" target="_blank">
        COSIC, KU Leuven
      </a>.
      
      <br />
      My research interests primarily revolve around the intersection of
      Cryptography, (usable) Formal Methods and Privacy Enhancing Technologies.
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
        <a href="https://eprint.iacr.org/2025/576"
          >Pre-Constructed Publicly Verifiable Secret Sharing and Applications</a
        >
        (ACNS 2025)<br />
        -
        <a href="https://eprint.iacr.org/2024/662"
          >Faster Private Decision Tree Evaluation for Batched Input from Homomorphic Encryption</a
        >
        (SCN 2024)<br />
        -
        <a href="https://eprint.iacr.org/2024/559"
          >Convolution-Friendly Image Processing in FHE</a
        >
        (FHE.org Conference 2024)<br />
        -
        <a href="https://eprint.iacr.org/2023/274"
          >Panacea: Stateless and Non-Interactive Oblivious RAM</a
        >
        (IEEE Euro S&P 2024, FHE.org <a href="https://fhe.org/meetups/029-Panacea_Non-interactive_and_Stateless_Oblivious_RAM">Meetup</a> + Conference 2023)<br />
        -
        <a href="https://www.esat.kuleuven.be/cosic/blog/rwc-2022-a-new-security-model-uncovers-a-authentication-vulnerabilities-in-signal/"
          >A new security model uncovers authentication vulnerabilities in Signal</a
        > (COSIC Blog)<br />
        -
        <a href="https://eprint.iacr.org/2019/971"
          >Verifpal: Cryptographic Protocol Analysis for the Real World</a
        >
        (ACM CCSW 2020, Indocrypt 2020, Real World Crypto 2021)<br />
        -
        <a href="https://symbolic.software/blog/2020-04-05-dp3t/"
          >Modeling DP-3T with Verifpal</a
        > (Symbolic Software Blog)<br />
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
      <div class="font-mono text-2xl font-black">Supervised Masters Theses:</div>
      <div class="font-mono text-base">
        -
        <a href="https://kuleuven.limo.libis.be/discovery/fulldisplay?docid=alma9994890755901488&context=L&vid=32KUL_KUL:KULeuven&search_scope=All_Content&tab=all_content_tab&lang=en"
          >On Publicly Verifiable Secret Sharing Schemes and Applications</a
        > - Noah Knapen (2024)<br />
        -
        <a href="https://kuleuven.limo.libis.be/discovery/fulldisplay?docid=alma9993527084601488&context=L&vid=32KUL_KUL:KULeuven&search_scope=All_Content&tab=all_content_tab&lang=en"
          >A Deductively Verifiable Implementation of Shamir Secret Sharing in Rust</a
        > - Xander Fransen (2023)<br />
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
          The joy of {<a href="https://www.quantamagazine.org/tag/the-joy-of-x">x</a>, <a href="https://www.quantamagazine.org/tag/the-joy-of-why">wh(y)</a>}
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
      <div class="font-bold text-2xl">E-mail Address:</div>
      <div>me[at]georgio[dot]xyz</div>
    </div>
  </div>
</template>
<script>
import info from "./info.json";

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
