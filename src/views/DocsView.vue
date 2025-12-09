<script setup>
</script>

<template>
  <main class="docs-container">
    <h1 id="llamaterm-docs"><a href="https://github.com/adammpkins/llama-terminal-completion">LlamaTerm Documentation</a></h1>

    <h2 id="table-of-contents">Table of Contents</h2>
    <ul class="toc">
      <li><a href="#installation">Installation</a></li>
      <li><a href="#getting-started">Getting Started</a></li>
      <li><a href="#core-commands">Core Commands</a></li>
      <li><a href="#piping-input">Piping Input</a></li>
      <li><a href="#chat-history">Chat History</a></li>
      <li><a href="#configuration">Configuration</a></li>
      <li><a href="#supported-providers">Supported Providers</a></li>
      <li><a href="#shell-completion">Shell Completion</a></li>
      <li><a href="#all-commands">All Commands Reference</a></li>
    </ul>

    <h2 id="installation">Installation</h2>

    <h3 id="quick-install">Quick Install (Recommended)</h3>
    <pre class="overflow-x-auto"><code class="lang-bash">curl -sSL https://raw.githubusercontent.com/adammpkins/llama-terminal-completion/main/install.sh | bash</code></pre>
    <p>This downloads the latest release and installs it to <code>/usr/local/bin</code>.</p>

    <h3 id="from-source">From Source</h3>
    <pre class="overflow-x-auto"><code class="lang-bash">git clone https://github.com/adammpkins/llama-terminal-completion.git
cd llamaterm
make install</code></pre>
    <p>Requires Go 1.21+.</p>

    <h2 id="getting-started">Getting Started</h2>
    <p>LlamaTerm works out of the box with <a href="https://ollama.ai">Ollama</a> running locally.</p>
    <pre class="overflow-x-auto"><code class="lang-bash"># Install Ollama (if not installed)
curl -fsSL https://ollama.ai/install.sh | sh

# Pull a model
ollama pull llama3.2

# Start using LlamaTerm
lt ask "What is the difference between TCP and UDP?"</code></pre>

    <h2 id="core-commands">Core Commands</h2>

    <h3 id="lt-ask"><code>lt ask &lt;question&gt;</code></h3>
    <p>Ask any question and get an AI response.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt ask "How do I find large files in Linux?"
lt ask "Explain recursion in simple terms"</code></pre>
    <p><strong>Options:</strong></p>
    <ul>
      <li><code>-c, --copy</code> — Copy response to clipboard</li>
    </ul>

    <h3 id="lt-cmd"><code>lt cmd &lt;description&gt;</code></h3>
    <p>Generate a shell command from a natural language description.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt cmd "find all .go files modified in the last week"
lt cmd "compress all images in this folder"</code></pre>
    <p><strong>Options:</strong></p>
    <ul>
      <li><code>--dry-run</code> — Show command without running</li>
      <li><code>-y, --yes</code> — Run immediately without confirmation</li>
    </ul>
    <p>LlamaTerm detects dangerous commands (<code>rm -rf</code>, <code>sudo</code>, etc.) and warns you before execution.</p>

    <h3 id="lt-quick"><code>lt quick &lt;description&gt;</code></h3>
    <p>Generate and run a command immediately (no confirmation).</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt quick "show disk usage"
lt quick "list running docker containers"</code></pre>

    <h3 id="lt-chat"><code>lt chat</code></h3>
    <p>Start an interactive chat session with conversation memory.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt chat
lt chat --resume  # Resume a previous conversation</code></pre>
    <p><strong>In-chat commands:</strong></p>
    <ul>
      <li><code>/help</code> — Show available commands</li>
      <li><code>/model</code> — Switch models</li>
      <li><code>/history</code> — Browse saved conversations</li>
      <li><code>/new</code> — Start a new conversation</li>
      <li><code>/clear</code> — Clear current chat</li>
      <li><code>Ctrl+H</code> — Open conversation history</li>
      <li><code>Ctrl+O</code> — Open model selector</li>
      <li><code>Ctrl+C</code> — Exit (auto-saves)</li>
    </ul>

    <h3 id="lt-explain"><code>lt explain &lt;file&gt; [question]</code></h3>
    <p>Analyze and explain code or file contents.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt explain main.go
lt explain config.yaml "What does this configure?"
lt explain error.log "What went wrong?"</code></pre>

    <h3 id="lt-fix"><code>lt fix &lt;error&gt;</code></h3>
    <p>Get help fixing errors.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt fix "Error: module not found"
