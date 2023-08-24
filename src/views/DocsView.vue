<script setup>
</script>

<template>
  <main>
    <h1 id="llama-terminal-completion"><a href="https://github.com/adammpkins/llama-terminal-completion">Llama Terminal Completion</a></h1>

    <h2 id="table-of-contents">Table of Contents</h2>
    <ul>
      <li><a href="#llama-terminal-completion">Llama Terminal Completion</a>
        <ul>
          <li><a href="#table-of-contents">Table of Contents</a></li>
          <li><a href="#installation">Installation</a>
            <ul>
              <li><a href="#llama-cpp-installation">Llama.cpp installation</a></li>
              <li><a href="#llama-terminal-completion-installation">Llama Terminal Completion installation</a></li>
              <li><a href="#environment-variables">Environment Variables</a></li>
            </ul>
          </li>
          <li><a href="#usage">Usage</a>
            <ul>
              <li><a href="#alias">Alias</a></li>
            </ul>
          </li>
          <li><a href="#contributing">Contributing</a></li>
          <li><a href="#license">License</a></li>
        </ul>
      </li>
    </ul>
    <p>This Python script interacts with the <a href="https://github.com/ggerganov/llama.cpp">llama.cpp</a> library to
      provide virtual assistant capabilities through the command line. It allows you to ask questions and receive
      intelligent responses, as well as generate Linux commands based on your prompts.</p>
    <h2 id="installation">Installation</h2>
    <h3 id="llama-cpp-installation">Llama.cpp installation</h3>
    <ol>
      <li>Clone the &#39;llama.cpp&#39; repository to your local machine
        <pre><code class="lang-bash">git <span class="hljs-keyword">clone</span> <span class="hljs-title">https</span>://github.com/ggerganov/llamacpp.git
</code></pre>
      </li>
      <li>Build the llama.cpp library by following the instructions in the llama.cpp repository. A good tutorial for this
        can be found at <a href="https://wandb.ai/capecape/LLMs/reports/How-to-Run-LLMs-Locally--Vmlldzo0Njg5NzMx">How to
          Run LLMs Locally</a></li>
    </ol>
    <h3 id="llama-terminal-completion-installation">Llama Terminal Completion installation</h3>
    <ol>
      <li>Clone the llama-terminal-completion repository to your local machine:
        <pre><code class="lang-bash">git <span class="hljs-keyword">clone</span> <span class="hljs-title">https</span>://github.com/adammpkins/llama-terminal-completion.git
</code></pre>
      </li>
      <li>Set up the environment variables (see below)</li>
    </ol>
    <h3 id="environment-variables">Environment Variables</h3>
    <p>Before using this script, you need to set up the <code>LLAMA_COMPLETION_DIR</code> and <code>LLAMA_CPP_DIR</code>
      environment variables. These variables point to the directories where the <code>llama-terminal-completion</code> and
      <code>llama.cpp</code> files are located, respectively. You can set these variables in your shell configuration file
      (e.g., <code>.bashrc</code> or <code>.zshrc</code>) like this:</p>
    <pre><code class="lang-bash"><span class="hljs-keyword">export</span> LLAMA_COMPLETION_DIR=<span class="hljs-string">"/path/to/llama-terminal-completion/"</span>
<span class="hljs-keyword">export</span> LLAMA_CPP_DIR=<span class="hljs-string">"/path/to/llama.cpp/"</span>
</code></pre>
    <p>Replace /path/to/llama-terminal-completion/ and /path/to/llama.cpp/ with the actual paths to the respective
      directories on your system.</p>
    <h2 id="usage">Usage</h2>
    <p>Open a terminal window.</p>
    <p>Navigate to the directory where the ask_llama.py script is located.</p>
    <p>Run the script with the desired options. Here are some examples:</p>
    <ul>
      <li>To generate a Linux command based on a prompt:
        <pre><code class="lang-bash">  python3 ask_llama.py <span class="hljs-comment">"list the contents of the current directory"</span>
</code></pre>
      </li>
      <li>
        <p>To ask a question to the virtual assistant:</p>
        <pre><code class="lang-bash">  python3 ask_llama<span class="hljs-selector-class">.py</span> -<span class="hljs-selector-tag">q</span> <span class="hljs-string">"How does photosynthesis work?"</span>
