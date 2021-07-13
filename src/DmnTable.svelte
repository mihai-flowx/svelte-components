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
      <th class="py-10 border" />
      {#each inputs as inputHead}
        <th class="py-10 px-5 border">{inputHead.label}</th>
      {/each}

      {#each outputs as outputHead}
        <th class="py-10 px-5 border">{outputHead.label}</th>
      {/each}

      <th class="py-10 px-5 border">Annotations</th>
    </tr>
  </thead>
  <tbody>
    {#each rules as rule, i}
      <tr class="border">
        <td class="border">{i + 1}</td>
        {#each rule.inputEntries as inputEntry}
          <td class="border">
            <input bind:value={inputEntry} />
          </td>
        {/each}
      </tr>
    {/each}

    <tr class="border">
      <td class="border"><button class="text-blue-500" on:click={addRow}>+</button></td>
      <td class="border" />
      <td class="border" />
      <td class="border" />
    </tr>
  </tbody>
</table>

<button class="mt-4 rounded-md bg-blue-500 text-white px-4 py-2" on:click={logDmn}>Log</button>
