<script>
  import { onMount } from "svelte";
  const apiURL = "./data.json";
  let data = [];
  onMount(async function () {
    const response = await fetch(apiURL);
    data = await response.json();
  });

  let code;
</script>

<h1>Configurateur ABM TECNA</h1>
{#each data as category}
  <h2>{category.name}</h2>
  {#each category.content as form}
    <form>
      <fieldset>
        <legend>{form.name}</legend>
        {#each form.content as label}
          <div class="columns">
            <div>
              {label.name} :
              <div class="input-list">
                {#each label.content as input}
                  <label>
                    <input type="radio" bind:group={label.name} value={input} />
                    <span>{input}</span>
                  </label>
                {/each}
              </div>
            </div>
            <div>
              <details>
                <summary>Aide</summary>
                <p>Petite description avec images, texte, et schémas...</p>
              </details>
            </div>
          </div>
        {/each}
      </fieldset>
    </form>
  {/each}
{/each}

<input value={code} placeholder="Code" />
