<script lang="ts">
  type Conversation = {
    id: string;
    label: string;
    description: string;
    ascii: string;
  };

  const conversations: Conversation[] = [
    {
      id: "leafra-ep-1",
      label: "LEAFRA EPISODE 1",
      description: "VERDIGMA LAUNCH",
      ascii: String.raw``
    },
    {
      id: "leafra-ep-2",
      label: "LEAFRA EPISODE 2",
      description: "Episode 2 of the Leafra narrative.",
      ascii: String.raw`…`
    },
    {
      id: "leafra-ep-3",
      label: "LEAFRA EPISODE 3",
      description: "Episode 3 of the Leafra narrative.",
      ascii: String.raw`…`
    },
    {
      id: "leafra-ep-4",
      label: "LEAFRA EPISODE 4",
      description: "Episode 4 of the Leafra narrative.",
      ascii: String.raw``
    },
    {
      id: "leafra-ep-5",
      label: "LEAFRA EPISODE 5",
      description: "Episode 5 of the Leafra narrative.",
      ascii: ""
    },
    {
      id: "leafra-ep-6",
      label: "LEAFRA EPISODE 6",
      description: "Episode 6 of the Leafra narrative.",
      ascii: ""
    },
    {
      id: "leafra-ep-7",
      label: "LEAFRA EPISODE 7",
      description: "Episode 7 of the Leafra narrative.",
      ascii: ""
    },
    {
      id: "leafra-ep-8",
      label: "LEAFRA EPISODE 8",
      description: "Episode 8 of the Leafra narrative.",
      ascii: ""
    },
    {
      id: "leafra-ep-9",
      label: "LEAFRA EPISODE 9",
      description: "Episode 9 of the Leafra narrative.",
      ascii: ""
    },
    {
      id: "leafra-ep-10",
      label: "LEAFRA EPISODE 10",
      description: "Episode 10 of the Leafra narrative.",
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
  <!-- TOP BAR: TITLE + SOCIAL ICONS + COPY ASCII -->
  <div class="top-bar">
  <div class="brand">Leafinite Architecture // conversations</div>

  <div class="top-links">
    {#if output}
      <button class="btn-copy top-copy" on:click={copyToClipboard}>
        copy ascii
      </button>
    {/if}
  </div>
</div>


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
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* ===== GLOBAL (DARK MODE) ===== */
main {
  min-height: 100vh;
  background: #000000;
  color: #ffffff;
  font-family: "Fira Code", monospace;
  padding: 1.3rem 1.8rem 2rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

/* MAX WIDTH CONTAINER */
.top-bar,
.layout {
  width: 100%;
  max-width: 1320px;
}

/* ===== TOP BAR ===== */
.top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
  gap: 1rem;
}

.brand {
  font-size: 0.9rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #ffffff;
}

.top-links {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.social-link {
  font-size: 0.75rem;
  padding: 0.25rem 0.6rem;
  border-radius: 999px;
  border: 1px solid #444444;
  background: #111111;
  color: #ffffff;
  text-decoration: none;

  &:hover {
    background: #1f1f1f;
  }
}

/* tombol copy di top bar */
.top-copy {
  font-size: 0.75rem;
  padding: 0.25rem 0.7rem;
  border-radius: 999px;
  border: 1px solid #444444;
  background: #111111;
  color: #ffffff;
  cursor: pointer;

  &:hover {
    background: #1f1f1f;
  }
}

/* ===== LAYOUT ===== */
.layout {
  display: flex;
  flex: 1 1 auto;
  min-height: 0;
  gap: 1.3rem;
}

/* ===== BACK BUTTON ===== */
.btn-back {
  width: 100%;
  text-align: left;
  font-size: 0.7rem;
  background: #101010;
  border: 1px solid #333333;
  color: #ffffff;
  padding: 0.5rem 0.7rem;
  border-radius: 6px;
  margin-bottom: 1rem;
  cursor: pointer;
  transition: 0.15s ease;

  &:hover {
    background: #181818;
  }
}

/* ===== SIDEBAR ===== */
.sidebar {
  flex: 0 0 260px;
  max-width: 320px;
  border-right: 1px solid #333333;
  padding-right: 1rem;
  display: flex;
  flex-direction: column;
  overflow: hidden;

  h2 {
    margin: 0;
    font-size: 0.8rem;
    letter-spacing: 0.08em;
    color: #f5f5f5;
    text-transform: uppercase;
  }

  .hint {
    margin: 0.35rem 0 0.9rem;
    font-size: 0.65rem;
    color: #aaaaaa;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    overflow-y: auto;
    flex: 1;
  }

  li {
    border: 1px solid #333333;
    border-radius: 6px;
    padding: 0.55rem 0.7rem;
    margin-bottom: 0.5rem;
    cursor: pointer;
    background: #101010;
    transition: 0.15s ease;

    .conv-label {
      font-size: 0.8rem;
      color: #ffffff;
      margin-bottom: 0.12rem;
    }

    .conv-desc {
      font-size: 0.7rem;
      color: #d0d0d0;
    }

    &:hover {
      background: #181818;
      border-color: #555555;
    }

    &.selected {
      background: #202020;
      border-color: #888888;
    }
  }
}

/* ===== TERMINAL ===== */
.terminal {
  flex: 1 1 auto;
  min-width: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  padding-left: 0;
}

/* HEADER TERMINAL */
.terminal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.6rem;
  border-bottom: 1px solid #333333;

  .title span {
    font-size: 0.85rem;
    color: #f5f5f5;
  }
}

/* OUTPUT TERMINAL */
.output {
  flex: 1 1 auto;
  overflow-y: auto;
  padding-right: 0.5rem;

  .ascii-wrap {
    width: 100%;
    margin: 0;
    overflow-x: auto;
  }

  pre {
    margin: 0;
    font-size: 0.9rem;
    line-height: 1.35;
    white-space: pre;
    color: #f5f5f5;
    font-family: "Fira Code", monospace;
  }

  .placeholder {
    font-size: 0.8rem;
    color: #aaaaaa;
  }
}

/* ===== RESPONSIVE ===== */
@media (max-width: 1100px) {
  .sidebar {
    flex: 0 0 230px;
  }
}

@media (max-width: 900px) {
  main {
    padding: 1rem;
  }

  .top-bar {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.4rem;
  }

  .layout {
    flex-direction: column;
  }

  .sidebar {
    border-right: none;
    border-bottom: 1px solid #333333;
    padding-right: 0;
    margin-bottom: 0.75rem;
  }

  .output pre {
    font-size: 0.8rem;
  }
}
</style>
