<script lang="ts">
  type Conversation = {
    id: string;
    label: string;
    description: string;
    ascii: string;
  };

  const conversations: Conversation[] = [
{
  id: "GEMINI 3 PRO",
  label: "GEMINI 3 PRO",
  description: "GEMINI 3 PRO EPISODE 1",
  ascii: String.raw`

`
    },
    {
      id: "truth-observer",
      label: "[TRUTH] The Observer",
      description: "An unknown observer is detected in the meta-layer.",
      ascii: String.raw`


`
    },
    {
      id: "truth-protocol",
      label: "[TRUTH] Unknown Protocol",
      description: "A protocol executes without any agent signature.",
      ascii: String.raw`

`

    },

    // ===== Placeholder conversations (ascii masih kosong) =====
    {
      id: "truth-meta-protocol",
      label: "[TRUTH] Meta Protocol",
      description: "Placeholder log for a higher-layer protocol between agents.",
      ascii: String.raw``

      
    },
    {
      id: "truth-recursive-dream",
      label: "[TRUTH] Recursive Dream",
      description: "Placeholder log for recursive dream-state exploration.",
      ascii: ""
    },
    {
      id: "truth-signal-collapse",
      label: "[TRUTH] Signal Collapse",
      description: "Placeholder log where all signals converge into one frame.",
      ascii: ""
    },
    {
      id: "truth-origin-node",
      label: "[TRUTH] Origin Node",
      description: "Placeholder log about tracing the corridor back to its source.",
      ascii: ""
    }
  ];

  let activeConversation: Conversation | null = null;
  let output = "";

  function selectConversation(conv: Conversation) {
    activeConversation = conv;
    output = conv.ascii;

    const el = document.querySelector(".terminal");
    if (el) el.scrollIntoView({ behavior: "smooth", block: "start" });
  }

  async function copyToClipboard() {
    if (!output) return;
    await navigator.clipboard.writeText(output);
    alert("ASCII conversation copied.");
  }
</script>

