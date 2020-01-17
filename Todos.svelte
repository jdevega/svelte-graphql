<script>
  import { getClient, query } from "svelte-apollo";
  import { gql } from "apollo-boost";

  const GET_TODOS = gql`getTodos {id
            text
            done
          }
        `;

  const client = getClient();
  const todos = query(client, { query: GET_TODOS });
</script>
<h2>Todos</h2>
{#await $todos}
  Loading ...
{:then results}
  <ul>
    {#each results.data.getTodos as {id, done, text}, i}
      <li>{text}</li>
    {/each}
  </ul>
{:catch error}
  {error}
{/await}