</code></pre>
      </li>
      <li>
        <p>To clear the history of commands:</p>
        <pre><code class="lang-bash">  python3 ask_llama<span class="hljs-selector-class">.py</span> -ch
</code></pre>
      </li>
    </ul>
    <p>For more options, you can run:</p>
    <pre><code class="lang-bash"><span class="hljs-keyword">python3</span> ask_llama.<span class="hljs-keyword">py</span> --<span class="hljs-keyword">help</span>
</code></pre>
    <p>Its output is as follows:</p>
    <pre><code class="lang-bash">Usage: python3 ask_llama.py [prompt]
Example: python3 ask_llama.py <span class="hljs-string">'list all files in the current directory'</span>
Options:
-q                ask <span class="hljs-keyword">a</span> question <span class="hljs-built_in">to</span> <span class="hljs-keyword">the</span> virtual assistant
-ch               <span class="hljs-built_in">clear</span> <span class="hljs-keyword">the</span> history <span class="hljs-keyword">of</span> commands
-cqh              <span class="hljs-built_in">clear</span> <span class="hljs-keyword">the</span> history <span class="hljs-keyword">of</span> questions
-h                show <span class="hljs-keyword">the</span> history <span class="hljs-keyword">of</span> commands
-qh               show <span class="hljs-keyword">the</span> history <span class="hljs-keyword">of</span> questions
-v                show <span class="hljs-keyword">the</span> <span class="hljs-built_in">version</span> <span class="hljs-keyword">of</span> llama-terminal-completion
<span class="hljs-comment">--help            show this help message and exit</span>
</code></pre>
  <h3 id="alias">Alias</h3>
  <p>You can create an alias for the script in your shell configuration file (e.g., <code>.bashrc</code> or
    <code>.zshrc</code>) like this:</p>
  <pre><code class="lang-bash"><span class="hljs-keyword">alias</span> <span class="hljs-title">ask</span>=<span class="hljs-string">"python3 /path/to/llama-terminal-completion/ask_llama.py"</span>
</code></pre>
  <p>Then you can run the script like this:</p>
  <pre><code class="lang-bash">ask <span class="hljs-comment">"list the contents of the current directory"</span>
</code></pre>
  <h2 id="contributing">Contributing</h2>
  <p>Contributions to this project are welcome! Feel free to fork the repository, make changes, and submit pull
    requests.</p>
  <h2 id="license">License</h2>
  <p>This project is licensed under the <a href="https://choosealicense.com/licenses/mit/">MIT License</a></p>


</main></template>

<style scoped>
 h1, h2, h3 {
    color: #333;
    font-family: 'Patua';
  }

  h1 {
    margin-top: 30px;
    font-size: 32px;
    color:#757cd4;

  }

  h2 {
    font-size: 24px;
    margin-top: 20px;
    color:#757cd4;

  }

  h3 {
    font-size: 20px;
    margin-top: 15px;
    color:#757cd4;
  }

  p {
    
    margin-top: 10px;
    margin-bottom: 10px;
  }

  ul, ol {
    margin: 0;
    padding-left: 20px;
  }

  ul ul, ol ul {
    list-style-type: none;
    margin-top: 5px;
    padding-left: 20px;
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
    background-color: #444444;
    padding: 10px;
    border-radius: 5px;
  }

  code {
    font-family: Consolas, Monaco, monospace;
    font-size: 14px;
  }

  .lang-bash {
    color: #ffffff;
  }

  .hljs-keyword {
    color: #ffffff;
  }

  .hljs-string {
    color: #ffffff;
  }

  .hljs-selector-tag {
    color: #ffffff;
  }

  .hljs-selector-class {
    color: #ffffff;
  }

  .hljs-built_in {
    color: #ffffff;
  }

  .hljs-comment {
    color: #ffffff
  }

  .hljs-title {
    color: #6f42c1;
  }

  .hljs-variable {
    color: #ffffff;
  }

  .hljs-type {
    color: #ffffff;
  }

  .hljs-section {
    color: #ffffff;
  }

  .hljs-title {
    color: #ffffff;
  }
</style>