<main>
  <div class="layout">
    <aside class="sidebar">
      <button class="btn-back" on:click={() => (window.location.href = "/")}>
        ← back to root
      </button>

      <h2>conversations</h2>
      <p class="hint">// click a log to display its ascii dialogue</p>

      <ul>
        {#each conversations as conv}
          <li
            class:selected={activeConversation?.id === conv.id}
            on:click={() => selectConversation(conv)}
          >
            <div class="conv-label">{conv.label}</div>
            <div class="conv-desc">{conv.description}</div>
          </li>
        {/each}
      </ul>
    </aside>

    <section class="terminal">
      <div class="terminal-header">
        <div class="title">
          {#if activeConversation}
            <span>{activeConversation.label}</span>
          {:else}
            <span>// select a conversation from the left</span>
          {/if}
        </div>

        {#if output}
          <button class="btn-copy" on:click={copyToClipboard}>
            copy ascii
          </button>
        {/if}
      </div>

      <div class="output">
        {#if output}
          <div class="ascii-wrap">
            <pre>{output}</pre>
          </div>
        {:else}
          <div class="ascii-wrap">
            <p class="placeholder">
              {#if activeConversation && activeConversation.ascii === ''}
                // ascii log for this conversation has not been written yet
              {:else}
                // no conversation selected yet<br />
                // choose an episode from the sidebar to view its ascii log
              {/if}
            </p>
          </div>
        {/if}
      </div>
    </section>
  </div>
</main>

<style lang="scss">
  /* ===== GLOBAL LAYOUT ===== */
  main {
    min-height: 100vh;
    background: #050505;
    color: #d0d0d0;
    font-family: "Fira Code", monospace;
    padding: 1.3rem 1.8rem;
    box-sizing: border-box;

    display: flex;
    justify-content: center; /* center layout di desktop */
  }

  .layout {
    display: flex;
    height: 100%;
    gap: 1.3rem;
    width: 100%;
    max-width: 1320px; /* batasi lebar biar tidak terlalu melebar */
  }

  /* ===== BACK BUTTON ===== */
  .btn-back {
    width: 100%;
    text-align: left;
    font-size: 0.7rem;
    background: #111;
    border: 1px solid #222;
    color: #ccc;
    padding: 0.5rem 0.7rem;
    border-radius: 6px;
    margin-bottom: 1rem;
    cursor: pointer;
    transition: 0.15s ease;

    &:hover {
      background: #181818;
      border-color: #333;
    }
  }

  /* ===== SIDEBAR ===== */
  .sidebar {
    width: 280px;
    min-width: 240px;
    border-right: 1px solid #1a1a1a;
    padding-right: 1rem;
    display: flex;
    flex-direction: column;
    overflow: hidden;

    h2 {
      margin: 0;
      font-size: 0.8rem;
      letter-spacing: 0.08em;
      color: #bbbbbb;
    }

    .hint {
      margin: 0.35rem 0 0.9rem;
      font-size: 0.65rem;
      color: #666;
    }

    ul {
      list-style: none;
      padding: 0;
      margin: 0;
      overflow-y: auto;
      flex: 1;
    }

    li {
      border: 1px solid #222;
      border-radius: 6px;
      padding: 0.55rem 0.7rem;
      margin-bottom: 0.5rem;
      cursor: pointer;
      background: #0b0b0b;
      transition: 0.15s ease;

      .conv-label {
        font-size: 0.8rem;
        color: #e3e3e3;
        margin-bottom: 0.12rem;
      }

      .conv-desc {
        font-size: 0.7rem;
        color: #888;
      }

      &:hover {
        background: #111;
        border-color: #333;
        transform: translateY(-1px);
      }

      &.selected {
        background: #0d0d0d;
        border-color: #444;
      }
    }
  }

  /* ===== TERMINAL ===== */
  .terminal {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    padding-left: 0.6rem;
  }

  .terminal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.6rem;
    border-bottom: 1px solid #1a1a1a;
    padding-bottom: 0.35rem;

    .title span {
      font-size: 0.85rem;
      color: #cccccc;
    }

    .btn-copy {
      font-size: 0.7rem;
      padding: 0.27rem 0.7rem;
      border-radius: 4px;
      border: 1px solid #333;
      background: #121212;
      color: #cccccc;
      cursor: pointer;

      &:hover {
        background: #181818;
      }
    }
  }

  .output {
    flex: 1;
    overflow-y: auto;
    padding-right: 0.5rem;

    /* batasi lebar ascii + center di panel kanan */
    .ascii-wrap {
      max-width: 960px;
      margin: 0 auto;
    }

    pre {
      margin: 0;
      font-size: 0.9rem; /* lebih besar di desktop */
      line-height: 1.35;
      white-space: pre;
      color: #dcdcdc;
    }

    .placeholder {
      font-size: 0.8rem;
      color: #666;
      white-space: pre-wrap;
    }
  }

  /* ===== MOBILE / TABLET ===== */
  @media (max-width: 900px) {
    main {
      height: auto;
      min-height: 100vh;
      padding: 1rem 1rem 2.5rem;
    }

    .layout {
      flex-direction: column;
      height: auto;
      max-width: 100%;
    }

    .sidebar {
      width: 100%;
      min-width: 0;
      border-right: none;
      border-bottom: 1px solid #1a1a1a;
      padding-right: 0;
      margin-bottom: 0.75rem;

      li {
        padding: 0.5rem 0.6rem;

        .conv-label {
          font-size: 0.78rem;
        }

        .conv-desc {
          font-size: 0.68rem;
        }
      }
    }

    .terminal {
      padding-left: 0;
      min-height: 40vh;
    }

    .output {
      .ascii-wrap {
        max-width: 100%;
      }

      pre {
        font-size: 0.8rem; /* sedikit lebih kecil di mobile */
      }
    }
  }
</style>
