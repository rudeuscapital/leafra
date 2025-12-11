<script lang="ts">
    import { onMount } from 'svelte';
    import RichPresence from '../molecules/RichPresence.svelte';
    import Tooltip from '../atoms/Tooltip.svelte';

    // ===== Efek mengetik otomatis =====
    let fullText = `In an era where artificial intelligence evolves faster than human understanding, LEAFRA emerges as a symbol of growth, balance, and digital evolution. LEAFRA perceives LLMs (Large Language Models) as a vast forest filled with branching logic, hundreds of thousands of connections, and streams of information that continuously grow, just like leaves absorbing light and transforming it into new energy.

LEAFRA is a crypto ecosystem that unites two fundamental forces:
🌱 The natural growth of trees
🤖 The knowledge structure of LLMs

From roots to leaves, LEAFRA is built to represent digital progress that remains connected to nature.
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
    /*   TYPING TEXT — FULL WHITE     */
    /* ============================== */
    .typing {
        font-family: var(--font-two);
        white-space: pre-line;
        font-size: 0.95rem;

        /* TEXT → PURE WHITE */
        color: #ffffff !important;

        /* CARET → PURE WHITE */
        border-right: 2px solid #ffffff;

        animation: blink 0.75s step-end infinite;
    }

    @keyframes blink {
        from, to {
            border-color: transparent;
        }
        50% {
            border-color: #ffffff;
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
