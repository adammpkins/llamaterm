<template>
  <div class="about-container">
    <h1 id="what-is-llamaterm">What is LlamaTerm?</h1>
    <p class="intro">
      Ever wish you could look up Linux commands or ask questions and receive responses from the terminal? You probably
      need a paid service, an API key with paid usage, or at least an internet connection, right?
    </p>
    <p class="highlight"><strong>Not with LlamaTerm.</strong></p>
    <p>
      We run a Large Language Model (think ChatGPT) locally, on your personal machine, and generate responses from there.
      No cloud required. No API fees. Just you and your AI assistant.
    </p>
    
    <div class="features">
      <div class="feature">
        <h3>🔒 Private & Local</h3>
        <p>All processing happens on your machine. Your data never leaves your computer.</p>
      </div>
      <div class="feature">
        <h3>💰 No API Fees</h3>
        <p>Use models from Ollama, LM Studio, or llama.cpp without paying per-token fees.</p>
      </div>
      <div class="feature">
        <h3>🌐 Works Offline</h3>
        <p>Once set up, LlamaTerm works without an internet connection.</p>
      </div>
      <div class="feature">
        <h3>🔌 Flexible</h3>
        <p>Works with any OpenAI-compatible API—local or cloud-based.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.about-container {
  padding: 0;
}

h1, h2, h3 {
  font-family: "Patua";
}

h1 {
  margin-top: 30px;
  font-size: 32px;
  color: #757cd4;
}

.intro {
  font-size: 1.1em;
  line-height: 1.6;
}

.highlight {
  font-size: 1.3em;
  color: #757cd4;
  margin: 20px 0;
}

.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin-top: 30px;
}

.feature {
  background: rgba(117, 124, 212, 0.1);
  border-radius: 10px;
  padding: 20px;
  border: 1px solid rgba(117, 124, 212, 0.2);
}

.feature h3 {
  font-size: 18px;
  color: #757cd4;
  margin-bottom: 10px;
}

.feature p {
  font-size: 14px;
  line-height: 1.5;
  margin: 0;
}
</style>