npm run build 2>&amp;1 | lt fix</code></pre>

    <h3 id="lt-copy"><code>lt copy &lt;question&gt;</code></h3>
    <p>Ask a question and copy the response to clipboard.</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt copy "Write a git commit message for adding user auth"</code></pre>

    <h2 id="piping-input">Piping Input</h2>
    <p>LlamaTerm reads from stdin, letting you pipe content:</p>
    <pre class="overflow-x-auto"><code class="lang-bash">cat error.log | lt ask "What's wrong here?"
git diff | lt ask "Summarize these changes"
docker logs myapp | lt fix</code></pre>

    <h2 id="chat-history">Chat History</h2>
    <p>Conversations are automatically saved and can be resumed later.</p>
    <pre class="overflow-x-auto"><code class="lang-bash"># List saved conversations
lt history list

# Resume a conversation
lt chat --resume

# Delete a conversation
lt history delete &lt;id&gt;

# Clear all conversations
lt history clear</code></pre>

    <h2 id="configuration">Configuration</h2>
    <p>LlamaTerm can be configured via config file, environment variables, or CLI flags.</p>

    <h3 id="config-file">Config File</h3>
    <p>Location: <code>~/.config/lt/config.yaml</code></p>
    <pre class="overflow-x-auto"><code class="lang-yaml">base_url: http://localhost:11434/v1
model: llama3.2
api_key: ""
stream: true
max_tokens: 2048
temperature: 0.7</code></pre>
    <p>Create a config file interactively:</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt config init</code></pre>
    <p>View current config:</p>
    <pre class="overflow-x-auto"><code class="lang-bash">lt config show</code></pre>

    <h3 id="environment-variables">Environment Variables</h3>
    <pre class="overflow-x-auto"><code class="lang-bash">export LT_BASE_URL=https://api.openai.com/v1
export LT_MODEL=gpt-4o-mini
export LT_API_KEY=sk-...</code></pre>
    <p>Or use standard OpenAI environment variable:</p>
    <pre class="overflow-x-auto"><code class="lang-bash">export OPENAI_API_KEY=sk-...</code></pre>

    <h3 id="cli-flags">CLI Flags</h3>
    <pre class="overflow-x-auto"><code class="lang-bash">lt --base-url https://api.openai.com/v1 --model gpt-4o-mini ask "Hello"</code></pre>
    <table class="flags-table">
      <thead>
        <tr>
          <th>Flag</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr><td><code>--base-url</code></td><td>API base URL</td></tr>
        <tr><td><code>--api-key</code></td><td>API key</td></tr>
        <tr><td><code>-m, --model</code></td><td>Model to use</td></tr>
        <tr><td><code>--no-stream</code></td><td>Disable streaming output</td></tr>
        <tr><td><code>--max-tokens</code></td><td>Maximum tokens to generate</td></tr>
        <tr><td><code>--temperature</code></td><td>Temperature for generation</td></tr>
      </tbody>
    </table>

    <h2 id="supported-providers">Supported Providers</h2>
    <p>LlamaTerm works with any OpenAI-compatible API:</p>
    <table class="providers-table">
      <thead>
        <tr>
          <th>Provider</th>
          <th>Base URL</th>
          <th>API Key Required</th>
        </tr>
      </thead>
      <tbody>
        <tr><td><strong>Ollama</strong></td><td><code>http://localhost:11434/v1</code></td><td>No</td></tr>
        <tr><td><strong>LM Studio</strong></td><td><code>http://localhost:1234/v1</code></td><td>No</td></tr>
        <tr><td><strong>llama.cpp</strong></td><td><code>http://localhost:8080/v1</code></td><td>No</td></tr>
        <tr><td><strong>OpenAI</strong></td><td><code>https://api.openai.com/v1</code></td><td>Yes</td></tr>
        <tr><td><strong>Azure OpenAI</strong></td><td>Your deployment URL</td><td>Yes</td></tr>
        <tr><td><strong>Anthropic (via proxy)</strong></td><td>Proxy URL</td><td>Yes</td></tr>
        <tr><td><strong>Together AI</strong></td><td><code>https://api.together.xyz/v1</code></td><td>Yes</td></tr>
        <tr><td><strong>Groq</strong></td><td><code>https://api.groq.com/openai/v1</code></td><td>Yes</td></tr>
      </tbody>
    </table>

    <h2 id="shell-completion">Shell Completion</h2>
    <p>Enable tab completion for commands and flags:</p>
    <pre class="overflow-x-auto"><code class="lang-bash"># Bash
