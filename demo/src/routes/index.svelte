<script context="module">
  const is_browser = typeof window !== "undefined";

  import CodeMirror from "svelte-codemirror";
  // import CodeMirror, { set, update } from "svelte-codemirror";
  import "codemirror/lib/codemirror.css";

  if (is_browser) {
    import("../codeMirrorPlugins");
  }
</script>

<script>

  import { onMount } from "svelte";

  let value1 = ":b:{{1,0.25}imp}\909b;:s:{{1,0.25}imp}\909;:c:{{{1,0.66}imp,{1,0.8}imp}add}\909closed;:o:{{0.25,0.75}imp}\909open";
  let value2 = "MAIN -> SENTENCE '.' SENTENCE -> SUB _ VERB _ MOD  MD -> MD _ '*' _ E  {% function(d) {return {type: 'M', d:d, v:d[0].v*d[4].v}} %}";
  let cm1, cm2;
  let cmdEnter = () => console.log("cmd-Enter");
  let ctrlEnter = () => console.log("ctrl-Enter");
  let cmdPeriod = () => console.log("cmd-.");
  let ctrlPeriod = () => console.log("ctrl-.");
  let cmdForwardSlash = () => {
    // console.log("cmd-/");
  }
  let ctrlForwardSlash = () => {
    // console.log("ctrl-/");
  }

	onMount(async () => {

    cm1.set(value1, "js", 'monokai');

    cm2.set(value2, "ebnf");

	});

  const on = e => {
    console.log("DEBUG:on: ");
    console.log(e);
  }

</script>

<style>
  .codemirror-container {
    position: relative;
    width: 100%;
    height: 100%;
    border: none;
    line-height: 1.5;
    overflow: hidden;
  }
</style>

<svelte:head>
  <title>svelte-codemirror example</title>
</svelte:head>

<div class="codemirror-container flex">
  <div class="codemirror-container-sema">
    <CodeMirror bind:this={cm1}
                bind:value={value1}
                tab={false}
                on:change={ e => on(e) }
                on:focus={ e => on(e) }
                on:blur={ e => on(e) }
                on:refresh={ e => on(e) }
                on:gutterClick={ e => on(e) }
                on:viewportChange={ e => on(e) }
                {cmdEnter}
                {cmdPeriod}
                {ctrlEnter}
                {cmdForwardSlash}
                />
  </div>
  <br>

  <CodeMirror bind:this={cm2}
              bind:value={value2}
              on:change={ e => on(e) }
              on:focus={ e => on(e) }
              on:blur={ e => on(e) }
              on:refresh={ e => on(e) }
              on:gutterClick={ e => on(e) }
              on:viewportChange={ e => on(e) }
              {ctrlEnter}
              {cmdPeriod}
              {cmdForwardSlash}
              />
  <br>
  <button on:click="{ () => { value1 += value1 + '1'; cm2.update(value1); console.log(value1); }}" >Press me!</button>
</div>
