<svelte:options tag="flx-dmn-table" />

<script lang="ts">
  import { range as _range } from 'lodash/fp'

  let inputs = [
    {
      label: 'Season',
      inputExpression: '',
    },
    {
      label: 'How many guests',
      inputExpression: 'guestCount',
    },
  ]

  let rules = [
    {
      inputEntries: ['Fall', '<= 8', 'Spareribs'],
    },
  ]

  let outputs = [
    {
      label: 'Dish',
      name: 'desiredDish',
      typeRef: 'string',
    },
  ]

  let annotations = []

  function parseFeelExpression(expression: string): string {
    return
  }

  function addRow(): void {
    rules = [
      ...rules,
      { inputEntries: _range(0, outputs.length + inputs.length + 1).map((index) => null) },
    ]
  }

  function logDmn() {
    console.log(rules)
  }
</script>

<table>
  <thead>
    <tr>
      <th class="table-header" />
      {#each inputs as inputHead}
        <th class="table-header">{inputHead.label}</th>
      {/each}

      {#each outputs as outputHead}
        <th class="table-header">{outputHead.label}</th>
      {/each}

      <th class="table-header">Annotations</th>
    </tr>
  </thead>
  <tbody>
    {#each rules as rule, i}
      <tr class="border-data">
        <td class="border-data">{i + 1}</td>
        {#each rule.inputEntries as inputEntry}
          <td class="border-data">
            <input bind:value={inputEntry} />
          </td>
        {/each}
      </tr>
    {/each}

    <tr class="border-data">
      <td class="border-data"><button class="add-button" on:click={addRow}>+</button></td>
      <td class="border-data" />
      <td class="border-data" />
      <td class="border-data" />
    </tr>
  </tbody>
</table>

<button class="button" on:click={logDmn}>Log</button>

<style lang="postcss">
  @tailwind base;
  .button {
    @apply mt-4 rounded-md bg-blue-500 text-white px-4 py-2;
  }

  .table-header {
    @apply py-10 px-5 border;
  }

  .border-data {
    @apply border;
  }

  .add-button {
    @apply text-blue-500;
  }
</style>