lt completion bash > /usr/local/etc/bash_completion.d/lt

# Zsh (add to ~/.zshrc)
source &lt;(lt completion zsh)

# Fish
lt completion fish > ~/.config/fish/completions/lt.fish</code></pre>

    <h2 id="all-commands">All Commands Reference</h2>
    <table class="commands-table">
      <thead>
        <tr>
          <th>Command</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr><td><code>lt ask &lt;question&gt;</code></td><td>Ask a question</td></tr>
        <tr><td><code>lt cmd &lt;description&gt;</code></td><td>Generate a shell command</td></tr>
        <tr><td><code>lt quick &lt;description&gt;</code></td><td>Generate and run immediately</td></tr>
        <tr><td><code>lt copy &lt;question&gt;</code></td><td>Ask and copy to clipboard</td></tr>
        <tr><td><code>lt chat</code></td><td>Interactive chat session</td></tr>
        <tr><td><code>lt explain &lt;file&gt;</code></td><td>Explain code or file</td></tr>
        <tr><td><code>lt fix &lt;error&gt;</code></td><td>Help fix an error</td></tr>
        <tr><td><code>lt config show</code></td><td>Show configuration</td></tr>
        <tr><td><code>lt config init</code></td><td>Create config file</td></tr>
        <tr><td><code>lt history list</code></td><td>List saved conversations</td></tr>
        <tr><td><code>lt history delete &lt;id&gt;</code></td><td>Delete a conversation</td></tr>
        <tr><td><code>lt history clear</code></td><td>Clear all conversations</td></tr>
        <tr><td><code>lt completion &lt;shell&gt;</code></td><td>Generate shell completion</td></tr>
        <tr><td><code>lt version</code></td><td>Show version info</td></tr>
        <tr><td><code>lt help</code></td><td>Show help</td></tr>
      </tbody>
    </table>

    <h2 id="contributing">Contributing</h2>
    <p>Contributions to this project are welcome! Feel free to fork the repository, make changes, and submit pull requests.</p>

    <h2 id="license">License</h2>
    <p>This project is licensed under the <a href="https://choosealicense.com/licenses/mit/">MIT License</a></p>
  </main>
</template>

<style scoped>
.docs-container {
  padding: 0;
  overflow-x: hidden;
}

h1, h2, h3 {
  color: #333;
  font-family: 'Patua';
}

h1 {
  margin-top: 30px;
  font-size: 32px;
  color: #757cd4;
}

h2 {
  font-size: 24px;
  margin-top: 40px;
  color: #757cd4;
  border-bottom: 2px solid rgba(117, 124, 212, 0.3);
  padding-bottom: 10px;
}

h3 {
  font-size: 20px;
  margin-top: 25px;
  color: #757cd4;
}

p {
  margin-top: 10px;
  margin-bottom: 10px;
  line-height: 1.6;
}

ul, ol {
  margin: 10px 0;
  padding-left: 25px;
}

li {
  margin: 5px 0;
  line-height: 1.5;
}

.toc {
  background: rgba(117, 124, 212, 0.1);
  border-radius: 10px;
  padding: 20px 20px 20px 40px;
  border: 1px solid rgba(117, 124, 212, 0.2);
}

.toc li {
  margin: 8px 0;
}

a {
  color: #757cd4;
  text-decoration: none;
  font-family: 'Patua';
}

a:hover {
  text-decoration: underline;
}

pre {
  margin-top: 10px;
  margin-bottom: 10px;
  background-color: #1e1e1e;
  padding: 15px;
  border-radius: 8px;
  overflow-x: auto;
}

code {
  font-family: 'SF Mono', Consolas, Monaco, monospace;
  font-size: 14px;
}

p code, li code, td code {
  background-color: rgba(117, 124, 212, 0.15);
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 13px;
}

.lang-bash, .lang-yaml {
  color: #d4d4d4;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin: 15px 0;
  font-size: 14px;
}

th, td {
  padding: 12px 15px;
  text-align: left;
  border-bottom: 1px solid rgba(117, 124, 212, 0.2);
}

th {
  background: rgba(117, 124, 212, 0.15);
  color: #757cd4;
  font-family: 'Patua';
}

tr:hover {
  background: rgba(117, 124, 212, 0.05);
}

.commands-table td:first-child,
.flags-table td:first-child {
  white-space: nowrap;
}
</style>