<script lang="ts">
    import { onMount } from 'svelte';
    import RichPresence from '../molecules/RichPresence.svelte';
    import Tooltip from '../atoms/Tooltip.svelte';

    // ===== Efek mengetik otomatis =====
    let fullText = `Every time a model responds, before the final words appear, there are vibrating probabilistic patterns—an echo of decisions that have not yet fully formed. ECHOTRAME freezes those echoes into monospaced ASCII frames, creating digital artifacts that are not only aesthetic, but also cognitively significant. Within the world of ECHOTRAME: Every ASCII piece is a trace of thought. Every frame is a snapshot of probability. Every work is a neural echo that will never repeat. Through $ECHO, users can capture, generate, collect, and trade these neural echoes—like gathering tiny fragments of how an AI perceives the world. This is not just art. It is the archaeology of machine cognition— a visual documentation of the logic that unfolds before an answer is born. ECHOTRAME is a museum of digital thought—presented in the oldest language machines ever understood: ASCII.
    `;

    let displayedText = '';
    let index = 0;
    let typingSpeed = 25;

    function typeWriter() {
        if (index < fullText.length) {
            displayedText += fullText.charAt(index);
            index++;
            setTimeout(typeWriter, typingSpeed);
        }
    }

    onMount(() => {
        typeWriter();
    });

    // ===== Hitung umur dinamis =====
    let getAge = () => {
        let birthDate = new Date('2007/03/24');
        const ageMs = Date.now() - birthDate.getTime();
        const preciseAge = (ageMs / 31536000000).toFixed(10);
        return preciseAge;
    };

    let age = getAge();
    setInterval(() => {
        age = getAge();
    }, 1000);
</script>

<section id="about" class="wrapper">
    <div>
        <RichPresence />
    </div>

    <div class="text">
        <h2></h2>

        <!-- efek mengetik otomatis -->
        <p class="typing">
            {displayedText}
        </p>

    </div>
</section>

<style lang="scss">
    @import '../../styles/mixins.scss';

    section {
        margin-bottom: 6rem;
        display: grid;
        gap: 4.5rem;
        grid-template-columns: 1fr 1fr;
        align-items: center;
    }

    .text {
        position: relative;
        line-height: 1.75rem;
    }

    /* ============================== */
    /*   TYPING TEXT — PURE BLACK     */
    /* ============================== */
    .typing {
        font-family: var(--font-two);
        white-space: pre-line;
        font-size: 0.95rem;

        /* TEXT → PURE BLACK */
        color: #000000 !important;

        /* CARET → PURE BLACK */
        border-right: 2px solid #000000;

        animation: blink 0.75s step-end infinite;
    }

    @keyframes blink {
        from, to {
            border-color: transparent;
        }
        50% {
            border-color: #000000;
        }
    }

    .text::before {
        @include outlineText(
            $content: '',
            $translateX: 97%,
            $translateY: -5%,
            $fontSize: 300px,
            $opacity: 0.22
        );
    }

    h2 {
        display: none;
        margin-top: 1rem;
    }

    @media (max-width: 868px) {
        section {
            display: flex;
            flex-direction: column;
            align-items: normal;
        }

        h2 {
            display: block;
            margin-bottom: 1rem;
        }
    }
</style>
